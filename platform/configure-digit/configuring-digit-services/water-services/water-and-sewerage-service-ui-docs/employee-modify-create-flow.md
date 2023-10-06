---
description: >-
  Water and Sewerage modify create application feature for employees - technical
  implementation doc
---

# Employee: Modify Create Flow

**Objective:** The Apply and Modify feature in the WS module allows counter employees to create or modify Water and Sewerage applications.

Every application is a part of the workflow.

## **Workflow Details** <a href="#validations" id="validations"></a>

Once a new application connection is activated, the system generates the consumer code. This code is used to route users to the connection details screen from the search/connection screen.\
\
Clicking on the Take Action button displays multiple options based on conditions. Clicking on the Modify Connection option routes users to the modify screen.

<figure><img src="../../../../../.gitbook/assets/image (106).png" alt=""><figcaption></figcaption></figure>

![](<../../../../../.gitbook/assets/image (544).png>)

#### **Validations** <a href="#validations" id="validations"></a>

* To disconnect, the connection should be in an **ACTIVE** state. Connections which are under **WORKFLOW** or **INACTIVE** are not eligible for Modify.

**Connection details**: [Employee: Water and Sewerage Connection Details](employee-connection-details.md)

#### **Acknowledgement screen**

<div align="left">

<figure><img src="../../../../../.gitbook/assets/image (563).png" alt=""><figcaption></figcaption></figure>

</div>

#### W\&S-Application <a href="#w-and-s-application" id="w-and-s-application"></a>

Creating an application on the water and sewerage module generates an acknowledgement form that can be downloaded by users. Processing the applications pending field inspection and user payment generates the Estimation Letter and Sanction Letter respectively. Find the configuration details for enabling the download of these documents.

**Acknowledgement Download**

Users can download the acknowledgement after submitting the W\&S Create application.

<figure><img src="../../../../../.gitbook/assets/image (580).png" alt=""><figcaption></figcaption></figure>

## Technical Implementation Details

File Path: [https://github.com/egovernments/DIGIT-Dev/blob/develop/frontend/micro-ui/web/micro-ui-internals/packages/modules/ws/src/pages/employee/ModifyApplication/index.js](https://github.com/egovernments/DIGIT-Dev/blob/develop/frontend/micro-ui/web/micro-ui-internals/packages/modules/ws/src/pages/employee/ModifyApplication/index.js)

**Data fetch, load and render**:

`ws-services/wc/_create`

`sw-services/swc/_create`

**Case 1: In the case of Water connections:**

* Clicking on the Submit button calls the `ws-services/wc/_create` API and creates the application. The update API `ws-services/`is called after getting a successful response on creating the application.

**Case 2: In the case of Sewerage connections:**

* Clicking on Submit button calls the `sw-services/swc/_create` API and creates the application. The update API `sw-services/swc/_update`is called after getting a successful response on creating the application.

Successful create and update calls routes users to the acknowledgement screen.

File Path: [https://github.com/egovernments/DIGIT-Dev/blob/develop/frontend/micro-ui/web/micro-ui-internals/packages/modules/ws/src/pages/employee/WSResponse.js](https://github.com/egovernments/DIGIT-Dev/blob/develop/frontend/micro-ui/web/micro-ui-internals/packages/modules/ws/src/pages/employee/WSResponse.js)

File Path: [https://github.com/egovernments/DIGIT-Dev/blob/develop/frontend/micro-ui/web/micro-ui-internals/packages/modules/ws/src/pages/employee/WSResponse.js](https://github.com/egovernments/DIGIT-Dev/blob/develop/frontend/micro-ui/web/micro-ui-internals/packages/modules/ws/src/pages/employee/WSResponse.js)

For the application PDF, all related code is written to the W\&S folder in the below-mentioned file.

File Path: [https://github.com/egovernments/DIGIT-Dev/blob/develop/frontend/micro-ui/web/micro-ui-internals/packages/modules/ws/src/utils/getWSAcknowledgementData.js](https://github.com/egovernments/DIGIT-Dev/blob/develop/frontend/micro-ui/web/micro-ui-internals/packages/modules/ws/src/utils/getWSAcknowledgementData.js)

## **Role Action Mapping**

| API                             | Roles              | Action ID    |
| ------------------------------- | ------------------ | ------------ |
| `/egov-mdms-service/v1/_search` | `WS_CEMP, SW_CEMP` | `954`        |
| `/ws-services/wc/_create`       | `WS_CEMP, SW_CEMP` | `1899, 1917` |
| `/sw-services/swc/_create`      | `WS_CEMP, SW_CEMP` | `1899, 1917` |
| `/ws-services/wc/_update`       | `WS_CEMP, SW_CEMP` | `1899, 1917` |
| `/sw-services/swc/_update`      | `WS_CEMP, SW_CEMP` | `1899, 1917` |
| `/filestore/v1/files/url`       | `EMPLOYEE`         |              |

