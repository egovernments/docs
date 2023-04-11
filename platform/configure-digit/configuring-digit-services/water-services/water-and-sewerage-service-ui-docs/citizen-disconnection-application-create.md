---
description: >-
  Water and Sewerage disconnection application for citizen users - technical
  implementation doc
---

# Citizen: Disconnection Application Create

**Objective:** To provide user facilities to disconnect an active W\&S connection when they are not using the service. So, that they don’t have to pay for any charges

#### **Validations** <a href="#validations" id="validations"></a>

* To disconnect, connection should be in **ACTIVE** state. Connections which are under **WORKFLOW** or **INACTIVE** are not eligible for disconnection.
* In cases dues are pending, user has to clear the dues before applying for Disconnection.
* ‘Disconnect’ option itself is not displayed in the action list for the connection which are **INACTIVE**.

![](<../../../../../.gitbook/assets/image (64).png>)![](<../../../../../.gitbook/assets/image (176).png>)![](<../../../../../.gitbook/assets/image (59).png>)

&#x20;**Route**&#x20;

My Connections → View Connection Details → Disconnect

Clicking on Disconnect it navigates to the Water and Sewerage Disconnection Application Document required screen.

![](<../../../../../.gitbook/assets/image (57).png>)

File Path: [https://github.com/egovernments/DIGIT-Dev/blob/develop/frontend/micro-ui/web/micro-ui-internals/packages/modules/ws/src/pageComponents/WSDisconnectionDocsRequired.js](https://github.com/egovernments/DIGIT-Dev/blob/develop/frontend/micro-ui/web/micro-ui-internals/packages/modules/ws/src/pageComponents/WSDisconnectionDocsRequired.js)

&#x20;![](<../../../../../.gitbook/assets/image (63).png>)

File Path: [https://github.com/egovernments/DIGIT-Dev/blob/develop/frontend/micro-ui/web/micro-ui-internals/packages/modules/ws/src/pageComponents/WSDisconnectionForm.js](https://github.com/egovernments/DIGIT-Dev/blob/develop/frontend/micro-ui/web/micro-ui-internals/packages/modules/ws/src/pageComponents/WSDisconnectionForm.js)

**Date Validation**

On Clicking on Next button in the document required screen,

if the proposed date is after \<slaDays for disconnection> it will route to Application form Water & Sewerage Disconnection, else it will throw an error in the form of toast messgae, “Date should be after \<slaDays for disconnection> from application create Date“.

To get the SLA days `/egov-workflow-v2/egov-wf/businessservice/_search?businessServices=DisconnectWSConnection` API call is made on load of Application Form Page

&#x20;

**Technical Implementation Details:**

Initial MDMS call is being made on page load

**Mdms data :**

Documents: [<img src="https://github.com/fluidicon.png" alt="" data-size="line">egov-mdms-data/DisconnectionDocuments.json at QA · egovernments/egov-mdms-data](https://github.com/egovernments/egov-mdms-data/blob/QA/data/pb/ws-services-masters/DisconnectionDocuments.json)

Disconnection Type: [<img src="https://github.com/fluidicon.png" alt="" data-size="line">egov-mdms-data/disconnectionType.json at QA · egovernments/egov-mdms-data](https://github.com/egovernments/egov-mdms-data/blob/QA/data/pb/ws-services-masters/disconnectionType.json)

&#x20;

On Clicking on Next button in the Application Form Screen , it will route to Upload Documents Screen

File Path: [https://github.com/egovernments/DIGIT-Dev/blob/develop/frontend/micro-ui/web/micro-ui-internals/packages/modules/ws/src/pageComponents/WSDisconnectionDocumentsForm.js](https://github.com/egovernments/DIGIT-Dev/blob/develop/frontend/micro-ui/web/micro-ui-internals/packages/modules/ws/src/pageComponents/WSDisconnectionDocumentsForm.js)

![](<../../../../../.gitbook/assets/image (123).png>)

On Clicking on Next button in the Upload Documents Screen , it will route to Summary Check Page Screen

File Path: [https://github.com/egovernments/DIGIT-Dev/blob/develop/frontend/micro-ui/web/micro-ui-internals/packages/modules/ws/src/pages/citizen/WSDisconnection/CheckPage.js](https://github.com/egovernments/DIGIT-Dev/blob/develop/frontend/micro-ui/web/micro-ui-internals/packages/modules/ws/src/pages/citizen/WSDisconnection/CheckPage.js)

![](<../../../../../.gitbook/assets/image (91).png>)

In Check Page you can edit the entered data for Disconnection.

On Clicking on Submit button in the Check Page Screen , it will make water or sewerage create and update API calls.

**Data fetch , load and render** :

* `ws-services/wc/_create`

**Payload: `WaterConnection: {`**

`...data,`

`isdisconnection : true,`

`isDisconnectionTemporary:` `true (if Temporary Disconnection selected else false)`,

`disconnectionReason`: ““

&#x20;

**`},`**

`disconnectRequest`: true

* `sw-services/swc/_create`

**Payload: `WaterConnection: {`**

`...data,`

`isdisconnection : true,`

`isDisconnectionTemporary:` `true (if Temporary Disconnection selected else false)`,

`disconnectionReason`: ““

&#x20;

**`},`**

`disconnectRequest`: true

* `ws-services/wc/_update`

**Payload: `WaterConnection: {`**

`...data,`

`isdisconnection : true,`

`isDisconnectionTemporary:` `true (if Temporary Disconnection selected else false)`,

`disconnectionReason`: ““

&#x20;

**`},`**

`disconnectRequest`: true

* `sw-services/swc/_update`

**Payload: `WaterConnection: {`**

`...data,`

`applicationType: if(Water Application) "DISCONNECT_WATER_CONNECTION" else (if Sewerage Application) "DISCONNECT_SEWERAGE_CONNECTION",`   &#x20;

`processInstance: {`

`...data?.processInstance,`

`businessService: if(Water Application) "DisconnectWSConnection" else (if Sewerage Application) "DisconnectSWConnection",`

`action: "SUBMIT_APPLICATION",     }`

&#x20;

**`},`**

After the Success of the Create and Update calls it routes users to the Disconnection Acknowledgement screen.

File Path: [https://github.com/egovernments/DIGIT-Dev/blob/develop/frontend/micro-ui/web/micro-ui-internals/packages/modules/ws/src/pageComponents/WSDisconnectAcknowledgement.js](https://github.com/egovernments/DIGIT-Dev/blob/develop/frontend/micro-ui/web/micro-ui-internals/packages/modules/ws/src/pageComponents/WSDisconnectAcknowledgement.js)

![](<../../../../../.gitbook/assets/image (173).png>)

Clicking on the Download Acknowledgement Form button downloads the Water or Sewerage Disconnection Acknowledgement PDF.

&#x20;

\
