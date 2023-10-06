# Privacy UI

**Objective:** To provide the facility of abstraction of private details of users. It will also help in masking sensitive details and unmasking the information by authorized roles whenever needed.

## Workflow Details

**Masking / Un-Masking of Data**

Particular entries of an object from the search API will appear masked if it is enabled in the MDMS (mentioned in the technical implementation section below). This is based on roles and if the value is masked in UI, the eye icon will be available adjacent to it. Clicking on this icon allows users to unmask it.

<figure><img src="../../../../../.gitbook/assets/image (532).png" alt=""><figcaption></figcaption></figure>

Once the user clicks on the eye icon, the corresponding search API is called with `plainAccessRequest`object in the request info. This allows the data to be unmasked in the response object and leads to the refreshing of values and the whole data is visible. The eye icon will not be visible anymore.\


<figure><img src="../../../../../.gitbook/assets/image (168).png" alt=""><figcaption></figcaption></figure>

## **Technical Implementation Details** <a href="#technical-implementation-details" id="technical-implementation-details"></a>

The masking of data and its dependency on roles is defined in the following MDMS file: [egov-mdms-data/SecurityPolicy.json at develop · egovernments/egov-mdms-data (github.com)](https://github.com/egovernments/egov-mdms-data/blob/dab961bc1f7661eb69b25d6e27424010eadbc716/data/pb/DataSecurity/SecurityPolicy.json)

Let us take an example of an object in the MDMS file i.e. WnSConnection

{% code lineNumbers="true" %}
```
{
      "model": "WnSConnection",
      "uniqueIdentifier": {
        "name": "applicationNo",
        "jsonPath": "applicationNo"
      },
      "attributes": [
        {
          "name": "ownerType",
          "jsonPath": "connectionHolders/*/ownerType",
          "patternId": "005",
          "defaultVisibility": ""
        },        
        {
          "name": "plumberInfoMobileNumber",
          "jsonPath": "plumberInfo/*/mobileNumber",
          "patternId": "008",
          "defaultVisibility": ""
        },
        {
          "name": "relationship",
          "jsonPath": "connectionHolders/*/relationship",
          "patternId": "005",
          "defaultVisibility": ""
        }
      ],
      "roleBasedDecryptionPolicy": [
        {
          "roles": ["EMPLOYEE","CITIZEN","WS_CEMP","WS_DOC_VERIFIER","WS_FIELD_INSPECTOR","WS_APPROVER","WS_CLERK","SW_CEMP","SW_DOC_VERIFIER","SW_FIELD_INSPECTOR","SW_APPROVER","SW_CLERK"],
          "attributeAccessList": [
            
            {
              "attribute": "ownerType",
              "firstLevelVisibility": "MASKED",
              "secondLevelVisibility": ""
            },
            {
              "attribute": "plumberInfoMobileNumber",
              "firstLevelVisibility": "MASKED",
              "secondLevelVisibility": ""
            },
            {
              "attribute": "relationship",
              "firstLevelVisibility": "MASKED",
              "secondLevelVisibility": ""
            }
          ]
        }
      ]
    },
```
{% endcode %}

Here the unique identifier is defined as applicationNo, so from UI plain request object which is sent in Search API contains `recordId` as applicationNo. Similarly, the list of attributes mentioned here is received as masked by default in the response object from the Search API. The roles mentioned in the roles array defines the roles for which these attributes were to be masked.

&#x20;Masking in details Page

In the UI code repository, If any particular data has to be masked then we have to send a Privacy object along with corresponding data to `ApplicationDetailsTemplate`

Example:

<div align="left">

<figure><img src="../../../../../.gitbook/assets/image (535).png" alt=""><figcaption></figcaption></figure>

</div>

For water application details the connection holder details have to be masked. The privacy object is passed from the applicationdetails hook.

Relationship object of connection holder details below:

{% code lineNumbers="true" %}
```
 { title: "WS_CONN_HOLDER_OWN_DETAIL_RELATION_LABEL", value: wsDataDetails?.connectionHolders?.[0]?.relationship,
              privacy: { uuid: uuid, fieldName: ["relationship"], model: "WnSConnection",showValue: false,
              loadData: {
                serviceName: serviceType === "WATER" ? "/ws-services/wc/_search" : "/sw-services/swc/_search",
                requestBody: {},
                requestParam: { tenantId, applicationNumber },
                jsonPath: serviceType === "WATER" ? "WaterConnection[0].connectionHolders[0].relationship" : "SewerageConnections[0].connectionHolders[0].relationship",
                isArray: false,
              }, },
            },
```
{% endcode %}

Here uuid is the record id which we have to send for a particular model; fieldName is the name defined in the MDMS as well as the exact param which we receive in the response object; model is the model from SecurityPolicy MDMS; showValue is sent as true if we want to append any data with the newly unmasked data. Usually, this is used for property address and loadData is an object in which we sent the body and params for the API call that must be made in order to get the unmasked data. Refer code - [DIGIT-Dev/Search.js at 090ef18028a50f38222e426ec59ab9f123833af0 · egovernments/DIGIT-Dev (github.com)](https://github.com/egovernments/DIGIT-Dev/blob/090ef18028a50f38222e426ec59ab9f123833af0/frontend/micro-ui/web/micro-ui-internals/packages/libraries/src/services/molecules/WS/Search.js#L120)

`ApplicationDetailsTemplate` has the eye icon already integrated with Row Component, which can be enabled by passing the above privacy object. Refer code - [DIGIT-Dev/StatusTable.js at 090ef18028a50f38222e426ec59ab9f123833af0 · egovernments/DIGIT-Dev (github.com)](https://github.com/egovernments/DIGIT-Dev/blob/090ef18028a50f38222e426ec59ab9f123833af0/frontend/micro-ui/web/micro-ui-internals/packages/react-components/src/atoms/StatusTable.js)

**UnMaskComponent** is the main component which handles all the unmasking action through the eye icon. The following component must be integrated if the eye icon needs to be implemented in any given place.

{% code lineNumbers="true" %}
```
 const { isLoading, data } = Digit.Hooks.useCustomMDMS(
    Digit.ULBService.getStateId(),
    "DataSecurity",
    [{ name: "SecurityPolicy" }],
    {
      select: (data) => data?.DataSecurity?.SecurityPolicy?.find((elem) => elem?.model == privacy?.model) || {},
    }
  );
  const { privacy: privacyValue, updatePrivacy } = Digit.Hooks.usePrivacyContext();
  if (isLoading || privacy?.hide) {
    return null;
  }
  
  if (Digit.Utils.checkPrivacy(data, privacy) && iseyevisible) {
    sessionStorage.setItem("isPrivacyEnabled","true");
    return (
      <span
        onClick={() => {
          sessionStorage.setItem("eyeIconClicked",privacy?.fieldName);
          updatePrivacy(privacy?.uuid, privacy?.fieldName);
        }}
      >
      <div className={`tooltip`}>
        <PrivacyMaskIcon className="privacy-icon" style={style}></PrivacyMaskIcon>
            <span className="tooltiptext" style={{
                    fontSize: "medium",
                    width: "unset",
                    display: "block",
                    marginRight:"-60px",
                  }}>
                   {t("CORE_UNMASK_DATA")}
                  </span>
                </div>
      </span>
    );
  }
  return null;
});

```
{% endcode %}

This loads the MDMS data and filters it out as per the specified model for which the unmaskComponent is being called. Next, it calls the checkprivacy obejct to verify if privacy is enabled for that particular role and model (refer to below code for privacy check).

{% code lineNumbers="true" %}
```
export const checkPrivacy = (mdmsObj, privacyDetail) => {
  if (mdmsObj?.attributes?.some((ele) => (ele?.name === privacyDetail?.fieldName || privacyDetail?.fieldName?.includes(ele?.name) )&& ele?.defaultVisibility === "MASKED")) {
    return true;
  }
  const userInfo = Digit.UserService.getUser();
  const userRoles = userInfo?.info?.roles?.map((roleData) => roleData?.code);
  if (
    mdmsObj?.roleBasedDecryptionPolicy?.some(
      (ele) =>
        ele?.roles?.some((e) => userRoles?.includes(e)) &&
        ele?.attributeAccessList?.some(
          (ele) => (ele?.attribute === privacyDetail?.fieldName || privacyDetail?.fieldName?.includes(ele?.attribute)) && ele?.firstLevelVisibility === "MASKED" && ele?.secondLevelVisibility === ""
        )
    )
  ) {
    return true;
  }
  return false;
};
```
{% endcode %}

If the checkprivacy is returned true, the eye icon is visible and clicking on it calls the updateprivacy method defined in useprivacycontext hook: Refer - [DIGIT-Dev/usePrivacyContext.js at 090ef18028a50f38222e426ec59ab9f123833af0 · egovernments/DIGIT-Dev (github.com)](https://github.com/egovernments/DIGIT-Dev/blob/090ef18028a50f38222e426ec59ab9f123833af0/frontend/micro-ui/web/micro-ui-internals/packages/libraries/src/hooks/usePrivacyContext.js)

<div align="left">

<figure><img src="../../../../../.gitbook/assets/image (124).png" alt=""><figcaption></figcaption></figure>

</div>

This triggers the search hook called again with `plainAccessRequest` (mentioned in the above picture), but for that privacy object has to be sent in the hook for re-triggering.

{% code lineNumbers="true" %}
```
  let { isLoading, isError, data: applicationDetails, error } = Digit.Hooks.ws.useWSDetailsPage(t, tenantId, applicationNumber, serviceType, userInfo,{ privacy: Digit.Utils.getPrivacyObject() });
```
{% endcode %}

For all methods related to privacy, refer to the document here: [DIGIT-Dev/privacy.js at develop · egovernments/DIGIT-Dev (github.com)](https://github.com/egovernments/DIGIT-Dev/blob/090ef18028a50f38222e426ec59ab9f123833af0/frontend/micro-ui/web/micro-ui-internals/packages/libraries/src/utils/privacy.js)

Unmasking in Edit Details page

<figure><img src="../../../../../.gitbook/assets/image (414).png" alt=""><figcaption></figcaption></figure>

For enabling the eye icon in the text field similar steps have to be followed :

1. The search API Hook used to prefill the data in the edit screen should have a privacy object being sent in it.
2. Unmask component has to be defined with the corresponding component.

{% code lineNumbers="true" %}
```
  let { isLoading, isError, data: applicationDetails, error } = Digit.Hooks.ws.useWSDetailsPage(t, tenantId, details?.applicationNo, details?.applicationData?.serviceType,{privacy : Digit.Utils.getPrivacyObject() });
```
{% endcode %}

{% code lineNumbers="true" %}
```
render={(props) => (
                <div style={{display:"flex",alignItems:"baseline",marginRight:props.value?.includes("*")? "-20px" : "-4%"}}>
                <div className="employee-card-input employee-card-input--front" style={{ position: "relative", marginTop:"4px" }}>+91</div>
                <TextInput
                  //type="number"
                  value={props.value}
                  autoFocus={focusIndex.index === connectionHolderDetail?.key && focusIndex.type === "mobileNumber"}
                  errorStyle={(localFormState.touched.mobileNumber && errors?.mobileNumber?.message) ? true : false}
                  onChange={(e) => {
                    setMobileNumber(e.target.value)
                    props.onChange(e.target.value);
                    setFocusIndex({ index: connectionHolderDetail?.key, type: "mobileNumber" });
                  }}
                  labelStyle={{ marginTop: "unset" }}
                  onBlur={props.onBlur}
                  style={checkifPrivacyValid() && !(props.value?.includes("*")) ? (!(Digit.Utils.checkPrivacy(privacyData, { uuid:connectionHolderDetail?.uuid, fieldName: "connectionHoldersMobileNumber", model: "WnSConnectionOwner" })) && !(Digit.Utils.checkPrivacy(privacyData, { uuid:connectionHolderDetail?.uuid, fieldName: "mobileNumber", model: "User" })) ? {width:"96%"} : {width:"96%", background: "#FAFAFA"}) : {background: "#FAFAFA"}}
                />
                {checkifPrivacyValid() && <div style={{marginRight:"-10px",marginLeft:"10px"}}>
                <UnMaskComponent iseyevisible={props.value?.includes("*")?true:false} privacy={{ uuid:connectionHolderDetail?.uuid, fieldName: "connectionHoldersMobileNumber", model: "WnSConnectionOwner" }}></UnMaskComponent>
                </div>}
                </div>
```
{% endcode %}

Refer: Index page for edit details: [DIGIT-Dev/index.js at develop · egovernments/DIGIT-Dev (github.com)](https://github.com/egovernments/DIGIT-Dev/blob/develop/frontend/micro-ui/web/micro-ui-internals/packages/modules/ws/src/pages/employee/EditApplication/index.js)

## **MDMS Data**

SecurityPolicy.json is used to handle all privacy-related action

| MDMS Detail                                       | Module Details Name | Master Detail Name |
| ------------------------------------------------- | ------------------- | ------------------ |
| List of Privacy object and roles associated to it | `DataSecurity`      | `SecurityPolicy`   |



