---
description: >-
  Water & Sewerage create applications feature for citizen users - technical
  implementation doc
---

# Citizen: Create Application

**Objective:** Provide the UI technical implementation details for the Create applications feature available for citizen users.

## Workflow Details

To provide user facilities to add new W\&S connection applications and view the details of the connection and application currently on their number. It also allows the users to update the connection or edit the application.

![](<../../../../../.gitbook/assets/image (48).png>)

**Water & Sewerage Create**

Users can add new connections using the Apply For New Connection button. The workflow adds valid information, as per the question asked. At the end of the flow, a Check page is displayed on which the user can cross-verify the information entered. The application is created upon submission.

**Water & Sewerage Create Flow:**

WNS information screen is displayed after login, which helps the user to understand the necessary documents needed to complete the new registration for a new connection.

![](<../../../../../.gitbook/assets/image (132).png>)

**Property Details Flow:**

Users can either add the property details by using the property search of commonPT or can choose to create a lightweight property using the commonPT create. Both screens lead users to the property details page, which displays a summary of the property selected or created.

![](<../../../../../.gitbook/assets/image (61).png>)

**Connection Details Flow:**

Here users can either select to go with the owners of the property or can choose to add connection holder details. Users have 3 options to choose from in context to the type of connection required:

1. Water Connection
2. Sewerage Connection
3. Water and Sewerage Connection

Based on the selection, the create API is called.

{% code lineNumbers="true" %}
```
water_create: "/ws-services/wc/_create",
sewarage_create: "/sw-services/swc/_create",
```
{% endcode %}

<figure><img src="../../../../../.gitbook/assets/image (109).png" alt=""><figcaption></figcaption></figure>

**Document Details:**

Users can upload all documents related to the data entered. The list of documents is controlled by the MDMS data and hence can be modified as per requirements.

![](<../../../../../.gitbook/assets/image (62).png>)

Check Page & Acknowledgement Screens:

Users can cross-verify the data entered throughout the flow on the Check page. If any changes or updates are required to the data users can do this by clicking on the Edit option available in front of the section header. This routes them to the specific page where data needs to be changed and then the whole flow needs to be repeated again in order to submit the application.

For the final Initiation of the application Update API is being called, which is used to particularly send the data of document details:

{% code lineNumbers="true" %}
```
water_update: "/ws-services/wc/_update",
sewarage_update: "/sw-services/swc/_update"
```
{% endcode %}

If the API response is successful, then the Acknowledgement Screen is displayed. Else, the Failed Acknowledgement Screen is displayed.

![](<../../../../../.gitbook/assets/image (140).png>)![](<../../../../../.gitbook/assets/image (46).png>)

## **Technical Implementation Details**

The structure followed here is the same as in the previous modules. The path for the WNS Main Index is given below and can be used to understand the starting point of the flow:

/DIGIT-Dev/frontend/micro-ui/web/micro-ui-internals/packages/modules/ws/src/pages/citizen/WSCreate/index.js

The module had been segregated into a specified structure. The screen configuration is inside the PageComponent Folder, and the configuration for routing of the pages is mentioned in the config folder which is common for both citizen users as well as employees.

The Create API is called based on the service selected on the Connection Details page. The following hook call can be found on the respective pages :

/DIGIT-Dev/frontend/micro-ui/web/micro-ui-internals/packages/modules/ws/src/pageComponents/WSSewerageConnectionDetails.js

{% code lineNumbers="true" %}
```
 Digit.WSService.create(payload, "SEWERAGE")
              .then((result, err) => {
                setIsDisableForNext(false);
                let data = {...formData, SewerageConnectionResult: result, sewerageConnectionDetails : {proposedWaterClosets : proposedWaterClosets, proposedToilets : proposedToilets}  }
                //1, units
                onSelect("", data, "", true);
      
              })
              .catch((e) => {
                setIsDisableForNext(false);
                setShowToast({ key: "error" });
                setError(e?.response?.data?.Errors[0]?.message || null);
              });
```
{% endcode %}

/DIGIT-Dev/frontend/micro-ui/web/micro-ui-internals/packages/modules/ws/src/pageComponents/WSWaterConnectionDetails.js

{% code lineNumbers="true" %}
```
Digit.WSService.create(payload, "WATER")
        .then((result, err) => {
          setIsDisableForNext(false);
          let data = {...formData, WaterConnectionResult: result, waterConectionDetails : {proposedTaps : proposedTaps, proposedPipeSize : proposedPipeSize}  }
          //1, units
          onSelect("", data, "", true);

        })
        .catch((e) => {
          setIsDisableForNext(false);
          setShowToast({ key: "error" });
          setError(e?.response?.data?.Errors[0]?.message || null);
        });
```
{% endcode %}

After the check page, the Update API is called and this is available on the Acknowledgement page:

/DIGIT-Dev/frontend/micro-ui/web/micro-ui-internals/packages/modules/ws/src/pages/citizen/WSCreate/WSAcknowledgement.js

{% code lineNumbers="true" %}
```
 if(data?.serviceName?.code === "WATER" || data?.serviceName?.code === "BOTH"){
        tenantId = data?.cpt?.details?.tenantId || tenantId;
        let formdata = isEdit ? convertToEditWSUpdate(data) : convertToWSUpdate(data);
        WSmutation.mutate(formdata, {
          onSuccess,
        })
```
{% endcode %}

After completing the flow, the users can download the acknowledgement PDF form of the application created and the config for the PDF generation is available in the link given below:

/DIGIT-Dev/frontend/micro-ui/web/micro-ui-internals/packages/modules/ws/src/utils/getWSAcknowledgementData.js

## **MDMS Data**

Throughout the flow, a few of the page data is imported from the MDMS. Following is the list of pages using MDMS data. The pages .js files are available in the page component column.

| PageComponent             | MDMS Detail                                  | Module Detail Name                                                 |                                                              |
| ------------------------- | -------------------------------------------- | ------------------------------------------------------------------ | ------------------------------------------------------------ |
| WSDocsRequired            | List of documents required for each category | `ws-services-masters`                                              | `Documents`                                                  |
| WSConnectionHolderDetails | Gender List                                  | <p><code>common-masters,</code></p><p><code>PropertyTax</code></p> | <p><code>GenderType</code>,</p><p><code>OwnerType</code></p> |
| WSWaterConnectionDetails  | Pipe Size                                    | `ws-services-calculation`                                          | `PipeSize`                                                   |
| WSDocumentDetails         | List of documents to be uploaded             | `ws-services-masters`                                              | `Documents`                                                  |

For calling the MDMS data React Hooks are used so that it could be shared throughout the modules. Below is the little code snippet for the call used for MDMS.

{% code lineNumbers="true" %}
```
 const { isLoading: wsDocsLoading, data: wsDocs } = Digit.Hooks.ws.WSSearchMdmsTypes.useWSServicesMasters(tenantId);
```
{% endcode %}

## **Localization**

The localization keys are added under the ‘_rainmaker-ws_’ locale module. In future, if any new labels are implemented in the Water and Sewerage they should also be pushed in the locale DB within the _rainmaker-ws_ locale module.

## &#x20;API **Role Action Mapping**

| API                             | Roles   | Action ID    |
| ------------------------------- | ------- | ------------ |
| `/egov-mdms-service/v1/_search` | CITIZEN | `954`        |
| `/ws-services/wc/_create`       | CITIZEN | `1899, 1917` |
| `/sw-services/swc/_create`      | CITIZEN | `1899, 1917` |
| `/ws-services/wc/_update`       | CITIZEN | `1899, 1917` |
| `/sw-services/swc/_update`      | CITIZEN | `1899, 1917` |
| `/filestore/v1/files/url`       | CITIZEN |              |

