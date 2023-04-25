# Employee: Bill Amendment - Create Flow

**Objective:** The create Bill Amendment feature is used for applying for amendments on Water and Sewerage Bills.&#x20;

## Workflow Details <a href="#objective" id="objective"></a>

Bill amendment can be applied on any Water and Sewerage connection for which the bill has been generated and an amount is due. Counter Employee can apply for a bill amendment i.e., User with these roles “WS\_CEMP”, “SW\_CEMP”.

Every bill amendment application is part of the workflow.

The Create Bill Amendment flow starts when the user clicks on the action Bill Amendment from the Connection Details page of Water/Sewerage Connection and a Required Documents acknowledge screen is rendered.

{% hint style="info" %}
Bill Amendment action will only be enabled when a bill is generated and an amount is due.
{% endhint %}

<figure><img src="../../../../../.gitbook/assets/image (90).png" alt=""><figcaption></figcaption></figure>

Clicking on apply continues the flow and renders the bill amendment apply page.

<figure><img src="../../../../../.gitbook/assets/image (568).png" alt=""><figcaption></figcaption></figure>

* Here the user can enter the required details, like whether the user wants to apply for a Reduced amount(Rebate) or an additional amount(penalty). Other details can be understood from the screen itself.
* Apart from the details users also have the option to add a Rebate/ Penalty that is not covered under the default tax heads and is shown at the bottom as an Adhoc rebate/penalty.

<figure><img src="../../../../../.gitbook/assets/image (559).png" alt=""><figcaption></figcaption></figure>

When a user clicks on Submit and all the validations on frontend are successful then a create post request is sent the this API endpoint “`/billing-service/amendment/_create?`“ with an Amendment Object in the body(payload) which contains all the required details to apply for the amendment and a corresponding success/failure acknowledgement screen is shown on the screen.

<figure><img src="../../../../../.gitbook/assets/image (572).png" alt=""><figcaption></figcaption></figure>

## Technical Implementation Details

Bill Amendment File path:

{% embed url="https://github.com/egovernments/DIGIT-Dev/blob/6fe9842a7c175f0d38ec007ec14bc0eeb958e707/frontend/micro-ui/web/micro-ui-internals/packages/modules/ws/src/pages/employee/RequiredDocuments.js" %}

Bill Amendment Apply File Path:

{% embed url="https://github.com/egovernments/DIGIT-Dev/blob/6fe9842a7c175f0d38ec007ec14bc0eeb958e707/frontend/micro-ui/web/micro-ui-internals/packages/modules/ws/src/pages/employee/ApplicationBillAmendment.js" %}

{% hint style="info" %}
The payload sent to the “`/billing-service/amendment/_create`" endpoint looks like the following:
{% endhint %}

```
{
    "consumerCode": "WS/107/2021-22/227166",
    "tenantId": "pb.amritsar",
    "businessService": "WS",
    "amendmentReason": "COURT_CASE_SETTLEMENT",
    "reasonDocumentNumber": "1234",
    "effectiveFrom": 1652227200000,
    "effectiveTill": 1652313600000,
    "documents": [
        {
            "fileName": "consumer-PB-TL-2022-03-27-024497.pdf",
            "fileStoreId": "8c9ec928-a18f-41ee-b4ff-283e715d31ad",
            "fileStore": "8c9ec928-a18f-41ee-b4ff-283e715d31ad",
            "documentType": "PASTBILLS",
            "fileUrl": "https://egov-rainmaker.s3-ap-south-1.amazonaws.com/pb.amritsar/WS/May/11/1652243671676UFiQJSMWqv.pdf?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIA42DEGMQ2NZVNTLNI%2F20220511%2Fap-south-1%2Fs3%2Faws4_request&X-Amz-Date=20220511T043431Z&X-Amz-Expires=86400&X-Amz-SignedHeaders=host&X-Amz-Signature=c2d089faac71ee0ee3597b26d450555e5a4b9d1a27a29d7cb51b3a37632dcd76"
        },
        {
            "fileName": "consumer-PB-TL-2022-03-27-024497.pdf",
            "fileStoreId": "6292701a-00a2-4dc3-ba83-528373934767",
            "fileStore": "6292701a-00a2-4dc3-ba83-528373934767",
            "documentType": "IDENTITYPROOF",
            "fileUrl": "https://egov-rainmaker.s3-ap-south-1.amazonaws.com/pb.amritsar/WS/May/11/1652243675149sIkVhbTMFg.pdf?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIA42DEGMQ2NZVNTLNI%2F20220511%2Fap-south-1%2Fs3%2Faws4_request&X-Amz-Date=20220511T043435Z&X-Amz-Expires=86400&X-Amz-SignedHeaders=host&X-Amz-Signature=a5ff23c0c145792086e0cbc08e060becbea2c8ee3792ba039bbb9125c0f03b26"
        },
        {
            "fileName": "consumer-PB-TL-2022-03-27-024497.pdf",
            "fileStoreId": "9bab8541-ed04-4a9b-99c9-51407ebf0021",
            "fileStore": "9bab8541-ed04-4a9b-99c9-51407ebf0021",
            "documentType": "ADDRESSPROOF",
            "fileUrl": "https://egov-rainmaker.s3-ap-south-1.amazonaws.com/pb.amritsar/WS/May/11/1652243678618FJZAJZkOjr.pdf?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIA42DEGMQ2NZVNTLNI%2F20220511%2Fap-south-1%2Fs3%2Faws4_request&X-Amz-Date=20220511T043438Z&X-Amz-Expires=86400&X-Amz-SignedHeaders=host&X-Amz-Signature=e74b3e374d93571815a0ad321addec3634e4f88af2b2f9aee9aab6083d496c81"
        },
        {
            "fileName": "consumer-PB-TL-2022-03-27-024497.pdf",
            "fileStoreId": "0ba7df45-9767-4969-a7b6-a3ca21ebd354",
            "fileStore": "0ba7df45-9767-4969-a7b6-a3ca21ebd354",
            "documentType": "COURTORDER",
            "fileUrl": "https://egov-rainmaker.s3-ap-south-1.amazonaws.com/pb.amritsar/WS/May/11/1652243668712ndmiSGTcuP.pdf?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIA42DEGMQ2NZVNTLNI%2F20220511%2Fap-south-1%2Fs3%2Faws4_request&X-Amz-Date=20220511T043429Z&X-Amz-Expires=86400&X-Amz-SignedHeaders=host&X-Amz-Signature=e62a348748677e73b93b71d8721050a1cd428d488be7a478593d7f070c4119b9"
        },
        {
            "fileName": "acknowledgement.pdf",
            "fileStoreId": "0d759e3e-acc2-4f4a-9098-18df24ae3967",
            "fileStore": "0d759e3e-acc2-4f4a-9098-18df24ae3967",
            "documentType": "SELFDECLARATION",
            "fileUrl": "https://egov-rainmaker.s3-ap-south-1.amazonaws.com/pb.amritsar/WS/May/11/1652243682179UKJXrGkfAR.pdf?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIA42DEGMQ2NZVNTLNI%2F20220511%2Fap-south-1%2Fs3%2Faws4_request&X-Amz-Date=20220511T043442Z&X-Amz-Expires=86400&X-Amz-SignedHeaders=host&X-Amz-Signature=aaf389d422b7520761230a4623a89bb71a3dbce878bddabfde7cabe7c4eaf3d7"
        }
    ],
    "demandDetails": [
        {
            "taxHeadMasterCode": "WS_CHARGE",
            "taxAmount": -100
        },
        {
            "taxHeadMasterCode": "WS_TIME_PENALTY",
            "taxAmount": -10
        },
        {
            "taxHeadMasterCode": "WS_TIME_INTEREST",
            "taxAmount": -5
        },
        {
            "taxHeadMasterCode": "WS_WATER_CESS",
            "taxAmount": -5
        }
    ],
    "additionalDetails": {
        "searchBillDetails": {
            "WS_CHARGE": "100",
            "WS_TIME_PENALTY": "10",
            "WS_TIME_INTEREST": "5",
            "WS_WATER_CESS": "5",
            "TOTAL": 120
        }
    }
}
```

## **MDMS Data**

* Tax Heads: [<img src="https://github.com/fluidicon.png" alt="" data-size="line">egov-mdms-data/TaxHeadMaster.json at 95466d51227427fcb79b45cc6ac6ef8be6b34f94 · egovernments/egov-mdms-data](https://github.com/egovernments/egov-mdms-data/blob/95466d51227427fcb79b45cc6ac6ef8be6b34f94/data/pb/BillingService/TaxHeadMaster.json)
* Demand Revision: [<img src="https://github.com/fluidicon.png" alt="" data-size="line">egov-mdms-data/DemandRevisionBasis.json at 95466d51227427fcb79b45cc6ac6ef8be6b34f94 · egovernments/egov-mdms-data](https://github.com/egovernments/egov-mdms-data/blob/95466d51227427fcb79b45cc6ac6ef8be6b34f94/data/pb/BillAmendment/DemandRevisionBasis.json)
* Required Documents: [<img src="https://github.com/fluidicon.png" alt="" data-size="line">egov-mdms-data/documentObj.json at 95466d51227427fcb79b45cc6ac6ef8be6b34f94 · egovernments/egov-mdms-dat](https://github.com/egovernments/egov-mdms-data/blob/95466d51227427fcb79b45cc6ac6ef8be6b34f94/data/pb/BillAmendment/documentObj.json)

## **Role Action Mapping** <a href="#role-action-mapping" id="role-action-mapping"></a>

| **API**                              | **ROLES**         | **ACTION ID**      |
| ------------------------------------ | ----------------- | ------------------ |
| `/billing-service/amendment/_create` | WS\_CEMP,SW\_CEMP | 2047               |
| `/egov-mdms-service/v1/_search`      | WS\_CEMP,SW\_CEMP | <p>954</p><p> </p> |
| `/filestore/v1/files/url`            | EMPLOYEE          |                    |

\
