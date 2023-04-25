# Employee: Bill Amendment - Search, Edit & Resubmit, Approve, Reject & Send-Back Flows

**Objective:** To provide employees with search, edit, resubmit, approve, reject and option to send back amendment bills.

## Workflow Details <a href="#search-bill-amendment" id="search-bill-amendment"></a>

#### **Search Bill Amendment** <a href="#search-bill-amendment" id="search-bill-amendment"></a>

When the Bill Amendment application is created by the counter employee a bill amendment application number is generated. Using this number as well as other parameters, a user can search for the application on the Bill Amendment Inbox page.

{% hint style="info" %}
Insert Bill Amend inbox Screenshot here (not developed yet in new-UI)
{% endhint %}

The first column of the result is the Bill Amendment number and every cell in this column is a link that leads the user to the Bill Amendment application details. This page has all details regarding the amendment application.

{% hint style="info" %}
A download option is provided to download the application acknowledgement
{% endhint %}

<figure><img src="../../../../../.gitbook/assets/image (477).png" alt=""><figcaption></figcaption></figure>

{% hint style="info" %}
Timelines Panel shows the status history and current status of the application
{% endhint %}

{% hint style="info" %}
Once the application is approved the download button has the option to download coupon-pdf as well that looks as follows:
{% endhint %}

<figure><img src="../../../../../.gitbook/assets/image (585).png" alt=""><figcaption></figcaption></figure>

#### **Approve, Reject & Send-Back Bill Amendment** <a href="#approve-reject-and-send-back-bill-amendment" id="approve-reject-and-send-back-bill-amendment"></a>

Only users with the role of approver i.e., “WS-AP”, “SW-AP” can approve the application.

The Application Details page of the bill amendment contains the Take Action button on the action bar at the bottom of the screen. The Take Action button opens a dropdown that contains some options described below. After clicking any of the given options an Action modal window is rendered.

* Approve → After verifying approver can approve the application
* Reject → Approver can Reject the application by giving a reason in the comments section displayed in the action modal.
* Send-Back → Approver can send back the application to the counter employee after giving the reason in the action modal. This option is used when there is an error in the application or something needs to be changed by the counter employee.

<figure><img src="../../../../../.gitbook/assets/image (560).png" alt=""><figcaption></figcaption></figure>

For Counter Employees, the action bar is not visible until the approver sends the application back to the counter employee. It is visible when the approver sends back the application and it shows an option to resubmit using which the counter employee can submit the application again.

<figure><img src="../../../../../.gitbook/assets/image (517).png" alt=""><figcaption></figcaption></figure>

## Implementation Details

File Path:&#x20;

{% embed url="https://github.com/egovernments/DIGIT-Dev/blob/fed230dba3b9698a01310968bf052dc68de85801/frontend/micro-ui/web/micro-ui-internals/packages/modules/ws/src/pages/employee/ApplicationDetailsBillAmendment.js" %}

## **MDMS Data**

* Tax Heads: [<img src="https://github.com/fluidicon.png" alt="" data-size="line">egov-mdms-data/TaxHeadMaster.json at 95466d51227427fcb79b45cc6ac6ef8be6b34f94 · egovernments/egov-mdms-data](https://github.com/egovernments/egov-mdms-data/blob/95466d51227427fcb79b45cc6ac6ef8be6b34f94/data/pb/BillingService/TaxHeadMaster.json)
* Demand Revision: [<img src="https://github.com/fluidicon.png" alt="" data-size="line">egov-mdms-data/DemandRevisionBasis.json at 95466d51227427fcb79b45cc6ac6ef8be6b34f94 · egovernments/egov-mdms-data](https://github.com/egovernments/egov-mdms-data/blob/95466d51227427fcb79b45cc6ac6ef8be6b34f94/data/pb/BillAmendment/DemandRevisionBasis.json)
* Required Documents: [<img src="https://github.com/fluidicon.png" alt="" data-size="line">egov-mdms-data/documentObj.json at 95466d51227427fcb79b45cc6ac6ef8be6b34f94 · egovernments/egov-mdms-data](https://github.com/egovernments/egov-mdms-data/blob/95466d51227427fcb79b45cc6ac6ef8be6b34f94/data/pb/BillAmendment/documentObj.json)

## API Details

| **API**                              |                    | **API description**                                                          |
| ------------------------------------ | ------------------ | ---------------------------------------------------------------------------- |
| `inbox/v1/_search?_`                 | `WS_CEMP, SW_CEMP` | `Bill Amendment Search`                                                      |
| `/billing-service/amendment/_update` | `WS_CEMP, WS_AP`,  | `To Update bill amendment application(For edit,resubmit,approve and reject)` |

&#x20;
