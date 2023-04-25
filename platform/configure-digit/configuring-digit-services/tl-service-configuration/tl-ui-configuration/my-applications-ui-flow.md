# My Applications UI Flow

## **Overview**

Users can review the list of applications and their status registered under their mobile numbers in the My Applications tab. Each Application for the initial view displays the Application No, Service Category, Owner Name (Multiple with a comma), status, SLA, and Trade Name with the View Details option. If the status is pending for payment the View Details & Pay button is available that enables the users to look up more details about the application.

![](<../../../../../.gitbook/assets/image (231) (5).png>)

Once the user clicks on the View Details or View Details & Pay button, the Application Details Page is displayed with all the necessary information about the application.

![](<../../../../../.gitbook/assets/image (260).png>)

The user can download the Application Acknowledgement Form (status - pending for payment ) or TL Certificate or the payment receipt using the Download Link button available at the top right corner of the page.

![](<../../../../../.gitbook/assets/image (148).png>)

![](<../../../../../.gitbook/assets/image (150).png>)

If the status is Pending for Payment for the application or Action required by a citizen (discussed elaborately here), a button will be visible to pay or edit at the end of the page respectively. On clicking on the Make Payment button it will redirect to the common pay screen through which the user can make the payment.

![](<../../../../../.gitbook/assets/image (270).png>)

**Timeline Component -** timeline component is present at the end of the application details which tells about the current status and history of the application being initiated, Applied, Pending for Document Verification, Pending for Field Inspection, Pending approval, Pending payment, Approved etc.

![](<../../../../../.gitbook/assets/image (257).png>)

## **Technical Implementation Details**

The link for the Applications and Application Details main code is given below, it can be used to understand the working of the code, Below is the folder link.

[<img src="https://github.com/fluidicon.png" alt="" data-size="line">digit-ui-internals/packages/modules/tl/src/pages/citizen/Applications at main · egovernments/digit-ui-internals](https://github.com/egovernments/digit-ui-internals/tree/main/packages/modules/tl/src/pages/citizen/Applications)

The template for My Application List is present under [https://github.com/egovernments/digit-ui-internals/blob/main/packages/modules/tl/src/pages/citizen/Applications/Application.js](https://github.com/egovernments/digit-ui-internals/blob/main/packages/modules/tl/src/pages/citizen/Applications/Application.js) and Application Details page is present inside - [https://github.com/egovernments/digit-ui-internals/blob/main/packages/modules/tl/src/pages/citizen/Applications/ApplicationDetails.js](https://github.com/egovernments/digit-ui-internals/blob/main/packages/modules/tl/src/pages/citizen/Applications/ApplicationDetails.js) .

All the Application lists are retrieved by calling the search API "`/tl-services/v1/_search`". If the view is set as “bills”, all the application is loaded using the hook `useFetchBill` which calls the `/billing-service/bill/v2/_fetchbill` API. SLA value in the Application List Screen is calculated from the data received from workflow API : `/egov-workflow-v2/egov-wf/process/_search`

Following is the hook used for the trade search API.

```
const { isLoading, isError, data, error, ...rest } = view === "bills" ? Digit.Hooks.tl.useFetchBill(
    {
      params: { businessService: "TL", tenantId, mobileNumber },
      config: { enabled: view === "bills" }
    }
  ) : Digit.Hooks.tl.useTLSearchApplication({}, {
    enabled: view !== "bills"
  });
```

To get the Application details in key-value format, in order to make it more compatible, the following hook is being used, which is a common service to be used across modules.

```
 const { isLoading, isError, error, data: application, error: errorApplication } = Digit.Hooks.tl.useTLApplicationDetails({
    tenantId: tenantId,
    applicationNumber: id,
  });
```

## **MDMS**

No MDMS data is being used here, all the data is being loaded from Search API/Fetch Bill API.

## **Localization**

For My Applications also the localization keys are added in the ‘_rainmaker-tl_’ locale module same as other parts of the TL module. Change, update or add any new localization key is done in the same locale module only.



> [![Creative Commons License](https://i.creativecommons.org/l/by/4.0/80x15.png)_​_](http://creativecommons.org/licenses/by/4.0/)_All content on this page by_ [_eGov Foundation_](https://egov.org.in/) _is licensed under a_ [_Creative Commons Attribution 4.0 International License_](http://creativecommons.org/licenses/by/4.0/)_._
