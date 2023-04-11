---
description: >-
  Water & Sewerage my applications feature for citizen users - technical
  implementation doc
---

# Citizen: My Applications

**Objective:** Provide the UI technical implementation details for the My Applications feature available for citizen users.

## Workflow Details

Users can review the list of applications and their status registered under their mobile numbers in the My Applications tab. Each application for the initial view displays Application No., Service Name, Consumer Name, Property Id, Status, SLA and Property Address with the View Details option, through which the user can look up more details about the application.

![](<../../../../../.gitbook/assets/image (49).png>)

Once the user clicks on the View Details button, the Application Details page is displayed with all the necessary information about the application.

![](<../../../../../.gitbook/assets/image (126).png>)

There are two links provided in the application details screen. One is for Property Details which allows users to see the in-depth details of the property associated with the application. The other is available on the Connection Details page to view the Additional Details of the connection for the application.

![](<../../../../../.gitbook/assets/image (95).png>)

![](<../../../../../.gitbook/assets/image (104).png>)

**Timeline Component**

The Timeline component is present at the end of the application details which tells about the current status and history of the application (open to edit, approve, reject, or closed).

![](<../../../../../.gitbook/assets/image (86).png>)

## **Technical Implementation Details**

The file path for the My Applications and Application Details common Index is given below. It provides an understanding of the working of the code.&#x20;

File path: packages/modules/ws/src/pages/citizen/WSMyApplications/index.js

The template for My Application is available within packages/modules/ws/src/pages/citizen/WSMyApplications/ws-application.js. The Application Details page is available within packages/modules/ws/src/pages/citizen/WSApplicationDetails.js. The Application list is retrieved by calling the search API `"/ws-services/wc/_search"` & `"/sw-services/swc/_search"`

Hooks used for fetching the applications for Water and Sewerage are:

{% code lineNumbers="true" %}
```
const { isLoading, isError, error, data } = Digit.Hooks.ws.useMyApplicationSearch({ filters: filter1 }, { filters: filter1 });

const { isLoading: isSWLoading, isError : isSWError, error : SWerror, data: SWdata } = Digit.Hooks.ws.useMyApplicationSearch({ filters: filter1,BusinessService:"SW"}, { filters: filter1 });
```
{% endcode %}

## **MDMS Data**

No MDMS data is used here. The data is loaded from the Search API.

## **Localization Details**

For My Applications, the Localization keys are added to the ‘_rainmaker-ws_’ locale module same as My connections and Create. Changes, updates or addition of any new localization key is done in the same locale module only.

## **API Role Action Mapping**

| URL                                                 | Roles                   | Action ID |
| --------------------------------------------------- | ----------------------- | --------- |
| `egov-workflow-v2/egov-wf/process/_search`          | `PTCEMP,FI,APPROVER,DV` | `1730`    |
| `/ws-services/wc/_search`                           | `PTCEMP,FI,APPROVER,DV` |           |
| `/sw-services/swc/_search`                          | `PTCEMP,FI,APPROVER,DV` |           |
| `/egov-workflow-v2/egov-wf/businessservice/_search` | `PTCEMP,FI,APPROVER,DV` | `1743`    |
| `/filestore/v1/files/url`                           | `PTCEMP,FI,APPROVER,DV` | `1528`    |
