# Property Tax - Quick Pay for Citizen

## Overview

The Quick Pay feature allows a citizen to quickly view or pay all his pending bills for Property Tax \(or any other supported business Service\) by clicking links directly from the Digit-UI home screen.

Digit UI Home screen



Clicking on the Property Tax link in the Quick Pay section, a user is logged in and redirected to the My Bills Screen. Else, the user has to log in using his mobile number and the OTP sent to the number. The user is redirected to the My Bills screen.

On My Bills screen user is displayed all his pending property Tax bills \(as cards\) for all properties, which are registered to user’s logged in mobile Number. He can click View Details button of the corresponding card to check the detailed bill summary which takes him to bill details page. There is also a link for case when the user is unable to find the property tax bills.

My Bills Screen :![](blob:https://digit-discuss.atlassian.net/1c51ed7f-78cb-4781-8637-a7691081146b#media-blob-url=true&id=449f95fd-2fb9-4fd8-afd1-2167a98dd3db&collection=contentId-1610154021&contextId=1610154021&mimeType=image%2Fpng&name=Screenshot%202021-05-17%20121222.png&size=41133&width=282&height=600)

On arriving on Bill Details screen user can see a list of various categories of taxes that are present. After checking user can select to pay full amount or custom amount, which can be not less than the ₹100, and not be more than the total tax, these restriction however can be changed through MDMS.

Bill Details Screen:![](blob:https://digit-discuss.atlassian.net/b7cc5923-9287-4e1e-ae03-c8dd55ba20a5#media-blob-url=true&id=b57eb580-0032-41f5-aef9-368a03d4cbab&collection=contentId-1610154021&contextId=1610154021&mimeType=image%2Fjpeg&name=Screenshot_2021-05-17-13-24-56-79.jpg&size=419380&width=1080&height=3990)

 After clicking Proceed To Pay button you get to the pay screen. Where the user is asked to select the payment gateway from a bunch of radio buttons, and then after clicking pay, the user is redirected to bank payment gateway.

Payment Screen:![](blob:https://digit-discuss.atlassian.net/5e5d37ad-9fec-4099-b1bf-255a48f4222f#media-blob-url=true&id=da5485eb-0d67-4100-93da-15a20ce5f533&collection=contentId-1610154021&contextId=1610154021&mimeType=image%2Fpng&name=Screenshot%202021-05-17%20142349.png&size=23874&width=224&height=527)

After making a successful payment through bank’s gateway the user is redirected to the response screen which shows the details of the payment and other bill details.

Response Screen \(Successful\):![](blob:https://digit-discuss.atlassian.net/2d3b93af-f5ba-4b8a-966a-065a3662e0c5#media-blob-url=true&id=3593c089-3272-4418-92b9-2ca521ae1b03&collection=contentId-1610154021&contextId=1610154021&mimeType=image%2Fpng&name=Screenshot%202021-05-17%20143056.png&size=135418&width=293&height=595)

in case payment fails for any reason the response screen shows the message, that payment failed.

Response Screen \(Failure\):![](blob:https://digit-discuss.atlassian.net/8205ea2c-3889-4d4a-bf0d-7008b14f6240#media-blob-url=true&id=c5009310-b8c9-45ae-9c6a-24817ea6bf58&collection=contentId-1610154021&contextId=1610154021&mimeType=image%2Fpng&name=Screenshot%202021-05-17%20220609.png&size=29443&width=284&height=612)

**Case When user wants to pay for Property for different mobile number:**

My Bills page only displays the properties with pending Taxes, which are associated with the mobile number which is logged in. But if user wants to search for any other property then he can click on the link below the My Bills screen which will take the user to the search screen.

Search Screen:![](blob:https://digit-discuss.atlassian.net/3a5dfbeb-54f3-4357-9d25-6ca8ae6a4d71#media-blob-url=true&id=a7e1fe2a-62f1-4795-90db-1a8b2db9e58b&collection=contentId-1610154021&contextId=1610154021&mimeType=image%2Fpng&name=Screenshot%202021-05-19%20094911.png&size=33639&width=284&height=608)

On Search screen user can search a property by mobile Number, a unique property ID, or an existing property ID. After mentioning the parameters the search performed will take user to the search results screen. Where user can see all the properties with the matching criteria, whether or not they have pending taxes.

Search Results Screen:![](blob:https://digit-discuss.atlassian.net/75306b8b-cd79-459b-8d4b-cd27b82c886b#media-blob-url=true&id=f8c4311d-5f98-4f16-a4dd-086ceaa2b436&collection=contentId-1610154021&contextId=1610154021&mimeType=image%2Fpng&name=Screenshot%202021-05-19%20095824.png&size=47701&width=282&height=608)

From Here on clicking view Details a user is redirected to the bill-details Screen, for the property, just as in case of My Bills Screen.

#### Technical Details  <a id="Technical-Details"></a>

**My Bills Screen** 

For My Bills screen the starting file is located at the link :-

[https://github.com/egovernments/digit-ui-internals/blob/development/packages/modules/common/src/payments/citizen/bills/index.js](https://github.com/egovernments/digit-ui-internals/blob/development/packages/modules/common/src/payments/citizen/bills/index.js)

on this page an MDMS call is made which is to fetches all the restrictions that are put on bill payment such as whether partial payment is allowed or not, advance payment allowed or not, minimum payable amount etc. for the particular business Service which is supplied into URL.

the MDMS criteria used here for fetching MDMS details is:

 `1{ 2 "MdmsCriteria": { 3 "tenantId": "pb", 4 "moduleDetails": [ 5 { 6 "moduleName": "BillingService", 7 "masterDetails": [ 8 { 9 "name": "BusinessService" 10 }, 11 { 12 "name": "TaxHeadMaster" 13 }, 14 { 15 "name": "TaxPeriod" 16 } 17 ] 18 } 19 ] 20 } 21 }`

Also the pending bills are fetched for the citizen for the specific business service using the custom hook, that fetches bill for logged in mobile number.![](blob:https://digit-discuss.atlassian.net/b5b9b396-2c40-4922-9c00-bdafda63adfb#media-blob-url=true&id=959433e4-85b6-4fec-a1cd-30aac7d1d645&collection=contentId-1610154021&contextId=1610154021&mimeType=image%2Fjpeg&name=Capture.JPG&size=71203&width=1117&height=508)

The bill is rendered using a keynoteConfig file which can be located using the following link:-

[https://github.com/egovernments/digit-ui-internals/blob/development/packages/modules/common/src/payments/citizen/keynotesConfig.js](https://github.com/egovernments/digit-ui-internals/blob/development/packages/modules/common/src/payments/citizen/keynotesConfig.js)

On this page for each business service there is a configuration stored to define what part of the bill is to be displayed.

the configuration returns an object of structure``1{ 2        "my-bill": [ 3          { 4            keyValue: "CS_COMMON_AMOUNT_DUE", 5            keyPath: [ 6              (d) => { 7                const overdueBy = new Date().getTime() - new Date(d.billDetails[0]?.toPeriod).getTime(); 8                const days = Math.floor(overdueBy / (86400 * 1000)); 9                return ( 10                  <React.Fragment> 11                    {"₹" + d["totalAmount"]} 12                    {days >= 0 ? ( 13                      <span className={"card-label-error"} style={{ fontSize: "16px", fontWeight: "normal" }}>{` ( ${t( 14                        "CS_PAYMENT_OVERDUE" 15                      )} ${days} ${t(days === 1 ? "CS_COMMON_DAY" : "CS_COMMON_DAYS")})`}</span> 16                    ) : null} 17                  </React.Fragment> 18                ); 19              }, 20            ], 21            fallback: "N/A", 22            noteStyle: { fontWeight: "bold", fontSize: "24px", paddingTop: "5px" }, 23          }, 24          { 25            keyValue: "PT_PROPERTY_ID", 26            keyPath: ["propertyId"], 27            fallback: "", 28          } 29 ] 30}``

Here my-bill key has config for my-bills screen, this configuration decides what details to show on the card for each service from the bill object returned through fetchBill API.

It is an array of objects, where each object puts the bill detail on the My-Bills bill card.

each object contains 4 properties ie keyValue, keyPath, fallback, noteStyle

the keynote config is added into the Digit component Registry as getBillDetailsConfigWithBusinessService

The implementation of the config can be found in the link :-

[https://github.com/egovernments/digit-ui-internals/blob/development/packages/modules/common/src/payments/citizen/bills/routes/my-bills/my-bills.js](https://github.com/egovernments/digit-ui-internals/blob/development/packages/modules/common/src/payments/citizen/bills/routes/my-bills/my-bills.js)

**Bill Details Screen**

The bill details screen can be found in the link :-

[https://github.com/egovernments/digit-ui-internals/blob/development/packages/modules/common/src/payments/citizen/bills/routes/bill-details/bill-details.js](https://github.com/egovernments/digit-ui-internals/blob/development/packages/modules/common/src/payments/citizen/bills/routes/bill-details/bill-details.js)

It checks for various payment restrictions which are fetched from the MDMS on above mentioned MY Bills description, and also all the tax heads that are to be displayed in the summary are also fetched from the same MDMS.

The structure for payment rule response from the MDMS is :-`1 { 2                   "businessService": "PropertyTax", 3                    "code": "PT", 4                    "collectionModesNotAllowed": [ 5                        "DD", 6                        "OFFLINE_NEFT", 7                        "OFFLINE_RTGS", 8                        "POSTAL_ORDER" 9                    ], 10                    "partPaymentAllowed": true, 11                    "minAmountPayable": 100, 12                    "isAdvanceAllowed": false, 13                    "demandUpdateTime": 86400000, 14                    "isVoucherCreationEnabled": true, 15                    "billGineiURL": "egov-searcher/bill-genie/billswithaddranduser/_g 16}`

partPaymentAllowed key when true allows payment less than bill details to be payed otherwise the user can pay only bill Amount.

minAmountPayable is the minimum bill amount a user can pay.

isAdvanceAllowed if true user can enter the amount more than the specified.

The link for the MDMS can be found at :-

[https://github.com/egovernments/egov-mdms-data/blob/DEV/data/pb/BillingService/BusinessService.json](https://github.com/egovernments/egov-mdms-data/blob/DEV/data/pb/BillingService/BusinessService.json)

**Payment Screen**

The payment screen fetches the payment gateways from an MDMS call.`1{ 2 "MdmsCriteria": { 3 "tenantId": "pb", 4 "moduleDetails": [ 5 { 6 "moduleName": "DIGIT-UI", 7 "masterDetails": [ 8 { 9 "name": "PaymentGateway" 10 } 11 ] 12 } 13 ] 14 } 15}`

The code can be found here

[https://github.com/egovernments/digit-ui-internals/blob/development/packages/modules/common/src/payments/citizen/payment-type/index.js](https://github.com/egovernments/digit-ui-internals/blob/development/packages/modules/common/src/payments/citizen/payment-type/index.js)

**Response Screen**

The response page code can be found here:-

[https://github.com/egovernments/digit-ui-internals/blob/development/packages/modules/common/src/payments/citizen/response/index.js](https://github.com/egovernments/digit-ui-internals/blob/development/packages/modules/common/src/payments/citizen/response/index.js)

**Search Screen**

The search screen is a part of PT module and it’s code can be found in

[https://github.com/egovernments/digit-ui-internals/blob/development/packages/modules/pt/src/pages/citizen/SearchProperty/index.js](https://github.com/egovernments/digit-ui-internals/blob/development/packages/modules/pt/src/pages/citizen/SearchProperty/index.js)

**Search Result Screen**

The Search Result screen code can be referred from

[https://github.com/egovernments/digit-ui-internals/blob/development/packages/modules/pt/src/pages/citizen/SearchResults/index.js](https://github.com/egovernments/digit-ui-internals/blob/development/packages/modules/pt/src/pages/citizen/SearchResults/index.js)

#### Adding a new Bill detail for the business Service <a id="Adding-a-new-Bill-detail-for-the-business-Service"></a>

The keynote config is responsible for adding the new bill UI for adding a new Bill for a business Service.

The whole function is exposed within the component Registry as getBillDetailsConfigWithBusinessService

and can be redefined from there.

[https://github.com/egovernments/digit-ui-internals/blob/development/packages/modules/common/src/payments/citizen/keynotesConfig.js](https://github.com/egovernments/digit-ui-internals/blob/development/packages/modules/common/src/payments/citizen/keynotesConfig.js)

**API Call Role Action mapping:**

| **S. No.** | **API** | **Action id** | **Roles** |
| :--- | :--- | :--- | :--- |
| 1 | /access/v1/actions/mdms/\_get | 870 | CITIZEN |
| 3 | /egov-mdms-service/v1/\_search | 954 | CITIZEN |
| 4 | /localization/messages/v1/\_search | 1531 | CITIZEN |
| 5 | /billing-service/bill/v2/\_fetchbill | 1862 | CITIZEN, |
| 6 | /pg-service/transaction/v1/\_create | 1571 | CITIZEN |
| 7 | /collection-services/payments/\_search | 1864 | CITIZEN |
| 8 | /pg-service/transaction/v1/\_update | 1572 | CITIZEN |
| 9 | collection-services/payments/PT/\_search | 2029 | PTCEMP, CITIZEN |

