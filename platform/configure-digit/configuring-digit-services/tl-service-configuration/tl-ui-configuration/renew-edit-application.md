# Renew Edit Application

All the fields in this flow are the same as the New TL Application. The difference here is that max fields are having pre-populated data (On Loading the page, search is made for that particular application).

Will get the Renew Trade License option, when the application is in an approved state and the same financial year application is not present in the workflow.

File path:[ <img src="https://github.com/fluidicon.png" alt="" data-size="line">digit-ui-internals/ApplicationDetails.js at main · egovernments/digit-ui-internals](https://github.com/egovernments/digit-ui-internals/blob/main/packages/modules/tl/src/pages/employee/ApplicationDetails.js)

![](<../../../../../.gitbook/assets/image (269) (1).png>)

When we click on the Renew Trade License application, it will route to Renew screen

File Path:[ <img src="https://github.com/fluidicon.png" alt="" data-size="line">digit-ui-internals/ApplicationDetails.js at main · egovernments/digit-ui-internals](https://github.com/egovernments/digit-ui-internals/blob/main/packages/modules/tl/src/pages/employee/ApplicationDetails.js)

![](<../../../../../.gitbook/assets/image (232).png>)

File Path:[ <img src="https://github.com/fluidicon.png" alt="" data-size="line">digit-ui-internals/index.js at main · egovernments/digit-ui-internals](https://github.com/egovernments/digit-ui-internals/blob/main/packages/modules/tl/src/pages/employee/ReNewApplication/index.js)

**Direct Renewal:** There is no change in any fields and directly clicks on submitting an application, an update API call is made for the respective application with respective to Direct Renewal (`applicationType`: `RENEWAL`, `workflowCode`: `DIRECTRENEWAL,` )and it will go into direct renewal flow.

**Edit Renewal:** If there is any change in any fields and clicks on submitting an application, an update API call is made with respect to edit renewal (`applicationType`: `RENEWAL`,`workflowCode`: `EDITRENEWAL` )and update the application and it will go into the edit renewal flow.

**Units, Accessories, Owners and documents details in case of Edit/Renewal flow**

1. Employee can edit units in both cases, employee can add and delete multiple units, please find the file below reg all use cases:[ <img src="https://github.com/fluidicon.png" alt="" data-size="line">digit-ui-internals/TLTradeUnitsEmployee.js at main · egovernments/digit-ui-internals](https://github.com/egovernments/digit-ui-internals/blob/main/packages/modules/tl/src/pageComponents/TLTradeUnitsEmployee.js)
2. Employee cannot edit accessories in both cases, the employee can not add and delete multiple units and all fields are in disable state, please find the file below reg all use cases:[ <img src="https://github.com/fluidicon.png" alt="" data-size="line">digit-ui-internals/TLAccessoriesEmployee.js at main · egovernments/digit-ui-internals](https://github.com/egovernments/digit-ui-internals/blob/main/packages/modules/tl/src/pageComponents/TLAccessoriesEmployee.js)
3. Employee can edit in both cases, expect ownership details, ownership details field is in disable state in both cases. please find the file below reg all use cases:[ <img src="https://github.com/fluidicon.png" alt="" data-size="line">digit-ui-internals/TLTradeUnitsEmployee.js at main · egovernments/digit-ui-internals](https://github.com/egovernments/digit-ui-internals/blob/main/packages/modules/tl/src/pageComponents/TLTradeUnitsEmployee.js)
4. Employee can edit the documents in both cases, please find the file below reg all use cases:[ <img src="https://github.com/fluidicon.png" alt="" data-size="line">digit-ui-internals/TLDocumentsEmployee.js at main · egovernments/digit-ui-internals](https://github.com/egovernments/digit-ui-internals/blob/main/packages/modules/tl/src/pageComponents/TLDocumentsEmployee.js)

**Acknowledgement Screen**

After a successful update call, the user is routed to the acknowledgement screen.

File Path:[ <img src="https://github.com/fluidicon.png" alt="" data-size="line">digit-ui-internals/getTLAcknowledgementData.js at main · egovernments/digit-ui-internals](https://github.com/egovernments/digit-ui-internals/blob/main/packages/modules/tl/src/utils/getTLAcknowledgementData.js)

**EDIT Flow:** It is also the same as renewal flow only, but we are passing the action `action`: `RESUBMIT` on the update call with all the changes.

**Application/ Trade Details:** [Application Details/Trade Details](application-details-trade-details-ui-flows.md)

**TL Create New Application:**[ New Trade License Application](new-trade-license-ui-flow.md)

## **Role Action Mapping**

<table><thead><tr><th width="126">S.No.</th><th>API</th><th>Roles</th><th>Action ID</th></tr></thead><tbody><tr><td>1</td><td><code>/egov-mdms-service/v1/_search</code></td><td><code>TL_CEMP</code></td><td><code>954</code></td></tr><tr><td>2</td><td><code>/tl-services/v1/_create</code></td><td><code>TL_CEMP</code></td><td><code>1685</code></td></tr><tr><td>3</td><td><code>/tl-services/v1/_update</code></td><td><code>TL_CEMP</code></td><td><code>1686</code></td></tr><tr><td>4</td><td><code>/tl-calculator/billingslab/_search</code></td><td><code>TL_CEMP</code></td><td><code>1684</code></td></tr></tbody></table>
