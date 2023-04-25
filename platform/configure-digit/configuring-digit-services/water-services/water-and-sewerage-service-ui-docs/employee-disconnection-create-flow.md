---
description: >-
  Water and Sewerage disconnection application details feature for employees -
  technical implementation doc
---

# Employee: Disconnection Create Flow

**Objective:** The Water and Sewerage 'Apply Disconnection' is the major feature in WS Module. It allows Counter Employees to create Water and Sewerage Applications.

Every application is a part of the workflow.

## **Workflow Details** <a href="#validations" id="validations"></a>

Once a new application connection is activated, the system generates a consumer code. This code is used to route users to the connection details screen from the search/connection screen.

Clicking on the Take Action button displays multiple options based on conditions. Clicking on the Apply for Disconnection option routes users to the Disconnect Document Required screen.\


<figure><img src="../../../../../.gitbook/assets/image (425).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../../../../../.gitbook/assets/image (344).png" alt=""><figcaption></figcaption></figure>

#### **Validations** <a href="#validations" id="validations"></a>

* To disconnect, the connection should be in an **ACTIVE** state. Connections which are under **WORKFLOW** or **INACTIVE** are not eligible for disconnection.
* In cases dues are pending, the user has to clear the dues before applying for Disconnection.
* The Disconnect option itself is not displayed in the action list for the connection which is **INACTIVE**.

**Connection details**:[Employee: Water and Sewerage Connection Details](employee-connection-details.md)

Clicking on the Apply button routes users to the Disconnection apply screen.

<figure><img src="../../../../../.gitbook/assets/image (587).png" alt=""><figcaption></figcaption></figure>

**Acknowledgement screen**

Successful create and update calls routes users to the acknowledgement screen.

<figure><img src="../../../../../.gitbook/assets/image (576).png" alt=""><figcaption></figcaption></figure>

#### W\&S Application <a href="#w-and-s-application" id="w-and-s-application"></a>

Users get the acknowledgement form once they have created and submitted their application successfully. Processing of applications pending field inspection and user payment enables the download of the estimation letter and the sanction letter respectively. The section below provides the configuration for the document downloads.&#x20;

#### Acknowledgement Download

Users can download the acknowledgement after submitting the W\&S Create Application.

<figure><img src="../../../../../.gitbook/assets/image (561).png" alt=""><figcaption></figcaption></figure>

## Technical Implementation Details

File Path: [https://github.com/egovernments/DIGIT-Dev/blob/develop/frontend/micro-ui/web/micro-ui-internals/packages/modules/ws/src/pageComponents/WSDisconnectionDocsRequired.js](https://github.com/egovernments/DIGIT-Dev/blob/develop/frontend/micro-ui/web/micro-ui-internals/packages/modules/ws/src/pageComponents/WSDisconnectionDocsRequired.js)

File Path: [https://github.com/egovernments/DIGIT-Dev/blob/develop/frontend/micro-ui/web/micro-ui-internals/packages/modules/ws/src/pages/employee/DisconnectionApplication/index.js](https://github.com/egovernments/DIGIT-Dev/blob/develop/frontend/micro-ui/web/micro-ui-internals/packages/modules/ws/src/pages/employee/DisconnectionApplication/index.js)

&#x20;**Data fetch, load and render**

`ws-services/wc/_create`

`sw-services/swc/_create`

**Case 1: In the case of Water connections:**

* Clicking on Submit button calls the  `ws-services/wc/_create` API and creates the application. The update API `ws-services/wc/_update`is called after getting a successful response on creating the application.

**Case 2: In the case of Sewerage connections:**

* Clicking on Submit button calls the `sw-services/swc/_create` API and creates the application. The update API `sw-services/swc/_update` is called after getting a successful response on creating the application.

File Path: [https://github.com/egovernments/DIGIT-Dev/blob/develop/frontend/micro-ui/web/micro-ui-internals/packages/modules/ws/src/pages/employee/WSResponse.js](https://github.com/egovernments/DIGIT-Dev/blob/develop/frontend/micro-ui/web/micro-ui-internals/packages/modules/ws/src/pages/employee/WSResponse.js)

File Path: [https://github.com/egovernments/DIGIT-Dev/blob/develop/frontend/micro-ui/web/micro-ui-internals/packages/modules/ws/src/pages/employee/DisconnectionApplication/WSDisconnectionResponse.js](https://github.com/egovernments/DIGIT-Dev/blob/develop/frontend/micro-ui/web/micro-ui-internals/packages/modules/ws/src/pages/employee/DisconnectionApplication/WSDisconnectionResponse.js)

The code for the application PDF is written in the below-mentioned file.

File Path: [https://github.com/egovernments/DIGIT-Dev/blob/develop/frontend/micro-ui/web/micro-ui-internals/packages/modules/ws/src/utils/getWSAcknowledgementData.js](https://github.com/egovernments/DIGIT-Dev/blob/develop/frontend/micro-ui/web/micro-ui-internals/packages/modules/ws/src/utils/getWSAcknowledgementData.js)

## **Role Action Mapping**

| S.No. | API                             | Roles              | Action ID    |
| ----- | ------------------------------- | ------------------ | ------------ |
| 1     | `/egov-mdms-service/v1/_search` | `WS_CEMP, SW_CEMP` | `954`        |
| 2     | `/ws-services/wc/_create`       | `WS_CEMP, SW_CEMP` | `1899, 1917` |
| 3     | `/sw-services/swc/_create`      | `WS_CEMP, SW_CEMP` | `1899, 1917` |
| 4     | `/ws-services/wc/_update`       | `WS_CEMP, SW_CEMP` | `1899, 1917` |
| 5     | `/sw-services/swc/_update`      | `WS_CEMP, SW_CEMP` | `1899, 1917` |
| 6     | `/filestore/v1/files/url`       | `EMPLOYEE`         |              |

