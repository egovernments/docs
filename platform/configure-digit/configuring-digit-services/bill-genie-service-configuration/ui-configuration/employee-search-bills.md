# Employee Search Bills

**Objective:** Provide employees with the capability to search bills using filters.

## Workflow Details

On the employee home screen, the Bill Genie module card contains the links related to Bill Genie screens.

<figure><img src="../../../../../.gitbook/assets/image (482).png" alt=""><figcaption></figcaption></figure>

#### **Search Bill Screen** <a href="#search-bill-screen" id="search-bill-screen"></a>

<figure><img src="../../../../../.gitbook/assets/image (72).png" alt=""><figcaption></figcaption></figure>

#### Parameters required to search a bill <a href="#parameters-required-for-searching-a-bill" id="parameters-required-for-searching-a-bill"></a>

1. Service Category → It is a mandatory parameter
2. Bill No → Every bill in the system has a unique Bill No.
3. Consumer ID/Property ID → It is a dynamic ID which is dependent on the selection of Service Category.
   * If the selected service category is either Water or Sewerage then Consumer ID is used
   * In all the other services Property ID is used

4\. Mobile No.

#### **Search Results** <a href="#search-results" id="search-results"></a>

<figure><img src="../../../../../.gitbook/assets/image (504).png" alt=""><figcaption></figcaption></figure>

* Search Results are shown in a Tabular format with the columns as displayed above.
* Any Bill can have these 3 statuses and a unique action corresponding to that status
  * EXPIRED → Bill Genie User can generate a new bill if the existing bill is expired
  * Cancelled → Bill Genie User can generate a new bill if the existing bill is cancelled
  * PAID → Bill Genie users can download the receipt as a pdf if the bill is paid
* When the user clicks on a bill number cell that bill is downloaded as a pdf

## **Technical Implementation Details** <a href="#technical-implementation-details" id="technical-implementation-details"></a>

The search bill page’s technical implementation is available here:

{% embed url="https://github.com/egovernments/DIGIT-Dev/blob/0f62318dd3183fbce13b66af7012ddae027376f9/frontend/micro-ui/web/micro-ui-internals/packages/modules/bills/src/pages/employee/SearchApp.js" %}

Implementation details of Search Input parameters and error validation and handling details are available here:

{% embed url="https://github.com/egovernments/DIGIT-Dev/blob/0f62318dd3183fbce13b66af7012ddae027376f9/frontend/micro-ui/web/micro-ui-internals/packages/modules/bills/src/components/Search/SearchFields.js" %}

Implementation details of the results table is available here:

{% embed url="https://github.com/egovernments/DIGIT-Dev/blob/0f62318dd3183fbce13b66af7012ddae027376f9/frontend/micro-ui/web/micro-ui-internals/packages/modules/bills/src/components/Search/index.js" %}

### **Hooks/Utils Used**

To Download a bill → A util function named downloadBill is used which is defined in this file

{% embed url="https://github.com/egovernments/DIGIT-Dev/blob/db572b868bad5af8564452606be4690c25041419/frontend/micro-ui/web/micro-ui-internals/packages/libraries/src/utils/pdf.js" %}

This util function is inside Digit Utils hence it can be called anywhere throughout the application like this `Digit.Utils.downloadBill(consumerCode, businessService, "consolidatedreceipt")`

To Search a bill → A hook named useBillSearch is used to search bills which is defined in this file

{% embed url="https://github.com/egovernments/DIGIT-Dev/blob/b24905db78ba453cfdb606cf8069cde0e5025de6/frontend/micro-ui/web/micro-ui-internals/packages/libraries/src/hooks/bills/useBillSearch.js" %}

To fetch the data for the service category dropdown → A hook named useCommonMDMS is used to fetch this data. This hook is called with the following parameters:

`Digit.Hooks.useCommonMDMS(tenantId, "BillingService", "BillsGenieKey");`

Technical implementation of this hook is available here:

{% embed url="https://github.com/egovernments/DIGIT-Dev/blob/111d6269f3c7210cf829dea11dfe5062378b54f8/frontend/micro-ui/web/micro-ui-internals/packages/libraries/src/hooks/useMDMS.js" %}

### **API Curls** <a href="#api-curls" id="api-curls"></a>

Search bill API

```
curl 'https://qa.digit.org/egov-searcher/bill-genie/billswithaddranduser/_get?_=1657020362243' \
  -H 'authority: qa.digit.org' \
  -H 'accept: application/json, text/plain, */*' \
  -H 'accept-language: en-US,en;q=0.9' \
  -H 'content-type: application/json;charset=UTF-8' \
  -H 'origin: https://qa.digit.org' \
  -H 'referer: https://qa.digit.org/digit-ui/employee/bills/inbox' \
  -H 'sec-ch-ua: ".Not/A)Brand";v="99", "Google Chrome";v="103", "Chromium";v="103"' \
  -H 'sec-ch-ua-mobile: ?0' \
  -H 'sec-ch-ua-platform: "Windows"' \
  -H 'sec-fetch-dest: empty' \
  -H 'sec-fetch-mode: cors' \
  -H 'sec-fetch-site: same-origin' \
  -H 'user-agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/103.0.0.0 Safari/537.36' \
  --data-raw '{"searchCriteria":{"tenantId":"pb.amritsar","mobileNumber":"7878787878","limit":10,"sortBy":"commencementDate","sortOrder":"DESC","url":"/bill-genie/billswithaddranduser/_get","businesService":"PT"},"RequestInfo":{"apiId":"Rainmaker","authToken":"73541f52-2fd8-4c66-8f71-8b1b7cd4fa82","msgId":"1657020362242|en_IN","plainAccessRequest":{}}}' \
  --compressed
```

Download Bill API

```
curl 'https://qa.digit.org/egov-pdf/download/BILL/consolidatedbill?bussinessService=PT&tenantId=pb.amritsar&consumerCode=PB-PT-2020-02-07-003594' \
  -H 'authority: qa.digit.org' \
  -H 'accept: application/pdf' \
  -H 'accept-language: en-US,en;q=0.9' \
  -H 'content-type: application/json' \
  -H 'origin: https://qa.digit.org' \
  -H 'referer: https://qa.digit.org/digit-ui/employee/bills/inbox' \
  -H 'sec-ch-ua: ".Not/A)Brand";v="99", "Google Chrome";v="103", "Chromium";v="103"' \
  -H 'sec-ch-ua-mobile: ?0' \
  -H 'sec-ch-ua-platform: "Windows"' \
  -H 'sec-fetch-dest: empty' \
  -H 'sec-fetch-mode: cors' \
  -H 'sec-fetch-site: same-origin' \
  -H 'user-agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/103.0.0.0 Safari/537.36' \
  --data-raw '{"RequestInfo":{"apiId":"Rainmaker","authToken":"73541f52-2fd8-4c66-8f71-8b1b7cd4fa82","userInfo":{"id":12579,"uuid":"746412f0-93cc-4da2-8aff-33301aad92fc","userName":"JA","name":"Jagan","mobileNumber":"9092251026","emailId":"Dummy@dummy.com","locale":null,"type":"EMPLOYEE","roles":[{"name":"LOA Creator","code":"LOA_CREATOR","tenantId":"pb.amritsar"},{"name":"Grievance Routing Officer","code":"GRO","tenantId":"pb.amritsar"},{"name":"NoC counter employee","code":"NOC_CEMP","tenantId":"pb.amritsar"},{"name":"BPA Builder","code":"BPA_BUILDER","tenantId":"pb.amritsar"},{"name":"Finance Report View","code":"EGF_REPORT_VIEW","tenantId":"pb.amritsar"},{"name":"AssetReportViewer","code":"AssetReportViewer","tenantId":"pb.amritsar"},{"name":"BPA Field Inspector","code":"BPA_FIELD_INSPECTOR","tenantId":"pb.amritsar"},{"name":"TL Field Inspector","code":"TL_FIELD_INSPECTOR","tenantId":"pb.amritsar"},{"name":"EGF Bill Creator","code":"EGF_BILL_CREATOR","tenantId":"pb.amritsar"},{"name":"PT Counter Employee","code":"PT_CEMP","tenantId":"pb.amritsar"},{"name":"BPA Services Approver","code":"BPA_APPROVER","tenantId":"pb.amritsar"},{"name":"Fire Noc Department Approver","code":"FIRE_NOC_APPROVER","tenantId":"pb.amritsar"},{"name":"Counter Employee","code":"CEMP","tenantId":"pb.amritsar"},{"name":"Admin of a ULB","code":"CITY_ADMIN","tenantId":"pb.amritsar"},{"name":"PT Field Inspector","code":"PT_FIELD_INSPECTOR","tenantId":"pb.amritsar"},{"name":"WS Counter Employee","code":"WS_CEMP","tenantId":"pb.amritsar"},{"name":"FSM Driver","code":"FSM_DRIVER","tenantId":"pb.amritsar"},{"name":"Any User","code":"ANONYMUS","tenantId":"pb.amritsar"},{"name":"WS Field Inspector","code":"WS_FIELD_INSPECTOR","tenantId":"pb.amritsar"},{"name":"Works Administrator","code":"WORKS_ADMINISTRATOR","tenantId":"pb.amritsar"},{"name":"ULB Administrator","code":"PTADMIN","tenantId":"pb.amritsar"},{"name":"Property Tax Receipt Cancellator","code":"CR_PT","tenantId":"pb.amritsar"},{"name":"PT Doc Verifier","code":"PT_DOC_VERIFIER","tenantId":"pb.amritsar"},{"name":"FSM Administrator","code":"FSM_ADMIN","tenantId":"pb.amritsar"},{"name":"Employee","code":"EMPLOYEE","tenantId":"pb.amritsar"},{"name":"BPAREG Employee","code":"BPAREG_EMPLOYEE","tenantId":"pb.amritsar"},{"name":"TL Counter Employee","code":"TL_CEMP","tenantId":"pb.amritsar"},{"name":"Commissioner","code":"COMMISSIONER","tenantId":"pb.amritsar"},{"name":"TL Creator","code":"TL_CREATOR","tenantId":"pb.amritsar"},{"name":"EGF Bill Approver","code":"EGF_BILL_APPROVER","tenantId":"pb.amritsar"},{"name":"BPAREG doc verifier","code":"BPAREG_DOC_VERIFIER","tenantId":"pb.amritsar"},{"name":"BPA Structural Engineer","code":"BPA_STRUCTURALENGINEER","tenantId":"pb.amritsar"},{"name":"Redressal Officer","code":"RO","tenantId":"pb.amritsar"},{"name":"Collection Report Viewer","code":"COLL_REP_VIEW","tenantId":"pb.amritsar"},{"name":"BPA Engineer","code":"BPA_ENGINEER","tenantId":"pb.amritsar"},{"name":"Universal Collection Employee","code":"UC_EMP","tenantId":"pb.amritsar"},{"name":"FSM FSTP Opperator","code":"FSM_EMP_FSTPO","tenantId":"pb.amritsar"},{"name":"BPA Services verifier","code":"BPA_VERIFIER","tenantId":"pb.amritsar"},{"name":"State Administrator","code":"STADMIN","tenantId":"pb.amritsar"},{"name":"PT Counter Approver","code":"PT_APPROVER","tenantId":"pb.amritsar"},{"name":"NoC Field Inpector","code":"NOC_FIELD_INSPECTOR","tenantId":"pb.amritsar"},{"name":"Grievance Officer","code":"GO","tenantId":"pb.amritsar"},{"name":"FSM Employee Application Creator","code":"FSM_CREATOR_EMP","tenantId":"pb.amritsar"},{"name":"WS Clerk","code":"WS_CLERK","tenantId":"pb.amritsar"},{"name":"NoC Doc Verifier","code":"NOC_DOC_VERIFIER","tenantId":"pb.amritsar"},{"name":"Auto Escalation Employee","code":"AUTO_ESCALATE","tenantId":"pb.amritsar"},{"name":"WS Document Verifier","code":"WS_DOC_VERIFIER","tenantId":"pb.amritsar"},{"name":"FSM Employee Report Viewer","code":"FSM_REPORT_VIEWER","tenantId":"pb.amritsar"},{"name":"AssetCreator","code":"AssetCreator","tenantId":"pb.amritsar"},{"name":"BPA Architect","code":"BPA_ARCHITECT","tenantId":"pb.amritsar"},{"name":"TL Approver","code":"TL_APPROVER","tenantId":"pb.amritsar"},{"name":"PGR Administrator","code":"PGR-ADMIN","tenantId":"pb.amritsar"},{"name":"BPA Town Planner","code":"BPA_TOWNPLANNER","tenantId":"pb.amritsar"},{"name":"Field Employee","code":"FEMP","tenantId":"pb.amritsar"},{"name":"PTIS Admin","code":"PTIS_ADMIN","tenantId":"pb.amritsar"},{"name":"BPA Supervisor","code":"BPA_SUPERVISOR","tenantId":"pb.amritsar"},{"name":"FSM Payment Collector","code":"FSM_COLLECTOR","tenantId":"pb.amritsar"},{"name":"BPAREG Approver","code":"BPAREG_APPROVER","tenantId":"pb.amritsar"},{"name":"FSM Employee Application Editor","code":"FSM_EDITOR_EMP","tenantId":"pb.amritsar"},{"name":"TL doc verifier","code":"TL_DOC_VERIFIER","tenantId":"pb.amritsar"},{"name":"FSM Employee Application Viewer","code":"FSM_VIEW_EMP","tenantId":"pb.amritsar"},{"name":"PTIS Master","code":"PTIS_MASTER","tenantId":"pb.amritsar"},{"name":"FSM Desluding Operator","code":"FSM_DSO","tenantId":"pb.amritsar"},{"name":"TL Admin","code":"TL_ADMIN","tenantId":"pb.amritsar"},{"name":"SW Field Inspector","code":"SW_FIELD_INSPECTOR","tenantId":"pb.amritsar"},{"name":"NoC counter Approver","code":"NOC_APPROVER","tenantId":"pb.amritsar"},{"name":"HRMS Admin","code":"HRMS_ADMIN","tenantId":"pb.amritsar"},{"name":"WS Approver","code":"WS_APPROVER","tenantId":"pb.amritsar"},{"name":"Super User","code":"SUPERUSER","tenantId":"pb.amritsar"},{"name":"BPA NOC Verifier","code":"BPA_NOC_VERIFIER","tenantId":"pb.amritsar"},{"name":"FSM Employee Dashboard Viewer","code":"FSM_DASHBOARD_VIEWER","tenantId":"pb.amritsar"},{"name":"System user","code":"SYSTEM","tenantId":"pb.amritsar"},{"name":"SW Approver","code":"SW_APPROVER","tenantId":"pb.amritsar"},{"name":"Grivance Administrator","code":"GA","tenantId":"pb.amritsar"}],"active":true,"tenantId":"pb.amritsar","permanentCity":null},"msgId":"1657020371949|en_IN","plainAccessRequest":{}}}' \
  --compressed
```

### **APIs Used**

| **API Endpoint**                                     | **API description**                                                                       | **Employee Roles**                                            |
| ---------------------------------------------------- | ----------------------------------------------------------------------------------------- | ------------------------------------------------------------- |
| `egov-searcher/bill-genie/billswithaddranduser/_get` | <p>→ To search bills</p><p>→ Returns a list of bills according to the search criteria</p> | `EMPLOYEE`, CEMP roles ex : `PT_CEMP`,`WS_CEMP`,`SW_CEMP` etc |
| `/egov-pdf/download/BILL/consolidatedbill`           | <p>→ To download bills according to the search criteria</p><p>→ Returns a pdf file</p>    | `EMPLOYEE`, CEMP roles ex : `PT_CEMP`,`WS_CEMP`,`SW_CEMP` etc |

## &#x20;**Localization Details**

Localization keys are added under the `rainmaker-abg` locale module. Below is an example of few locale labels.

```
 {
      "code": "ABG_ADVERTISEMENT_TAX_INFO",
      "message": "Advertisement Tax",
      "module": "rainmaker-abg",
      "locale": "en_IN"
    },
    {
      "code": "ABG_ADVERTISEMENT_TAX_LABEL",
      "message": "Advertisement Tax",
      "module": "rainmaker-abg",
      "locale": "en_IN"
    },
       
```

\
\
