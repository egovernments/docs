---
description: Water and Sewerage employee application UI technical implementation doc
---

# Employee: Application Details

**Objective:** Provide employees with purposeful workflow actions.&#x20;

The same screen is used for both Application Details and Modify Application Details workflows. The details are provided below for the applicable scenarios.

## Workflow Details

#### **Application Details**

Clicking on the application number from the inbox/search screen/connection search, routes to the application details screen.\
A search call is made before rendering the screen and details are populated based on the search response.

**Application Details Screen**

![](<../../../../../.gitbook/assets/image (451).png>)

**Refer to** [Employee: Ad-hoc Rebate/Penalty and View Breakup in application details](employee-ad-hoc-rebate-penalty-and-view-breakup.md)

#### **Timeline View**

![](<../../../../../.gitbook/assets/image (345).png>)

#### **Downloads** <a href="#downloads" id="downloads"></a>

<figure><img src="../../../../../.gitbook/assets/image (359).png" alt=""><figcaption></figcaption></figure>

#### Estimation Letter

Once the Pending for Field Inspection stage is complete (if the status is pending approval) an Estimation Letter is generated.

<figure><img src="../../../../../.gitbook/assets/image (421).png" alt=""><figcaption></figcaption></figure>

#### Sanction Letter & Download Receipt

Once the payment stage is complete (and the status is pending for connection activation), the Sanction letter and receipt are generated.

<figure><img src="../../../../../.gitbook/assets/image (445).png" alt=""><figcaption></figcaption></figure>

### **Water & Sewerage Workflow Table**

| **Role**                                     | **Action**           | **Next State**                                   | **Status**                        |
| -------------------------------------------- | -------------------- | ------------------------------------------------ | --------------------------------- |
| Citizen/ Counter Employee/WS\_CEMP/ SW\_CEMP | INITIATE             | INITIATED                                        | INITIATED                         |
| Citizen/Counter Employee/WS\_CEMP / SW\_CEMP | EDIT                 | EDIT/ DOCUMENTVERIFICATION                       | Pending for Document Verification |
| Citizen/Counter Employee/WS\_CEMP / SW\_CEMP | Send Back to Citizen | <p>Pending for Citizen Action</p><p><br><br></p> | Pending for Citizen Action        |
| WS\_DOC\_VERIFIER / SW\_DOC\_VERIFIER        | VERIFY \&FORWARD     | FIELDVERIFICATION                                | Pending for Field Verification    |
| WS\_FIELD\_INSPECTOR / SW\_FIELD\_INSPECTOR  | VERIFY \&FORWARD     | PENDINGAPPROVAL                                  | Pending for APproval              |
| WS\_APPROVER / SW\_APPROVER                  | APPROVE              | PENDINGPAYMENT                                   | Pending for Payment               |
| Citizen/Counter Employee/WS\_CEMP / SW\_CEMP | PAY                  | Approved                                         | <p>Approved</p><p> </p>           |
| WS\_APPROVER / SW\_APPROVER                  | REJECT               | Rejected                                         | Rejected                          |
| WS\_CLERK/SW\_CLERK                          | Activate Connection  | Connection activated                             | Connection activated              |

## **Technical Implementation Details**

**Application Details File Path:** [https://github.com/egovernments/DIGIT-Dev/blob/develop/frontend/micro-ui/web/micro-ui-internals/packages/modules/ws/src/pages/employee/ApplicationDetails.js](https://github.com/egovernments/DIGIT-Dev/blob/develop/frontend/micro-ui/web/micro-ui-internals/packages/modules/ws/src/pages/employee/ApplicationDetails.js)

**Hook details for application details search:**

```
let { isLoading, isError, data: applicationDetails, error } = Digit.Hooks.ws.useWSDetailsPage(t, tenantId, applicationNumber, serviceType);  let workflowDetails = Digit.Hooks.useWorkflowDetails(    {      tenantId: tenantId,      id: applicationNumber,      moduleCode: applicationDetails?.processInstancesDetails?.[0]?.businessService,    },    {      enabled: applicationDetails?.processInstancesDetails?.[0]?.businessService ? true : false,    }  );
const { data: reciept_data, isLoading: recieptDataLoading } = Digit.Hooks.useRecieptSearch(    {      tenantId: stateCode,      businessService:  serviceType == "WATER" ? "WS.ONE_TIME_FEE" : "SW.ONE_TIME_FEE",      consumerCodes: applicationDetails?.applicationData?.applicationNo    },    {      enabled: applicationDetails?.applicationData?.applicationType?.includes("NEW_")    }  );
const { data: oldData } = Digit.Hooks.ws.useOldValue({    tenantId,    filters: { connectionNumber: applicationDetails?.applicationData?.connectionNo, isConnectionSearch: true },    businessService: serviceType,  });
```

The timeline view is common for all modules. File path: [https://github.com/egovernments/DIGIT-Dev/blob/develop/frontend/micro-ui/web/micro-ui-internals/packages/modules/templates/ApplicationDetails/index.js](https://github.com/egovernments/DIGIT-Dev/blob/develop/frontend/micro-ui/web/micro-ui-internals/packages/modules/templates/ApplicationDetails/index.js)

#### Downloads Method Reference:

`const applicationDownloadObject = { order: 3, label: t("WS_APPLICATION"), onClick: handleDownloadPdf, };`&#x20;

File Path: [https://github.com/egovernments/DIGIT-Dev/blob/develop/frontend/micro-ui/web/micro-ui-internals/packages/modules/ws/src/pages/employee/ApplicationDetails.js](https://github.com/egovernments/DIGIT-Dev/blob/develop/frontend/micro-ui/web/micro-ui-internals/packages/modules/ws/src/pages/employee/ApplicationDetails.js)

#### Estimation Letter Method Reference:

`const wsEstimateDownloadObject = { order: 1, label: t("WS_ESTIMATION_NOTICE"), onClick: () => getFiles([applicationDetails?.applicationData?.additionalDetails?.estimationFileStoreId], stateCode), };`

File Path: [https://github.com/egovernments/DIGIT-Dev/blob/develop/frontend/micro-ui/web/micro-ui-internals/packages/modules/ws/src/pages/employee/ApplicationDetails.js](https://github.com/egovernments/DIGIT-Dev/blob/develop/frontend/micro-ui/web/micro-ui-internals/packages/modules/ws/src/pages/employee/ApplicationDetails.js)

**Sanction Fee Method Reference:**

`const sanctionDownloadObject = { order: 2, label: t("WS_SANCTION_LETTER"), onClick: () => getFiles([applicationDetails?.applicationData?.additionalDetails?.sanctionFileStoreId], stateCode), };`

**Receipt Method Reference:**

`const appFeeDownloadReceipt = { order: 4, label: t("DOWNLOAD_RECEIPT_HEADER"), onClick: () => getRecieptSearch(applicationDetails?.applicationData?.tenantId ? applicationDetails?.applicationData?.tenantId : Digit.ULBService.getCurrentTenantId(), reciept_data?.Payments?.[0], applicationDetails?.applicationData?.applicationNo, receiptKey ), };`&#x20;

File Path: [https://github.com/egovernments/DIGIT-Dev/blob/develop/frontend/micro-ui/web/micro-ui-internals/packages/modules/ws/src/pages/employee/ApplicationDetails.js](https://github.com/egovernments/DIGIT-Dev/blob/develop/frontend/micro-ui/web/micro-ui-internals/packages/modules/ws/src/pages/employee/ApplicationDetails.js)

## **Localisation Details**

Localisation keys are added in the ‘_rainmaker-ws_’ locale module.

## **API Call Role Action Mapping**

| API                                                                                          | Action ID                                         | Roles                                                                                                                                                                                                          |
| -------------------------------------------------------------------------------------------- | ------------------------------------------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `/access/v1/actions/mdms/_get`                                                               | `870`                                             |                                                                                                                                                                                                                |
| `/user/_search`                                                                              | `604`                                             |                                                                                                                                                                                                                |
| `/localization/messages/v1/_search`                                                          | `1531`                                            |                                                                                                                                                                                                                |
| `/egov-workflow-v2/egov-wf/businessservice/_search`                                          | `1743`                                            | `EMPLOYEE`                                                                                                                                                                                                     |
| `/ws-services/wc/_search`                                                                    | `1900`                                            | `WS_CEMP`,`WS_DOC_VERIFIER`,`WS_FIELD_INSPECTOR`,`WS_APPROVER`,`WS_CLERK`                                                                                                                                      |
| `/sw-services/swc/_search`                                                                   | `1940`                                            | `SW_CEMP`,`SW_DOC_VERIFIER`,`SW_FIELD_INSPECTOR`,`SW_CLERK`                                                                                                                                                    |
| `/property-services/property/_search`                                                        | `1897`                                            | `PT_CEMP`,`PT_DOC_VERIFIER`,`PT_FIELD_INSPECTOR`,`PT_APPROVER`                                                                                                                                                 |
| `/ws-services/wc/_create`                                                                    | `1899`                                            | `WS_CEMP`                                                                                                                                                                                                      |
| `/filestore/v1/files/url`                                                                    | `1528`                                            | `EMPLOYEE`                                                                                                                                                                                                     |
| `/ws-services/wc/_update`                                                                    | `1901`                                            | `WS_CEMP`,`WS_DOC_VERIFIER`,`WS_FIELD_INSPECTOR`,`WS_APPROVER`,`WS_CLERK`                                                                                                                                      |
| `/sw-services/swc/_update`                                                                   | `1939`                                            | `SW_CEMP`,`SW_DOC_VERIFIER`,`SW_FIELD_INSPECTOR`,`SW_CLERK`                                                                                                                                                    |
| /`ws-calculator/waterCalculator/_estimate` and `/sw-calculator/sewerageCalculator/_estimate` | <p><code>1966,</code></p><p><code>1967</code></p> | <p><code>WS_CEMP</code>,<code>WS_DOC_VERIFIER</code>,<code>WS_FIELD_INSPECTOR</code>,<code>WS_APPROVER</code>,<code>WS_CLERK</code></p><p><code>SW_CEMP,SW_DOC_VERIFIER,SW_FIELD_INSPECTOR,SW_CLERK</code></p> |
| `/egov-hrms/employees/_search`                                                               | `1752`                                            |                                                                                                                                                                                                                |

&#x20;**Employee Roles and Credentials -** The credentials and details are available in the document attached below:

[<img src="https://developers.google.com/drive/images/drive_icon.png" alt="" data-size="line">DIGIT Login Credentials](https://docs.google.com/spreadsheets/d/15p6dmlVUXvopvzyyG06ty2rxtffSMQxN5F2l2FSWoFA/edit#gid=0)

