---
description: >-
  Water and Sewerage disconnection application details feature for employees -
  technical implementation doc
---

# Employee: Disconnection Application Details

**Objective:** Provide employees with specific workflow actions.

This page provides the workflow details and actions for water and sewerage disconnection application details.&#x20;

## Workflow Details

#### **Application Details**

Clicking on the Application Number in the inbox/search screen routes users to the disconnection application details screen.\
A search call is made before rendering the screen and details are populated based on the search response.

**Application Details Screen**

<figure><img src="../../../../../.gitbook/assets/image (148).png" alt=""><figcaption></figcaption></figure>

#### Application Timeline

<figure><img src="../../../../../.gitbook/assets/image (291).png" alt=""><figcaption></figcaption></figure>

#### Downloads <a href="#downloads" id="downloads"></a>

Application Form

<figure><img src="../../../../../.gitbook/assets/image (265).png" alt=""><figcaption></figcaption></figure>

**Disconnection Notice**

<figure><img src="../../../../../.gitbook/assets/image (177).png" alt=""><figcaption></figcaption></figure>

**Water & Sewerage Disconnection Workflow Table**

| **#** | **Action**            | **Role**                   | **From State**                                                                       | **To State**                                             |
| ----- | --------------------- | -------------------------- | ------------------------------------------------------------------------------------ | -------------------------------------------------------- |
| 1     | Initiate Application  | Citizen/ Counter Employee  |                                                                                      | Initiated                                                |
| 2     | Submit Application    | Citizen/ Counter Employee  | Initiated                                                                            | Pending for document verification                        |
| 3     | Verify and Forward    | Document Verifier          | Pending for document verification                                                    | Pending for field inspection                             |
| 4     | Verify and Forward    | Field Inspector            | Pending for field inspection                                                         | Pending approval for disconnection                       |
| 5     | Send Back             | Document Verifier          | Pending for document verification                                                    | Pending for counter employee action                      |
| 6     | Send Back             | Field Inspector            | Pending for Field inspection                                                         | Pending for document verification                        |
| 7     | Send Back             | Approver                   | Pending approval for disconnection                                                   | Pending for field inspection                             |
| 8     | Send Back To Citizen  | **\<roles having access>** | **\<Current Status>**                                                                | Pending for citizen action                               |
| 9     | Re-submit             | Citizen/ Counter Employee  | <p>Pending for citizen action</p><p>OR</p><p>Pending for counter employee action</p> | <**To the status application was sent back to citizen>** |
| 12    | Approve               | Approver                   | Pending approval for disconnection                                                   | Pending for payment                                      |
| 13    | Reject                | **\<roles having access>** | **\<Current Status>**                                                                | Rejected                                                 |
| 14    | Payment/ Collection   | Citizen/ Counter Employee  | Pending for payment                                                                  | Pending for disconnection execution                      |
| 15    | Execute Disconnection | Clerk                      | Pending for disconnection execution                                                  | <p>Disconnection Executed</p><p> </p>                    |

## **Implementation Details**

**Application Details File Path:** [https://github.com/egovernments/DIGIT-Dev/blob/develop/frontend/micro-ui/web/micro-ui-internals/packages/modules/ws/src/pages/employee/ApplicationDetails.js](https://github.com/egovernments/DIGIT-Dev/blob/develop/frontend/micro-ui/web/micro-ui-internals/packages/modules/ws/src/pages/employee/ApplicationDetails.js)

&#x20;**Hook details for application details search:**

```
let { isLoading, isError, data: applicationDetails, error } = Digit.Hooks.ws.useDisConnectionDetails(t, tenantId, applicationNumber, serviceType);
```

**Disconnection Notice Download File Path:** [https://github.com/egovernments/DIGIT-Dev/blob/develop/frontend/micro-ui/web/micro-ui-internals/packages/modules/ws/src/pages/employee/DisconnectionDetails.js](https://github.com/egovernments/DIGIT-Dev/blob/develop/frontend/micro-ui/web/micro-ui-internals/packages/modules/ws/src/pages/employee/DisconnectionDetails.js)

**Application Form Download File Path:** [https://github.com/egovernments/DIGIT-Dev/blob/develop/frontend/micro-ui/web/micro-ui-internals/packages/modules/ws/src/pages/employee/DisconnectionDetails.js](https://github.com/egovernments/DIGIT-Dev/blob/develop/frontend/micro-ui/web/micro-ui-internals/packages/modules/ws/src/pages/employee/DisconnectionDetails.js)

The timeline view is common for all modules. **Timeline view file path:** [https://github.com/egovernments/DIGIT-Dev/blob/develop/frontend/micro-ui/web/micro-ui-internals/packages/modules/templates/ApplicationDetails/index.js](https://github.com/egovernments/DIGIT-Dev/blob/develop/frontend/micro-ui/web/micro-ui-internals/packages/modules/templates/ApplicationDetails/index.js)

## **Localisation Details**

Localisation keys are added in the ‘_rainmaker-ws_’ locale module.

## **API Call Role Action Mapping**

| S.No. | API                                                                                          | Action ID                                         | Roles                                                                                                                                                                                                          |
| ----- | -------------------------------------------------------------------------------------------- | ------------------------------------------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| 1     | `/access/v1/actions/mdms/_get`                                                               | `870`                                             |                                                                                                                                                                                                                |
| 2     | `/user/_search`                                                                              | `604`                                             |                                                                                                                                                                                                                |
| 3     | `/localization/messages/v1/_search`                                                          | `1531`                                            |                                                                                                                                                                                                                |
| 4     | `/egov-workflow-v2/egov-wf/businessservice/_search`                                          | `1743`                                            | `EMPLOYEE`                                                                                                                                                                                                     |
| 5     | `/ws-services/wc/_search`                                                                    | `1900`                                            | `WS_CEMP`,`WS_DOC_VERIFIER`,`WS_FIELD_INSPECTOR`,`WS_APPROVER`,`WS_CLERK`                                                                                                                                      |
| 6     | `/sw-services/swc/_search`                                                                   | `1940`                                            | `SW_CEMP`,`SW_DOC_VERIFIER`,`SW_FIELD_INSPECTOR`,`SW_CLERK`                                                                                                                                                    |
| 7     | `/property-services/property/_search`                                                        | `1897`                                            | `PT_CEMP`,`PT_DOC_VERIFIER`,`PT_FIELD_INSPECTOR`,`PT_APPROVER`                                                                                                                                                 |
| 8     | `/ws-services/wc/_create`                                                                    | `1899`                                            | `WS_CEMP`                                                                                                                                                                                                      |
| 9     | `/filestore/v1/files/url`                                                                    | `1528`                                            | `EMPLOYEE`                                                                                                                                                                                                     |
| 10    | `/ws-services/wc/_update`                                                                    | `1901`                                            | `WS_CEMP`,`WS_DOC_VERIFIER`,`WS_FIELD_INSPECTOR`,`WS_APPROVER`,`WS_CLERK`                                                                                                                                      |
| 11    | `/sw-services/swc/_update`                                                                   | `1939`                                            | `SW_CEMP`,`SW_DOC_VERIFIER`,`SW_FIELD_INSPECTOR`,`SW_CLERK`                                                                                                                                                    |
| 12    | /`ws-calculator/waterCalculator/_estimate` and `/sw-calculator/sewerageCalculator/_estimate` | <p><code>1966,</code></p><p><code>1967</code></p> | <p><code>WS_CEMP</code>,<code>WS_DOC_VERIFIER</code>,<code>WS_FIELD_INSPECTOR</code>,<code>WS_APPROVER</code>,<code>WS_CLERK</code></p><p><code>SW_CEMP,SW_DOC_VERIFIER,SW_FIELD_INSPECTOR,SW_CLERK</code></p> |
| 13    | `/egov-hrms/employees/_search`                                                               | `1752`                                            |                                                                                                                                                                                                                |

Find the login credentials and details in the document here: [<img src="https://developers.google.com/drive/images/drive_icon.png" alt="" data-size="line">DIGIT Login Credentials](https://docs.google.com/spreadsheets/d/15p6dmlVUXvopvzyyG06ty2rxtffSMQxN5F2l2FSWoFA/edit#gid=0)
