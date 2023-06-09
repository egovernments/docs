# Stakeholder - Registration Flow

## **Overview** <a href="#objective" id="objective"></a>

This page provides details on the Stakeholder Registration workflow in the OBPAS module. Citizens have the option to submit registration applications for various stakeholders such as architects and construction companies.&#x20;

<div align="left">

<img src="../../../../../.gitbook/assets/Screenshot from 2021-09-30 10-20-48.png" alt="BPA Home Card">

</div>

## Workflow Details

### Apply For Stakeholder Application

Users can apply for stakeholder application by clicking on the “Register as a Stakeholder”, and while going through the workflow, can add all the information, according to the question asked, in the middle of the workflow after the correspondence address Create API will be called, and at the end of the flow, a summary screen will be visible for the review of the answers and on clicking the submit button an Update API will be called which will change the status from Initiated to Applied and Registration Application will get updated.

### Registration Flow

The stakeholder Document Required screen is displayed after login, which helps the user to understand the necessary documents needed to complete the new registration for stakeholders. A citizen info card is also shown at the bottom of the page containing additional information such as the maximum size of the file that can be uploaded.

<div align="left">

<img src="../../../../../.gitbook/assets/Screenshot from 2021-09-30 10-41-39.png" alt="Document Required Screen">

</div>

### TimeLine Component

The TimeLine component is present on all pages. It informs the users about the steppers in completing the application for registration.

<div align="left">

<img src="../../../../../.gitbook/assets/Screenshot from 2021-10-07 22-28-57.png" alt="TimeLine">

</div>

### Licensee Details&#x20;

In this step, users need to provide information about the License type and Licensee.

#### License Type

The system asks for the type of license that the user is registering for. If the user selects architecture, then a new field is displayed i.e. architecture number. For all other roles, no additional information user is required. All the roles are populated from the MDMS.

<div align="left">

<img src="../../../../../.gitbook/assets/Screenshot from 2021-10-07 22-26-32.png" alt="License Type">

</div>

#### Licensee Details

Here users have to provide the information of the person for whom the license application is being generated. By default, the name and mobile number field will be automatically pre-filled with the logged-in user data. Edits to this detail are disabled. Applicants must fill in the remaining information accordingly.

<div align="left">

<img src="../../../../../.gitbook/assets/Screenshot from 2021-10-07 22-32-30.png" alt="Licensee Details">

</div>

### Address Details

In this step, users have to enter their address details.

#### Permanent Address

Users have to provide a permanent address. This is mandatory information that the user needs to provide to move to proceed with the application.

<div align="left">

<img src="../../../../../.gitbook/assets/Screenshot from 2021-10-07 22-35-30.png" alt="Permanent Adress">

</div>

#### Correspondence Address

Here user gets the option to either pre-fill the form with the permanent address provided earlier or enter a different address. Users can also skip this step as it is non-mandatory.

<div align="left">

<img src="../../../../../.gitbook/assets/Screenshot from 2021-10-07 22-37-59.png" alt="Correspondence Address">

</div>

Clicking on the Next button calls the Create API. Further information is available in the technical Implementation details section.

### Document Details

#### Licensee Document Details

This screen displays a list of documents and their type (in dropdown format) from the MDMS. The document list displayed is as per the role selected by the user in the license step. Users have to upload all the mandatory documents in order to proceed further.

<div align="left">

<img src="../../../../../.gitbook/assets/Screenshot from 2021-10-07 22-42-20.png" alt="Document Details">

</div>

### Summary Page & Acknowledgement Screen

Users can cross-verify the data entered throughout the flow on the Summary page. In case of any change or update required, the edit icon available adjacent to the section header allows the users to make the changes. It redirects users to the particular section page and the whole flow is repeated again in order to submit the application.

Along with the application details, the fee estimate for the corresponding application is also shown on the summary page.

<div align="left">

<img src="../../../../../.gitbook/assets/Screenshot from 2021-10-07 22-48-38.png" alt="Fee Estimate">

</div>

The Update API is called for the BPAREG Application update. Update API snippet is given below:&#x20;

```
bpaRegUpdate: "/tl-services/v1/BPAREG/_update"
```

If the API response is successful, the Acknowledgement Screen is displayed. Else, the Failed Acknowledgement Screen is displayed.

<div align="left">

<img src="../../../../../.gitbook/assets/Screenshot from 2021-10-07 22-47-12.png" alt="Summary Page">

 

<img src="../../../../../.gitbook/assets/Screenshot from 2021-10-07 22-49-38.png" alt="Acknowledgement Page">

</div>

Click on the Make Payment option to pay the registration fees on the summary screen.

## **Technical Implementation**&#x20;

All the screen has been developed using the new-UI structure followed previously in FSM, PGR, PT and TL, few new components have been introduced such as TimeLine, Multi upload Document etc

The link for the Stakeholder Registration Main Index is given below, it can be used to understand the starting point of the flow:

[https://github.com/egovernments/DIGIT-Dev/blob/develop/frontend/micro-ui/web/micro-ui-internals/packages/modules/obps/src/pages/citizen/StakeholderRegistration/index.js](https://github.com/egovernments/DIGIT-Dev/blob/develop/frontend/micro-ui/web/micro-ui-internals/packages/modules/obps/src/pages/citizen/StakeholderRegistration/index.js)

The OBPAS module is segregated into a specified structure. The screen configuration details are available in the PageComponent folder and the configuration for routing of the pages is available in the config folder which is common for both citizens as well as employees. New components like TimeLine are defined in the component folder. Below is the snippet for folder structure and routing configuration.

<div align="left">

<img src="../../../../../.gitbook/assets/Screenshot from 2021-10-07 22-55-13.png" alt="">

</div>

The stakeholder config responsible for the routing of the pages is defined under the config folder. Click on the link below to access the code.

{% embed url="https://github.com/egovernments/DIGIT-Dev/blob/develop/frontend/micro-ui/web/micro-ui-internals/packages/modules/obps/src/config/stakeholderConfig.js" %}

```
 {
      head: "ES_NEW_APPLICATION_PROPERTY_ASSESSMENT",
      body: [
        {
          route: "stakeholder-docs-required",
          component: "StakeholderDocsRequired",
          key: "data",
          nextStep: "provide-license-type"
        },
        {
          type: "component",
          route: "provide-license-type",
          isMandatory: true,
          component: "LicenseType",
          texts: {
            headerCaption: "BPA_LICENSE_DET_CAPTION",
            header: "BPA_LICENSE_TYPE_LABEL",
            cardText: "BPA_LICENSE_TYPE_TEXT",
            submitBarLabel: "CS_COMMON_NEXT",
          },
          nextStep: "license-details",
          key: "LicneseType",
          withoutLabel: true,
          hideInEmployee: true,
        },
```

The Pages folder contains the high-level configuration for controlling the whole flow for citizens and employees. The flows for citizens include Apply flows, Send Back flows, Application details etc. These carry the index (the main starting point of the whole flow).

The main difference between the Stakeholder registration flow from the apply flow in other modules is that the Create API is called in between the flow and at the end, the Update API is called.

The code for Create API request object generation is found inside the correspondence address component. This API call is triggered when the user clicks on the Next button on the correspondence address page.

The hook used for this API call is `Digit.OBPSService.BPAREGCreate(payload, tenantId)` and payload can be found inside the gonext() method in the following file:

Code reference:

[https://github.com/egovernments/DIGIT-Dev/blob/develop/frontend/micro-ui/web/micro-ui-internals/packages/modules/obps/src/pageComponents/CorrospondenceAddress.js](https://github.com/egovernments/DIGIT-Dev/blob/develop/frontend/micro-ui/web/micro-ui-internals/packages/modules/obps/src/pageComponents/CorrospondenceAddress.js)

The Utils folder basically contains all the methods that are used throughout the OBPAS module, and if any common method needs to be declared here, which in turn can be imported into other files.&#x20;

For updating an application the Update API from BPAREG is called using the React hooks, which have been declared under hooks/elements/obps as OBPSService.

The response object from the Create API is used for the request object of Update API, with the addition of document details that the user has entered. This marks the status of the Application as Applied instead of initiated.

Below is the hook used for fetching the update API call.

```
const mutation = Digit.Hooks.obps.useStakeholderAPI(
    data?.address?.city ? data.address?.city?.code : tenantId,
    true
  );
```

This API is called in the Stakeholder Acknowledgement code, using the useEffect Hook.

Code reference:

{% embed url="https://github.com/egovernments/DIGIT-Dev/blob/develop/frontend/micro-ui/web/micro-ui-internals/packages/modules/obps/src/pages/citizen/StakeholderRegistration/StakeholderAcknowledgement.js" %}

## **MDMS Data**

Throughout the flow, a few of the page data is imported from MDMS. Following is the list of pages that use MDMS data. These pages .js files can be found under page components.

| PageComponent           | MDMS Detail                                 | Module Details Name        | Master Detail Name         |
| ----------------------- | ------------------------------------------- | -------------------------- | -------------------------- |
| StakeholderDocsRequired | List of documents required for registration | `StakeholderRegistraition` | `StakeholderRegistraition` |
| LicenseType             | License role options                        | `StakeholderRegistraition` | `StakeholderRegistraition` |
| LicenseDetails          | Gender                                      | `common-masters`           | `GenderType`               |
| StakeholderDocsRequired | Documents and its drop downs                | `StakeholderRegistraition` | `StakeholderRegistraition` |

For calling the MDMS data, React Hooks are used, so that it could be shared throughout the modules. Below is the little code snippet for the MDMS call.

```
const { data, isLoading } = Digit.Hooks.obps.useMDMS(state, "StakeholderRegistraition", "TradeTypetoRoleMapping");
```

## **Localization**

Localization keys are added in the ‘_rainmaker-bpareg_’ locale module. In future, if any new labels are implemented in the OBPS - Stakeholder (Citizen) they should be pushed in the locale DB under _rainmaker-bpareg_ locale module. Below is an example of a few locale labels.

## **API Call Role Action Mapping**

<table data-header-hidden><thead><tr><th width="150"></th><th width="294"></th><th></th><th></th></tr></thead><tbody><tr><td><a href="http://s.no/"><strong>S.No</strong></a><strong>.</strong></td><td><p><strong>API</strong></p><p> </p></td><td><strong>Action id</strong></td><td><strong>Roles</strong></td></tr><tr><td>1</td><td><code>/egov-mdms-service/v1/_search</code></td><td><code>954</code></td><td><code>CITIZEN</code></td></tr><tr><td>2</td><td><code>/tl-services/v1/BPAREG/_create</code></td><td> </td><td><code>CITIZEN</code></td></tr><tr><td>3</td><td><code>/filestore/v1/files/url</code></td><td><code>1528</code></td><td><code>CITIZEN</code></td></tr><tr><td>4</td><td><code>/billing-service/bill/v2/_fetchbill</code></td><td><code>1862</code></td><td><code>CITIZEN</code></td></tr><tr><td>5</td><td><code>/tl-calculator/billingslab/_search</code></td><td><code>1684</code></td><td><code>CITIZEN</code></td></tr><tr><td>6</td><td><code>/tl-services/v1/BPAREG/_update</code></td><td> </td><td><code>CITIZEN</code></td></tr><tr><td>7</td><td><code>/localization/messages/v1/_search</code></td><td><code>1531</code></td><td><code>CITIZEN</code></td></tr><tr><td>8</td><td><code>/tl-calculator/v1/BPAREG/_getbill</code></td><td> </td><td><code>CITIZEN</code></td></tr></tbody></table>



> [![Creative Commons License](https://i.creativecommons.org/l/by/4.0/80x15.png)_​_](http://creativecommons.org/licenses/by/4.0/)_All content on this page by_ [_eGov Foundation_](https://egov.org.in/) _is licensed under a_ [_Creative Commons Attribution 4.0 International License_](http://creativecommons.org/licenses/by/4.0/)_._
