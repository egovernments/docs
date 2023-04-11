# Employee Download Bill

**Objective:** Provide employees with the capability to download bills.

## Workflow Details

On the employee home screen, the Bill Genie module card contains the links related to Bill Genie screens.

<figure><img src="../../../../../.gitbook/assets/image (307).png" alt=""><figcaption></figcaption></figure>

### **Download Bills Screen** <a href="#download-bills-screen" id="download-bills-screen"></a>

<figure><img src="../../../../../.gitbook/assets/image (288).png" alt=""><figcaption></figcaption></figure>

The process of downloading each bill and consolidating them in a single pdf happens at the backend(pdf-service).

A snapshot of the details returned by the API is given below:

<figure><img src="../../../../../.gitbook/assets/image (514).png" alt=""><figcaption></figcaption></figure>

According to these details, the Status and corresponding Action details are shown in the results table.

Statuses and their Actions available are:

* Initiated → NA
* Expired → Retry
* Failed → Retry
* InProgress → Cancel
* Done → Download

When the status is done, that means totalrecords are equal to the recordscompleted. In this case, a filestore id is returned using which we can fetch the resulting pdf.

When the status is complete and 24hrs have passed then the status shows expired and the action is retry. In this case, the results are fetched again according to the requested criteria.

&#x20;A snapshot of resulting pdf is shown below:

<figure><img src="../../../../../.gitbook/assets/image (523).png" alt=""><figcaption></figcaption></figure>

## **Technical Implementation Details** <a href="#technical-implementation-details" id="technical-implementation-details"></a>

Download bills implementation can be found in this file:

{% embed url="https://github.com/egovernments/DIGIT-Dev/blob/00460c5492778678e06e09c74f494154e771baa4/frontend/micro-ui/web/micro-ui-internals/packages/modules/bills/src/pages/employee/DownloadBill/index.js" %}

### **Hook(s) Used**

```
const { data, isLoading, isError, error } = Digit.Hooks.useBulkPdfDetails({ filters: filters });
```

Technical Implementation file:

{% embed url="https://github.com/egovernments/DIGIT-Dev/blob/b24905db78ba453cfdb606cf8069cde0e5025de6/frontend/micro-ui/web/micro-ui-internals/packages/libraries/src/hooks/payment.js" %}

### **API Curl(s)** <a href="#api-curl-s" id="api-curl-s"></a>

For fetching the bulk bill download details:

```
curl 'https://qa.digit.org/pdf-service/v1/_getBulkPdfRecordsDetails?offset=0&limit=100&_=1657597779312' \
  -H 'authority: qa.digit.org' \
  -H 'accept: application/json, text/plain, */*' \
  -H 'accept-language: en-US,en;q=0.9' \
  -H 'content-type: application/json;charset=UTF-8' \
  -H 'origin: https://qa.digit.org' \
  -H 'referer: https://qa.digit.org/digit-ui/employee/bills/download-bill-pdf' \
  -H 'sec-ch-ua: ".Not/A)Brand";v="99", "Google Chrome";v="103", "Chromium";v="103"' \
  -H 'sec-ch-ua-mobile: ?0' \
  -H 'sec-ch-ua-platform: "Windows"' \
  -H 'sec-fetch-dest: empty' \
  -H 'sec-fetch-mode: cors' \
  -H 'sec-fetch-site: same-origin' \
  -H 'user-agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/103.0.0.0 Safari/537.36' \
  --data-raw '{"RequestInfo":{"apiId":"Rainmaker","authToken":"5f17dab3-d735-4ee2-9284-378a6b3009a9","userInfo":{"id":40977,"uuid":"3e713a84-826a-4e43-82f6-b693123c9a9a","userName":"QABG","name":"Emplyoee bill genie ","mobileNumber":"7754321234","emailId":"sirisha.deshpande@moolya.com","locale":null,"type":"EMPLOYEE","roles":[{"name":"PT Counter Employee","code":"PT_CEMP","tenantId":"pb.amritsar"},{"name":"WS Counter Employee","code":"WS_CEMP","tenantId":"pb.amritsar"},{"name":"SW Counter Employee","code":"SW_CEMP","tenantId":"pb.amritsar"},{"name":"Super User","code":"SUPERUSER","tenantId":"pb.amritsar"},{"name":"Employee","code":"EMPLOYEE","tenantId":"pb.amritsar"},{"name":"Universal Collection Employee","code":"UC_EMP","tenantId":"pb.amritsar"}],"active":true,"tenantId":"pb.amritsar","permanentCity":null},"msgId":"1657597779312|en_IN","plainAccessRequest":{}}}' \
  --compressed
```

For fetching the file with the filestoreId:

```
curl 'https://qa.digit.org/filestore/v1/files/url?tenantId=pb.amritsar&fileStoreIds=03b45f4b-5dab-4c80-8846-351ad9d86402' \
  -H 'authority: qa.digit.org' \
  -H 'accept: application/json, text/plain, */*' \
  -H 'accept-language: en-US,en;q=0.9' \
  -H 'referer: https://qa.digit.org/digit-ui/employee/bills/download-bill-pdf' \
  -H 'sec-ch-ua: ".Not/A)Brand";v="99", "Google Chrome";v="103", "Chromium";v="103"' \
  -H 'sec-ch-ua-mobile: ?0' \
  -H 'sec-ch-ua-platform: "Windows"' \
  -H 'sec-fetch-dest: empty' \
  -H 'sec-fetch-mode: cors' \
  -H 'sec-fetch-site: same-origin' \
  -H 'user-agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/103.0.0.0 Safari/537.36' \
  --compressed
```

For starting the download process again(For retry action)

```
curl 'https://qa.digit.org/egov-pdf/download/WNS/wnsgroupbill?tenantId=pb.amritsar&locality=SUN08&isConsolidated=true&bussinessService=WS&_=1657597872651' \
  -H 'authority: qa.digit.org' \
  -H 'accept: application/json, text/plain, */*' \
  -H 'accept-language: en-US,en;q=0.9' \
  -H 'content-type: application/json;charset=UTF-8' \
  -H 'origin: https://qa.digit.org' \
  -H 'referer: https://qa.digit.org/digit-ui/employee/bills/download-bill-pdf' \
  -H 'sec-ch-ua: ".Not/A)Brand";v="99", "Google Chrome";v="103", "Chromium";v="103"' \
  -H 'sec-ch-ua-mobile: ?0' \
  -H 'sec-ch-ua-platform: "Windows"' \
  -H 'sec-fetch-dest: empty' \
  -H 'sec-fetch-mode: cors' \
  -H 'sec-fetch-site: same-origin' \
  -H 'user-agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/103.0.0.0 Safari/537.36' \
  --data-raw '{"RequestInfo":{"apiId":"Rainmaker","authToken":"5f17dab3-d735-4ee2-9284-378a6b3009a9","userInfo":{"id":40977,"uuid":"3e713a84-826a-4e43-82f6-b693123c9a9a","userName":"QABG","name":"Emplyoee bill genie ","mobileNumber":"7754321234","emailId":"sirisha.deshpande@moolya.com","locale":null,"type":"EMPLOYEE","roles":[{"name":"PT Counter Employee","code":"PT_CEMP","tenantId":"pb.amritsar"},{"name":"WS Counter Employee","code":"WS_CEMP","tenantId":"pb.amritsar"},{"name":"SW Counter Employee","code":"SW_CEMP","tenantId":"pb.amritsar"},{"name":"Super User","code":"SUPERUSER","tenantId":"pb.amritsar"},{"name":"Employee","code":"EMPLOYEE","tenantId":"pb.amritsar"},{"name":"Universal Collection Employee","code":"UC_EMP","tenantId":"pb.amritsar"}],"active":true,"tenantId":"pb.amritsar","permanentCity":null},"msgId":"1657597872650|en_IN","plainAccessRequest":{}}}' \
  --compressed
```

### **API(s) Used**

| **API Endpoint**                            | **API description**                               | **Access Roles**                                              |
| ------------------------------------------- | ------------------------------------------------- | ------------------------------------------------------------- |
| `/pdf-service/v1/_getBulkPdfRecordsDetails` | → Bulk Bill download details                      | `EMPLOYEE`, CEMP roles ex : `PT_CEMP`,`WS_CEMP`,`SW_CEMP` etc |
| `/filestore/v1/files/url`                   | → To Download pdf given filestoreId               | `EMPLOYEE`, CEMP roles ex : `PT_CEMP`,`WS_CEMP`,`SW_CEMP` etc |
| `/egov-pdf/download/WNS/wnsgroupbill`       | → For Retry Action(Results will be fetched again) | `EMPLOYEE`, CEMP roles ex : `PT_CEMP`,`WS_CEMP`,`SW_CEMP` etc |

\
\
