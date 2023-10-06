---
description: >-
  Water & Sewerage my connection feature for citizen users - technical
  implementation doc
---

# Citizen: My Connections

**Objective:** Provide the UI technical implementation details for the My Connections feature available for citizen users.

## Workflow Details

Users can review the list of connections and their status registered under their mobile number in the My Connections tab. Each connection in the initial view will display the Consumer No, Service Name, Consumer Name, status, and property Address with the View Details option, through which the User can look up more details about the connection.

![](<../../../../../.gitbook/assets/image (156).png>)

Once the user clicks on the View Details button, the Connection Details page is displayed with all the necessary information about the connection.

![](<../../../../../.gitbook/assets/image (270).png>)

The link provided in the connection details page is similar to the link provided in the applications details page, eg Consumption details, for more reference [Citizen: Water & Sewerage - My Applications](citizen-my-applications.md)

## **Technical Implementation Details**

The path for the My Connections and Connection Details common Index is given below. It provides an understanding of the working of the code.&#x20;

**File path** - packages/modules/ws/src/pages/citizen/MyConnection/index.js

The template for My Connection is present within packages/modules/ws/src/pages/citizen/MyConnection/WSConnection.js. The Connection Details page is available within packages/modules/ws/src/pages/citizen/MyConnection/ConnectionDetails.js. The Connection list is retrieved by calling the search API `"/ws-services/wc/_search"` & `"/sw-services/swc/_search"` using the searchType as `CONNECTION` for the filter params.

Hooks used for fetching the connections for Water and Sewerage are:

{% code lineNumbers="true" %}
```
let filter1 = !isNaN(parseInt(filter))
    ? { tenantId: tenantId, mobileNumber: user?.info?.mobileNumber, searchType:"CONNECTION" }
    : { tenantId: tenantId, mobileNumber: user?.info?.mobileNumber, searchType:"CONNECTION" };

const { isLoading, isError, error, data } = Digit.Hooks.ws.useMyApplicationSearch({ filters: filter1 }, { filters: filter1 });

const { isLoading: isSWLoading, isError : isSWError, error : SWerror, data: SWdata } = Digit.Hooks.ws.useMyApplicationSearch({ filters: filter1,BusinessService:"SW"}, { filters: filter1 });
```
{% endcode %}

The code to the linked page, Consumption Details is available in the file: packages/modules/ws/src/pages/citizen/MyConnection/ConsumptionDetails.js

## **MDMS Data**

No MDMS data is used here. All data is loaded from the Search API.

## &#x20;**Localization**

For My Applications, the localization keys are added in the ‘_rainmaker-ws_’ locale module same as My connections and create. Changes, updates or addition of any new localization key is done in the same locale module only.

## **API Role Action Mapping**

| URL                                                 | Roles                   | Action ID |
| --------------------------------------------------- | ----------------------- | --------- |
| `egov-workflow-v2/egov-wf/process/_search`          | `PTCEMP,FI,APPROVER,DV` | `1730`    |
| `/ws-services/wc/_search`                           | `PTCEMP,FI,APPROVER,DV` |           |
| `/sw-services/swc/_search`                          | `PTCEMP,FI,APPROVER,DV` |           |
| `/egov-workflow-v2/egov-wf/businessservice/_search` | `PTCEMP,FI,APPROVER,DV` | `1743`    |
| `/filestore/v1/files/url`                           | `PTCEMP,FI,APPROVER,DV` | `1528`    |

