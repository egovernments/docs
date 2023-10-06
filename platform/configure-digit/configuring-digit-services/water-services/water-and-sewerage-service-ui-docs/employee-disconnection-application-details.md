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

<div align="left">

<figure><img src="../../../../../.gitbook/assets/image (381).png" alt=""><figcaption></figcaption></figure>

</div>

#### Application Timeline

<div align="left">

<figure><img src="../../../../../.gitbook/assets/image (572).png" alt=""><figcaption></figcaption></figure>

</div>

#### Downloads <a href="#downloads" id="downloads"></a>

Application Form

<figure><img src="../../../../../.gitbook/assets/image (571).png" alt=""><figcaption></figcaption></figure>

**Disconnection Notice**

<figure><img src="../../../../../.gitbook/assets/image (385).png" alt=""><figcaption></figcaption></figure>

**Water & Sewerage Disconnection Workflow Table**

<table data-header-hidden><thead><tr><th width="104"></th><th></th><th></th><th></th><th></th></tr></thead><tbody><tr><td><strong>#</strong></td><td><strong>Action</strong></td><td><strong>Role</strong></td><td><strong>From State</strong></td><td><strong>To State</strong></td></tr><tr><td>1</td><td>Initiate Application</td><td>Citizen/ Counter Employee</td><td> </td><td>Initiated</td></tr><tr><td>2</td><td>Submit Application</td><td>Citizen/ Counter Employee</td><td>Initiated</td><td>Pending for document verification</td></tr><tr><td>3</td><td>Verify and Forward</td><td>Document Verifier</td><td>Pending for document verification</td><td>Pending for field inspection</td></tr><tr><td>4</td><td>Verify and Forward</td><td>Field Inspector</td><td>Pending for field inspection</td><td>Pending approval for disconnection</td></tr><tr><td>5</td><td>Send Back</td><td>Document Verifier</td><td>Pending for document verification</td><td>Pending for counter employee action</td></tr><tr><td>6</td><td>Send Back</td><td>Field Inspector</td><td>Pending for Field inspection</td><td>Pending for document verification</td></tr><tr><td>7</td><td>Send Back</td><td>Approver</td><td>Pending approval for disconnection</td><td>Pending for field inspection</td></tr><tr><td>8</td><td>Send Back To Citizen</td><td><strong>&#x3C;roles having access></strong></td><td><strong>&#x3C;Current Status></strong></td><td>Pending for citizen action</td></tr><tr><td>9</td><td>Re-submit</td><td>Citizen/ Counter Employee</td><td><p>Pending for citizen action</p><p>OR</p><p>Pending for counter employee action</p></td><td>&#x3C;<strong>To the status application was sent back to citizen></strong></td></tr><tr><td>12</td><td>Approve</td><td>Approver</td><td>Pending approval for disconnection</td><td>Pending for payment</td></tr><tr><td>13</td><td>Reject</td><td><strong>&#x3C;roles having access></strong></td><td><strong>&#x3C;Current Status></strong></td><td>Rejected</td></tr><tr><td>14</td><td>Payment/ Collection</td><td>Citizen/ Counter Employee</td><td>Pending for payment</td><td>Pending for disconnection execution</td></tr><tr><td>15</td><td>Execute Disconnection</td><td>Clerk</td><td>Pending for disconnection execution</td><td><p>Disconnection Executed</p><p> </p></td></tr></tbody></table>

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

<table><thead><tr><th width="88">S.No.</th><th>API</th><th>Action ID</th><th>Roles</th></tr></thead><tbody><tr><td>1</td><td><code>/access/v1/actions/mdms/_get</code></td><td><code>870</code></td><td> </td></tr><tr><td>2</td><td><code>/user/_search</code></td><td><code>604</code></td><td> </td></tr><tr><td>3</td><td><code>/localization/messages/v1/_search</code></td><td><code>1531</code></td><td> </td></tr><tr><td>4</td><td><code>/egov-workflow-v2/egov-wf/businessservice/_search</code></td><td><code>1743</code></td><td><code>EMPLOYEE</code></td></tr><tr><td>5</td><td><code>/ws-services/wc/_search</code></td><td><code>1900</code></td><td><code>WS_CEMP</code>,<code>WS_DOC_VERIFIER</code>,<code>WS_FIELD_INSPECTOR</code>,<code>WS_APPROVER</code>,<code>WS_CLERK</code></td></tr><tr><td>6</td><td><code>/sw-services/swc/_search</code></td><td><code>1940</code></td><td><code>SW_CEMP</code>,<code>SW_DOC_VERIFIER</code>,<code>SW_FIELD_INSPECTOR</code>,<code>SW_CLERK</code></td></tr><tr><td>7</td><td><code>/property-services/property/_search</code></td><td><code>1897</code></td><td><code>PT_CEMP</code>,<code>PT_DOC_VERIFIER</code>,<code>PT_FIELD_INSPECTOR</code>,<code>PT_APPROVER</code></td></tr><tr><td>8</td><td><code>/ws-services/wc/_create</code></td><td><code>1899</code></td><td><code>WS_CEMP</code></td></tr><tr><td>9</td><td><code>/filestore/v1/files/url</code></td><td><code>1528</code></td><td><code>EMPLOYEE</code></td></tr><tr><td>10</td><td><code>/ws-services/wc/_update</code></td><td><code>1901</code></td><td><code>WS_CEMP</code>,<code>WS_DOC_VERIFIER</code>,<code>WS_FIELD_INSPECTOR</code>,<code>WS_APPROVER</code>,<code>WS_CLERK</code></td></tr><tr><td>11</td><td><code>/sw-services/swc/_update</code></td><td><code>1939</code></td><td><code>SW_CEMP</code>,<code>SW_DOC_VERIFIER</code>,<code>SW_FIELD_INSPECTOR</code>,<code>SW_CLERK</code></td></tr><tr><td>12</td><td>/<code>ws-calculator/waterCalculator/_estimate</code> and <code>/sw-calculator/sewerageCalculator/_estimate</code></td><td><p><code>1966,</code></p><p><code>1967</code></p></td><td><p><code>WS_CEMP</code>,<code>WS_DOC_VERIFIER</code>,<code>WS_FIELD_INSPECTOR</code>,<code>WS_APPROVER</code>,<code>WS_CLERK</code></p><p><code>SW_CEMP,SW_DOC_VERIFIER,SW_FIELD_INSPECTOR,SW_CLERK</code></p></td></tr><tr><td>13</td><td><code>/egov-hrms/employees/_search</code></td><td><code>1752</code></td><td> </td></tr></tbody></table>

Find the login credentials and details in the document here: [<img src="https://developers.google.com/drive/images/drive_icon.png" alt="" data-size="line">DIGIT Login Credentials](https://docs.google.com/spreadsheets/d/15p6dmlVUXvopvzyyG06ty2rxtffSMQxN5F2l2FSWoFA/edit#gid=0)
