---
description: >-
  Water and Sewerage connection details feature for employees - technical
  implementation doc
---

# Employee: Connection Details

**Objective:** Provide the details of the connection to the employees and citizens.

## Connection Details

<figure><img src="../../../../../.gitbook/assets/image (376).png" alt=""><figcaption></figcaption></figure>

The Connection Details page provides the details about the connection, the property which is used to create the connection and the owner details of the property. The same can be downloaded as a PDF file or printed directly from the page.

Employees will be able to open the “View Consumption Details” page from the “Connection Details” page for the Metered Reading Connection. The Consumption Details page will provide more options like adding details of the consumed water charges.

<figure><img src="../../../../../.gitbook/assets/image (141).png" alt=""><figcaption></figcaption></figure>

Users have the option to add new meter readings. Clicking on it displays a pop-up, where the user can fill in the asked details and click on submit to add a new meter reading for the connection.

![](<../../../../../.gitbook/assets/image (570).png>)

#### Downloads

![](<../../../../../.gitbook/assets/image (567).png>)

## Technical Implementation Details

The hook used for fetching connection details -

```
const { isLoading, isError, data: response } = Digit.Hooks.ws.useWSConsumptionSearch({ filters: filter1 }, { filters: filter1 });
```

Connection Details File Path: [https://github.com/egovernments/DIGIT-Dev/blob/master/frontend/micro-ui/web/micro-ui-internals/packages/modules/ws/src/pages/employee/connectionDetails/ConsumptionDetails.js](https://github.com/egovernments/DIGIT-Dev/blob/master/frontend/micro-ui/web/micro-ui-internals/packages/modules/ws/src/pages/employee/connectionDetails/ConsumptionDetails.js)

Meter Reading File Path: [https://github.com/egovernments/DIGIT-Dev/blob/develop/frontend/micro-ui/web/micro-ui-internals/packages/modules/ws/src/pages/employee/connectionDetails/connectionDetails.js](https://github.com/egovernments/DIGIT-Dev/blob/develop/frontend/micro-ui/web/micro-ui-internals/packages/modules/ws/src/pages/employee/connectionDetails/connectionDetails.js)

**Hook details for connection details search and others:**

```
const { isLoading, isError, data: applicationDetails, error } = Digit.Hooks.ws.useConnectionDetail(t, tenantId, applicationNumber, serviceType);
const {    isLoading: updatingApplication,    isError: updateApplicationError,    data: updateResponse,    error: updateError,    mutate,  } = Digit.Hooks.ws.useWSApplicationActions(serviceType);
const { data: reciept_data, isLoading: recieptDataLoading } = Digit.Hooks.useRecieptSearch(    {      tenantId: stateCode,      businessService:  serviceType == "WATER" ? "WS.ONE_TIME_FEE" : "SW.ONE_TIME_FEE",      consumerCodes: applicationDetails?.applicationData?.applicationNo    },    {      enabled: (applicationDetails?.applicationData?.applicationNo && applicationDetails?.applicationData?.applicationType?.includes("NEW_") && !applicationDetails?.colletionOfData?.length > 0) ? true : false    }  );
```

Downloads File Path: [https://github.com/egovernments/DIGIT-Dev/blob/develop/frontend/micro-ui/web/micro-ui-internals/packages/modules/ws/src/pages/employee/connectionDetails/connectionDetails.js](https://github.com/egovernments/DIGIT-Dev/blob/develop/frontend/micro-ui/web/micro-ui-internals/packages/modules/ws/src/pages/employee/connectionDetails/connectionDetails.js)

**Download Receipt Method:**

```
const appFeeDownloadReceipt = {    order: 1,    label: t("DOWNLOAD_RECEIPT_HEADER"),    onClick: () => getRecieptSearch(reciept_data?.Payments?.[0]),  };
```

**Connection Details Receipt Method:**

```
const connectionDetailsReceipt = {    order: 2,    label: t("WS_CONNECTION_DETAILS_RECEIPT"),    onClick: () => downloadConnectionDetails(),  };
```

## **Localisation Details**

Localisation keys used on this page are added under “rainmaker-ws” locale module and the same should be used if any new keys are added to this page.

## **API Call Role Action Mapping**

| API                                      | Action ID | Role                                                                      |
| ---------------------------------------- | --------- | ------------------------------------------------------------------------- |
| `/ws-calculator/meterConnection/_search` | `1913`    | `EMPLOYEE`                                                                |
| `/billing-service/bill/v2/_fetchbill`    | `1862`    | `EMPLOYEE`                                                                |
| `/ws-services/wc/_search`                | `1900`    | `WS_CEMP`,`WS_DOC_VERIFIER`,`WS_FIELD_INSPECTOR`,`WS_APPROVER`,`WS_CLERK` |
| `/sw-services/swc/_search`               | `1919`    | `WS_CEMP`,`WS_DOC_VERIFIER`,`WS_FIELD_INSPECTOR`,`WS_APPROVER`,`WS_CLERK` |
| /`property-services/property/_search`    | `1897`    | `EMPLOYEE`                                                                |
