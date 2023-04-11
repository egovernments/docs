---
description: >-
  Water and Sewerage modify application feature for employees - technical
  implementation doc
---

# Employee: Modify Application Details

**Objective:** Provide employees with specific workflow actions.

The same screen is used for both application details and to modify application details. The page provides the details of these workflows based on the conditions.

## **Workflow Details**

#### **Modify Application Details**

Clicking on the Application Number in the inbox/search screen/connection search routes users to the application details screen. A search call is made before rendering the screen and details are populated based on the search response.

**Modify Application Details Screen**

<figure><img src="../../../../../.gitbook/assets/image (169).png" alt=""><figcaption></figcaption></figure>

**Timeline View:**

![](<../../../../../.gitbook/assets/image (52).png>)

#### Downloads <a href="#downloads" id="downloads"></a>

<figure><img src="../../../../../.gitbook/assets/image (309).png" alt=""><figcaption></figcaption></figure>

**Water & Sewerage Workflow Table**

| **Role**                                     | **Action**       | **Next State**  | **Status**           |
| -------------------------------------------- | ---------------- | --------------- | -------------------- |
| Citizen/ Counter Employee/WS\_CEMP/ SW\_CEMP | INITIATE         | INITIATED       | INITIATED            |
| WS\_APPROVER / SW\_APPROVER                  | VERIFY \&FORWARD | PENDINGAPPROVAL | Pending for APproval |
| WS\_APPROVER / SW\_APPROVER                  | APPROVE          | Approved        | Approved             |
| WS\_APPROVER / SW\_APPROVER                  | REJECT           | Rejected        | Rejected             |

## **Implementation Details**

**Hook details for application details search:**

```
  let { isLoading, isError, data: applicationDetails, error } = Digit.Hooks.ws.useWSModifyDetailsPage(t, tenantId, applicationNumber, serviceType, userInfo, { privacy: Digit.Utils.getPrivacyObject() });
```

**File Path:** [https://github.com/egovernments/DIGIT-Dev/blob/develop/frontend/micro-ui/web/micro-ui-internals/packages/modules/ws/src/pages/employee/ModifyApplicationDetails.js](https://github.com/egovernments/DIGIT-Dev/blob/develop/frontend/micro-ui/web/micro-ui-internals/packages/modules/ws/src/pages/employee/ModifyApplicationDetails.js)

It is common for all modules, find the path here: [https://github.com/egovernments/DIGIT-Dev/blob/develop/frontend/micro-ui/web/micro-ui-internals/packages/modules/templates/ApplicationDetails/index.js](https://github.com/egovernments/DIGIT-Dev/blob/develop/frontend/micro-ui/web/micro-ui-internals/packages/modules/templates/ApplicationDetails/index.js)

**Method Reference:**

`const applicationDownloadObject = { order: 3, label: t("WS_APPLICATION"), onClick: handleDownloadPdf, };`&#x20;

File Path: [https://github.com/egovernments/DIGIT-Dev/blob/develop/frontend/micro-ui/web/micro-ui-internals/packages/modules/ws/src/pages/employee/ModifyApplicationDetails.js](https://github.com/egovernments/DIGIT-Dev/blob/develop/frontend/micro-ui/web/micro-ui-internals/packages/modules/ws/src/pages/employee/ModifyApplicationDetails.js)

## **Localisation Details**

Localisation keys are added in the ‘_rainmaker-ws_’ locale module.

**Water & Sewerage Workflow:**

| **Role**                                     | **Action**       | **Next State**  | **Status**           |
| -------------------------------------------- | ---------------- | --------------- | -------------------- |
| Citizen/ Counter Employee/WS\_CEMP/ SW\_CEMP | INITIATE         | INITIATED       | INITIATED            |
| WS\_APPROVER / SW\_APPROVER                  | VERIFY \&FORWARD | PENDINGAPPROVAL | Pending for APproval |
| WS\_APPROVER / SW\_APPROVER                  | APPROVE          | Approved        | Approved             |
| WS\_APPROVER / SW\_APPROVER                  | REJECT           | Rejected        | Rejected             |

**Employee Roles and Credentials:** The login credentials and details are available in the document here:[<img src="https://developers.google.com/drive/images/drive_icon.png" alt="" data-size="line">DIGIT Login Credentials](https://docs.google.com/spreadsheets/d/15p6dmlVUXvopvzyyG06ty2rxtffSMQxN5F2l2FSWoFA/edit#gid=0)

## **API Call Role Action Mapping**

| S.No | API                                                                                          | Action ID                                         | Roles                                                                                                                                                                                                          |
| ---- | -------------------------------------------------------------------------------------------- | ------------------------------------------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| 12   | /`ws-calculator/waterCalculator/_estimate` and `/sw-calculator/sewerageCalculator/_estimate` | <p><code>1966,</code></p><p><code>1967</code></p> | <p><code>WS_CEMP</code>,<code>WS_DOC_VERIFIER</code>,<code>WS_FIELD_INSPECTOR</code>,<code>WS_APPROVER</code>,<code>WS_CLERK</code></p><p><code>SW_CEMP,SW_DOC_VERIFIER,SW_FIELD_INSPECTOR,SW_CLERK</code></p> |
| 1    | `/access/v1/actions/mdms/_get`                                                               | `870`                                             |                                                                                                                                                                                                                |
| 13   | `/egov-hrms/employees/_search`                                                               | `1752`                                            |                                                                                                                                                                                                                |
| 4    | `/egov-workflow-v2/egov-wf/businessservice/_search`                                          | `1743`                                            | `EMPLOYEE`                                                                                                                                                                                                     |
| 9    | `/filestore/v1/files/url`                                                                    | `1528`                                            | `EMPLOYEE`                                                                                                                                                                                                     |
| 3    | `/localization/messages/v1/_search`                                                          | `1531`                                            |                                                                                                                                                                                                                |
| 7    | `/property-services/property/_search`                                                        | `1897`                                            | `PT_CEMP`,`PT_DOC_VERIFIER`,`PT_FIELD_INSPECTOR`,`PT_APPROVER`                                                                                                                                                 |
| 6    | `/sw-services/swc/_search`                                                                   | `1940`                                            | `SW_CEMP`,`SW_DOC_VERIFIER`,`SW_FIELD_INSPECTOR`,`SW_CLERK`                                                                                                                                                    |
| 11   | `/sw-services/swc/_update`                                                                   | `1939`                                            | `SW_CEMP`,`SW_DOC_VERIFIER`,`SW_FIELD_INSPECTOR`,`SW_CLERK`                                                                                                                                                    |
| 2    | `/user/_search`                                                                              | `604`                                             |                                                                                                                                                                                                                |
| 5    | `/ws-services/wc/_search`                                                                    | `1900`                                            | `WS_CEMP`,`WS_DOC_VERIFIER`,`WS_FIELD_INSPECTOR`,`WS_APPROVER`,`WS_CLERK`                                                                                                                                      |
| 10   | `/ws-services/wc/_update`                                                                    | `1901`                                            | `WS_CEMP`,`WS_DOC_VERIFIER`,`WS_FIELD_INSPECTOR`,`WS_APPROVER`,`WS_CLERK`                                                                                                                                      |

&#x20;**Employee Roles and Credentials:** The login credentials and details are available in the document here:[<img src="https://developers.google.com/drive/images/drive_icon.png" alt="" data-size="line">DIGIT Login Credentials](https://docs.google.com/spreadsheets/d/15p6dmlVUXvopvzyyG06ty2rxtffSMQxN5F2l2FSWoFA/edit#gid=0)
