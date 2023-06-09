# mCollect UI Flow

## Overview

Provide employees with the option to search challans, download receipts, check the current status, cancel challans, update challans and collect payment.

## Workflow Details

Once the user login with **UC\_EMP** Role, then the User will get the mCollect module card with the Total Challan Count.

<div align="left">

<img src="../../../../../.gitbook/assets/image (209) (1).png" alt="">

</div>

The clicking of Search Challan navigates to the Inbox/search challan screen.

Route - [mSeva](https://qa.digit.org/digit-ui/employee/mcollect/inbox)

![](<../../../../../.gitbook/assets/image (164) (1).png>)

Inbox File link -&#x20;

[<img src="https://github.com/fluidicon.png" alt="" data-size="line">digit-ui-internals/Inbox.js at main · egovernments/digit-ui-internals](https://github.com/egovernments/digit-ui-internals/blob/main/packages/modules/mCollect/src/pages/employee/Inbox.js)

### **Collect**

Clicking on the Collect button routes users to the common-pay screen with the URL.

example: “https://qa.digit.org/digit-ui/employee/payment/collect/{`selectedbusinessService`}/{`selectedChallanNumber`}/tenantId={`tenantId`}?workflow=mcollect”

This screen is common for all modules.

### **Download Receipt**

On Click on download receipt, able to download the receipt of the respective challan number using pdf service API `egov-pdf/download/PAYMENT/consolidatedreceipt`.

### **Cancel/Update Challan**

On search results we can click on the challan number to update/cancel any challan, it is explained in the following documentation - [Update / Cancel Challan](update-cancel-challan-ui-flow.md)

## Technical Implementation Details

MDMS Configs used in this inbox screen - `applicationStatus` to show all required statuses in the inbox, similarly `uiCommonPay` to get service categories.

**Table Structure**

* Uses the same table component similar to other modules.

#### Data fetch <a href="#data-fetch" id="data-fetch"></a>

* Once the data is fetched using `echallan-services/eChallan/v1/_search` API is being used to search and get data, after that using consumer codes, need to call fetch Bill API `billing-service/bill/v2/_fetchbill` to get bills for respective challan for showing status, amount and date etc.
* The count API`echallan-services/eChallan/v1/_count` to get the count of total challans.

## **Localisation Module**

`rainmaker-uc`

## **API Used**

1. `egov-mdms-service/v1/_search`
2. `echallan-services/eChallan/v1/_create`
3. `egov-pdf/download/UC/mcollect-challan`
4. `echallan-services/eChallan/v1/_count`

## **Role Action Mapping**

| API                                     | Roles    | Action ID |
| --------------------------------------- | -------- | --------- |
| `egov-mdms-service/v1/_search`          |          | `954`     |
| `echallan-services/eChallan/v1/_create` | `UC_EMP` | `2112`    |
| `egov-pdf/download/UC/mcollect-challan` | `UC_EMP` | `2115`    |
| `echallan-services/eChallan/v1/_count`  | `UC_EMP` | `2192`    |

## **Related Links**

| Related Title                  | Documentation                                                                                  |
| ------------------------------ | ---------------------------------------------------------------------------------------------- |
| MCollect Create Challan        | [Challan Creation](https://digit-discuss.atlassian.net/wiki/spaces/DD/pages/1845297183)        |
| MCollect Edit / Update Challan | [Update / Cancel Challan](https://digit-discuss.atlassian.net/wiki/spaces/DD/pages/1669955631) |
