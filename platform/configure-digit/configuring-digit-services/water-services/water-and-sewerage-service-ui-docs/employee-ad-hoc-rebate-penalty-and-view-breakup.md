---
description: >-
  View breakup, ad-hoc rebate and penalty details in applications feature for
  employees - technical implementation doc
---

# Employee: Ad-hoc Rebate/Penalty & View Breakup

**Objective:** Provide the UI screens and configuration details for the ad-hoc rebate or penalty feature and the view breakup option available in water and sewerage applications.

## Workflow Details

#### Ad-hoc Rebate/Penalty

The Water and Sewerage ad-hoc Rebate/Penalty is a feature in WS Module. It allows employees to add rebates or penalties for Water and Sewerage Applications.

<figure><img src="../../../../../.gitbook/assets/image (54).png" alt=""><figcaption></figcaption></figure>

&#x20;Clicking on the Add Rebate/Penalty option opens the popup with the fields.

![](<../../../../../.gitbook/assets/image (112).png>)

Clicking on the Add button on the pop-up screen closes the pop-up window and the filled-in data is updated in the Fee Estimate card.

![](<../../../../../.gitbook/assets/image (98).png>)![](<../../../../../.gitbook/assets/image (152).png>)

{% hint style="info" %}
**Note:** After adding add rebate/penalty, we must perform at least one action, then only it will save the data in WS/SW service. Estimated API will give the results based on the data, presently we are saving the data in the additional details of the WS/SW service.\

{% endhint %}

#### View Breakup

The View Breakup feature in the WS module allows employees to view the details of tax heads for water and sewerage applications.

After logging in with `Water and sewerage employee` roles the user gets the option to view the breakup in the new WS/SW Application in the Fee Estimate card in the WS/SW application details.

WS/SW Application details: [Employee: Water and Sewerage Application Details](employee-application-details.md)

<figure><img src="../../../../../.gitbook/assets/image (121).png" alt=""><figcaption></figcaption></figure>

Clicking on the View Breakup option opens the popup with the updated data.

![](<../../../../../.gitbook/assets/image (51).png>)

## **Implementation Details**

Once the user logs in with `"WS_APPROVER", "WS_FIELD_INSPECTOR", "SW_FIELD_INSPECTOR", "SW_APPROVER".` If the roles and actions buttons are visible on the screen, then the user gets the option to add Ad-hoc Rebate/Penalty to a new WS/SW application in the Fee Estimate card in the WS/SW application details.

&#x20;WS/SW Application details: [Employee: Water and Sewerage Application Details](employee-application-details.md)

Route: [![](https://cdn.jsdelivr.net/npm/@egovernments/digit-ui-css/img/browser-icon.png)mSeva](https://qa.digit.org/digit-ui/employee/ws/application-details?applicationNumber=WS\_AP/107/2022-23/638816\&tenantId=pb.amritsar\&service=WATER\&from=WS\_SEWERAGE\_APPLICATION\_SEARCH)

Fee Estimation File Path: [https://github.com/egovernments/DIGIT-Dev/blob/develop/frontend/micro-ui/web/micro-ui-internals/packages/modules/templates/ApplicationDetails/components/WSFeeEstimation.js](https://github.com/egovernments/DIGIT-Dev/blob/develop/frontend/micro-ui/web/micro-ui-internals/packages/modules/templates/ApplicationDetails/components/WSFeeEstimation.js) and the initial data and logic is from the Application details in [https://github.com/egovernments/DIGIT-Dev/blob/develop/frontend/micro-ui/web/micro-ui-internals/packages/libraries/src/services/molecules/WS/Search.js](https://github.com/egovernments/DIGIT-Dev/blob/develop/frontend/micro-ui/web/micro-ui-internals/packages/libraries/src/services/molecules/WS/Search.js)

Fee Estimation Pop-up functionality is present in the [https://github.com/egovernments/DIGIT-Dev/blob/develop/frontend/micro-ui/web/micro-ui-internals/packages/modules/templates/ApplicationDetails/components/WSFeeEstimation.js](https://github.com/egovernments/DIGIT-Dev/blob/develop/frontend/micro-ui/web/micro-ui-internals/packages/modules/templates/ApplicationDetails/components/WSFeeEstimation.js)

Route: [![](https://cdn.jsdelivr.net/npm/@egovernments/digit-ui-css/img/browser-icon.png)mSeva](https://qa.digit.org/digit-ui/employee/ws/application-details?applicationNumber=WS\_AP/107/2022-23/638816\&tenantId=pb.amritsar\&service=WATER\&from=WS\_SEWERAGE\_APPLICATION\_SEARCH)

View Breakup File Path: [https://github.com/egovernments/DIGIT-Dev/blob/develop/frontend/micro-ui/web/micro-ui-internals/packages/modules/templates/ApplicationDetails/components/ViewBreakup.js](https://github.com/egovernments/DIGIT-Dev/blob/develop/frontend/micro-ui/web/micro-ui-internals/packages/modules/templates/ApplicationDetails/components/ViewBreakup.js) and the initial data and logic is from the Application details in [https://github.com/egovernments/DIGIT-Dev/blob/develop/frontend/micro-ui/web/micro-ui-internals/packages/libraries/src/services/molecules/WS/Search.js](https://github.com/egovernments/DIGIT-Dev/blob/develop/frontend/micro-ui/web/micro-ui-internals/packages/libraries/src/services/molecules/WS/Search.js)

View Breakup pop-up functionality is present in the [https://github.com/egovernments/DIGIT-Dev/blob/develop/frontend/micro-ui/web/micro-ui-internals/packages/modules/templates/ApplicationDetails/components/ViewBreakup.js](https://github.com/egovernments/DIGIT-Dev/blob/develop/frontend/micro-ui/web/micro-ui-internals/packages/modules/templates/ApplicationDetails/components/ViewBreakup.js)\


## **Localisation Details**

Localisation keys are added under the ‘_rainmaker-ws_’ locale module.

## **API Call Role Action Mapping**

| API                                                                                          | Action ID                                         | Roles                                                                                                                                                                                                          |
| -------------------------------------------------------------------------------------------- | ------------------------------------------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `/localization/messages/v1/_search`                                                          | `1531`                                            |                                                                                                                                                                                                                |
| /`ws-calculator/waterCalculator/_estimate` and `/sw-calculator/sewerageCalculator/_estimate` | <p><code>1966,</code></p><p><code>1967</code></p> | <p><code>WS_CEMP</code>,<code>WS_DOC_VERIFIER</code>,<code>WS_FIELD_INSPECTOR</code>,<code>WS_APPROVER</code>,<code>WS_CLERK</code></p><p><code>SW_CEMP,SW_DOC_VERIFIER,SW_FIELD_INSPECTOR,SW_CLERK</code></p> |
| `/billing-service/bill/v2/_fetchbill`                                                        | `1862`                                            | `EMPLOYEE`                                                                                                                                                                                                     |
| `collection-services/payments/{businessService}/_search/`                                    |                                                   | `EMPLOYEE`                                                                                                                                                                                                     |
| `/egov-mdms-service/v1/_search`                                                              | `954`                                             |                                                                                                                                                                                                                |

**Employee Roles and Credentials:** The employee roles and credentials are available in the document here: [<img src="https://developers.google.com/drive/images/drive_icon.png" alt="" data-size="line">DIGIT Login Credentials](https://docs.google.com/spreadsheets/d/15p6dmlVUXvopvzyyG06ty2rxtffSMQxN5F2l2FSWoFA/edit#gid=0)
