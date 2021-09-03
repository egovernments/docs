---
description: 'New release features, enhancements, and fixes'
---

# Release Notes

### Release Summary <a id="Release-Summary"></a>

DIGIT 2.5 is a release that has got new modules, a few functional changes, and non-functional changes.

* Functional: Property Tax Citizen Open search flow UI/UX revamp, Property Tax Employee flow UI/UX revamp, Property Tax Mutation flow UI/UX revamp, HRMS UI/UX revamp, mCollect v2 \(eChallan\) UI/UX revamp, Trade License Citizen & Employee UI/UX revamp, Receipt Cancellation UI/UX Revamp, WhatsApp v2 \(Pay and Enhanced PGR\), Workflow Auto Escalation with reference implementations in PGR, W&S Enhancements, FSM DSS, and Standardized Reports for FSM/PT/mCollect.
* Non-functional: QA Automaton of APIs for FSM & eChallan, Product Standard Ontologies, Technical improvements, Internal Data Mart, etc.

### New ‌Feature Additions <a id="New-&#x200C;Feature-Additions"></a>

<table>
  <thead>
    <tr>
      <th style="text-align:left"><a href="http://s.no/"><b>S.No</b></a><b>.</b>
      </th>
      <th style="text-align:left"><b>Feature</b>
      </th>
      <th style="text-align:left"><b>Description</b>
      </th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td style="text-align:left">1</td>
      <td style="text-align:left">Property Tax UI/UX Revamp</td>
      <td style="text-align:left">
        <p><b>Citizen flow</b>
        </p>
        <ul>
          <li>Open Search and Payment</li>
        </ul>
        <p><b>Employee flow</b>
        </p>
        <ul>
          <li>Employee Inbox</li>
          <li>Create Property</li>
          <li>Search Property</li>
          <li>Transfer of Ownership</li>
          <li>Update Property</li>
          <li>Property Assessment</li>
        </ul>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">2</td>
      <td style="text-align:left">HRMS UI/UX Revamp</td>
      <td style="text-align:left">
        <ul>
          <li>Create employee</li>
          <li>Search employee</li>
          <li>Edit Employee</li>
          <li>Deactivate/re-activate employee</li>
        </ul>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">3</td>
      <td style="text-align:left">Trade License UX revamp</td>
      <td style="text-align:left">
        <ul>
          <li>Allow citizen to create Trade License application</li>
          <li>Allow citizen to check application status and make payment, download artefacts</li>
          <li>Allow Employee to create Trade License application on behalf of citizen</li>
          <li>Application processing by employees</li>
          <li>Allow citizen to renew the existing trade licenses which are due for renewal</li>
          <li>Allow employee to renew the existing trade license which are due for renewal</li>
        </ul>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">4</td>
      <td style="text-align:left">mCollect v2 (eChallan) UI/UX Revamp</td>
      <td style="text-align:left">
        <ul>
          <li>Challan Generation</li>
          <li>Challan Search Employee</li>
          <li>Total Challan Count</li>
          <li>My Challan - Citizen</li>
          <li>Search and Pay - Citizen</li>
        </ul>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">5</td>
      <td style="text-align:left">Receipt Cancellation UI/UX Revamp</td>
      <td style="text-align:left">Receipt Cancellation UI/UX Revamp</td>
    </tr>
    <tr>
      <td style="text-align:left">6</td>
      <td style="text-align:left">FSM DSS</td>
      <td style="text-align:left">
        <ul>
          <li>SLA Compliance</li>
          <li>Average Collections</li>
          <li>Performance by ULB and Districts</li>
          <li>Performance by Desludging Operator</li>
          <li>Plant Operating Efficiency</li>
          <li>Drill downs for Desluding and Vehicle log report</li>
        </ul>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">7</td>
      <td style="text-align:left">Workflow Auto Escalation</td>
      <td style="text-align:left">
        <ul>
          <li>Configure SLA at a workflow state level</li>
          <li>Escalate the application to a role if there is a breach in SLA</li>
          <li>Make the application status as deemed approved or reject on breach of
            an SLA</li>
          <li>Escalate the application to the next logical step in the workflow ladder
            if there is a breach in SLA</li>
        </ul>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">8</td>
      <td style="text-align:left">Product Standardized Reports</td>
      <td style="text-align:left">
        <p><b>FSM</b>
        </p>
        <ul>
          <li>Daily Collection Report</li>
          <li>Desludging Request Report</li>
          <li>Vehicle Log Report</li>
        </ul>
        <p><b>PT</b>
        </p>
        <ul>
          <li>Defaulter Report</li>
          <li>Collection Register Report</li>
          <li>Receipt Register Report</li>
        </ul>
        <p><b>mCollect</b>
        </p>
        <ul>
          <li>Challan Register Report</li>
          <li>Daily Collection Report</li>
          <li>Receipt Register Report</li>
        </ul>
      </td>
    </tr>
  </tbody>
</table>

### Enhancements <a id="Enhancements"></a>

<table>
  <thead>
    <tr>
      <th style="text-align:left"><a href="http://s.no/"><b>S.No</b></a><b>.</b>
      </th>
      <th style="text-align:left"><b>Updated Feature</b>
      </th>
      <th style="text-align:left"><b>Description</b>
      </th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td style="text-align:left">1</td>
      <td style="text-align:left">Water &amp; Sewerage Enhancements</td>
      <td style="text-align:left">
        <ul>
          <li>Bill Cancellation of latest bill</li>
          <li>Show Due Date in Arrears breakup</li>
          <li>Water &amp; Sewerage Combined PDF Changes</li>
          <li>Water &amp; Sewerage Due Validation on PT Title Transfer</li>
        </ul>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">2</td>
      <td style="text-align:left">WhatsApp v2 (Pay and PGR) Enhancements</td>
      <td style="text-align:left">
        <ul>
          <li><b>Improvements in Public Grievance Redressal Module</b>
            <ul>
              <li>Enhancements in messaging language.</li>
              <li>NLP Inclusion (For City &amp; Boundary Selection).</li>
            </ul>
          </li>
          <li><b>Improvements in Bill Payments</b>
            <ul>
              <li>Enhancements in messaging language.
                <ul>
                  <li>Inclusion of call to action buttons (for certain messages).</li>
                </ul>
              </li>
              <li>For Linked Mobile Numbers
                <ul>
                  <li>Single-click access to bills (for PT and W&amp;S)</li>
                </ul>
              </li>
              <li>For Non-Linked Mobile Numbers
                <ul>
                  <li>Provision of Search &amp; Pay (If Property/Connection Details are known).</li>
                  <li>Inclusion of Open Search Links (If Property/ Connection Details are unknown).</li>
                </ul>
              </li>
            </ul>
          </li>
          <li><b>Improvements in Payment History</b>
            <ul>
              <li>Enhancements in messaging language and flow.
                <ul>
                  <li>Inclusion of call to action buttons (for certain messages).</li>
                </ul>
              </li>
              <li>For Linked Mobile Numbers
                <ul>
                  <li>Access to view the last three payments made (for PT &amp; W&amp;S)</li>
                  <li>Provision to download the last three payment receipts</li>
                </ul>
              </li>
              <li>For Non-Linked Mobile Numbers
                <ul>
                  <li>Access control to view payments history only.</li>
                </ul>
              </li>
            </ul>
          </li>
        </ul>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">3</td>
      <td style="text-align:left">Bill Amendment Enhancement</td>
      <td style="text-align:left">
        <ul>
          <li>Additional changes in Bill Amendment screen to display current Demand</li>
        </ul>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">4</td>
      <td style="text-align:left">PT Enhancements</td>
      <td style="text-align:left">PT Enhancements - Fuzzy search for Name, Door number, and old PT ID (old
        UI)</td>
    </tr>
    <tr>
      <td style="text-align:left">5</td>
      <td style="text-align:left">QA Automaton of APIs</td>
      <td style="text-align:left">
        <p>APIs automation for</p>
        <ul>
          <li>eChallan APIs including end to end APIs automation</li>
          <li>Bill Amendment APIs</li>
          <li>FSM Inbox API</li>
        </ul>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">6</td>
      <td style="text-align:left">Other Improvements and Tech Enhancements</td>
      <td style="text-align:left">
        <ul>
          <li>Changes in Gender to introduce Transgender and Others.</li>
          <li>Standardization of Product ontologies for Property Tax, Water &amp; Sewerage,
            Fire NOC, mCollect (eChallan), PGR, and Online Building Plan Approval.</li>
          <li>Inbox API to support module wise inbox for UI/UX revamp.</li>
        </ul>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">7</td>
      <td style="text-align:left">Internal Data mart</td>
      <td style="text-align:left">Internal Data mart for PT, TL, PGR, W&amp;S, FSM, eChallan, OBPS, and
        Fire NOC modules.</td>
    </tr>
    <tr>
      <td style="text-align:left">8</td>
      <td style="text-align:left">eDCR Enhancements</td>
      <td style="text-align:left">
        <p></p>
        <ul>
          <li>River Distance: Colour code used to identify different river types.</li>
          <li>In the basement footprint layer, captured additional dimension to define
            the level of the basement under the ground.</li>
          <li>In the stilt parking layer, captured height from floor to the bottom of
            a beam of the stilt floor.</li>
        </ul>
      </td>
    </tr>
  </tbody>
</table>

### ‌Document Resources and Links <a id="&#x200C;Document-Resources-and-Links"></a>

#### UI Technical Documents

 **Trade License UI/UX Revamp**

 **Citizen**

{% page-ref page="../product/modules/trade-license-tl/tl-apply-flow-ui-details/" %}

{% page-ref page="../product/modules/trade-license-tl/tl-apply-flow-ui-details/my-applications-ui-flow.md" %}

{% page-ref page="../product/modules/trade-license-tl/tl-apply-flow-ui-details/send-back-edit-ui-flow.md" %}

{% page-ref page="../product/modules/trade-license-tl/tl-apply-flow-ui-details/trade-license-renewal-ui-flow.md" %}

 **Employee**

{% page-ref page="../product/modules/property-tax/pt-create-property-ui-details/create-application-employee-ui-ux-revamp.md" %}

{% page-ref page="../product/modules/property-tax/pt-create-property-ui-details/employee-inbox-and-application-details.md" %}

{% page-ref page="../product/modules/trade-license-tl/tl-apply-flow-ui-details/employee-search-application-search-license-ui-flow.md" %}

{% page-ref page="../product/modules/trade-license-tl/tl-apply-flow-ui-details/new-trade-license-ui-flow.md" %}

{% page-ref page="../product/modules/trade-license-tl/tl-apply-flow-ui-details/application-details-trade-details-ui-flows.md" %}

{% page-ref page="../product/modules/trade-license-tl/tl-apply-flow-ui-details/renew-edit-application.md" %}

 **HRMS UI/UX Revamp**

{% page-ref page="../product/modules/hrms/hrms-employee-create-edit-ui-flow.md" %}

{% page-ref page="../product/modules/hrms/employee-activation-deactivation-ui-flow.md" %}

{% page-ref page="../product/modules/hrms/employee-details-ui-flow.md" %}

{% page-ref page="../product/modules/hrms/search-employee-by-multiple-criteria-ui-flow.md" %}

{% page-ref page="../product/modules/hrms/employees-count-ui-flow.md" %}

 **Receipt cancellation UI/UX Revamp**

{% page-ref page="../product/modules/receipt-cancellation-ui-flow/" %}

{% page-ref page="../product/modules/receipt-cancellation-ui-flow/view-receipt-cancel-ui-flow.md" %}

 **Bill Cancellation**

{% page-ref page="../product/modules/current-bill-cancellation-ui-flow/" %}

{% page-ref page="../product/modules/current-bill-cancellation-ui-flow/bill-details-ui-flow.md" %}

{% page-ref page="../product/modules/current-bill-cancellation-ui-flow/cancel-bill-ui-flow.md" %}

 **mCollect v2 \(eChallan\) UI/UX Revamp**

{% page-ref page="../product/modules/mcollect-mcs/echallan-ui-details/mcollect-ui-flow.md" %}

{% page-ref page="../product/modules/mcollect-mcs/echallan-ui-details/update-cancel-challan-ui-flow.md" %}

{% page-ref page="../product/modules/mcollect-mcs/echallan-ui-details/search-and-pay-challan.md" %}

{% page-ref page="../product/modules/mcollect-mcs/echallan-ui-details/challan-creation.md" %}

 **Workflow Auto Escalation**

{% page-ref page="../product/modules/auto-escalation-ui-flow.md" %}

 **Property Tax UI/UX Revamp**

 **Citizen**

{% page-ref page="../product/modules/property-tax/pt-create-property-ui-details/" %}

{% page-ref page="../product/modules/property-tax/pt-create-property-ui-details/edit-update-property.md" %}

{% page-ref page="../product/modules/property-tax/pt-create-property-ui-details/property-tax-my-applications.md" %}

{% page-ref page="../product/modules/property-tax/pt-create-property-ui-details/property-tax-my-properties.md" %}

 **Employee**

{% page-ref page="../product/modules/property-tax/pt-create-property-ui-details/employee-edit-application-flow.md" %}

{% page-ref page="../product/modules/property-tax/pt-create-property-ui-details/create-application-employee-ui-ux-revamp.md" %}

{% page-ref page="../product/modules/property-tax/pt-create-property-ui-details/employee-search-property-property-details-page-and-assessment.md" %}

{% page-ref page="../product/modules/property-tax/pt-create-property-ui-details/employee-inbox-and-application-details.md" %}

 **Mutation**

{% page-ref page="../product/modules/property-tax/pt-create-property-ui-details/employee-mutation-ownership-transfer.md" %}

{% page-ref page="../product/modules/property-tax/pt-create-property-ui-details/citizen-mutation-flow.md" %}

 **DSS**

{% page-ref page="../product/modules/dss-ui-flow.md" %}

{% page-ref page="../product/modules/faecal-sludge-management-fsm/fsm-service-configuration/fsm-implementation-configuration.md" %}

#### Backend Service Documents

{% file src="../.gitbook/assets/egov-hrms \(1\).pdf" caption="eGov HRMS" %}

{% page-ref page="../product/modules/e-challan-service/" %}

{% page-ref page="../configuration/configure-digit/configuring-digit-services/configuring-workflows/workflow-auto-escalation.md" %}

{% page-ref page="../configuration/configure-digit/services-overview/core-services/nlp-engine-service.md" %}

{% page-ref page="../configuration/configure-digit/services-overview/core-services/xstate-core-chatbot/" %}

{% page-ref page="../configuration/configure-digit/services-overview/core-services/xstate-core-chatbot/xstate-chatbot-integration-document.md" %}

{% page-ref page="../configuration/configure-digit/services-overview/core-services/xstate-core-chatbot/xstate-chatbot-message-localisation.md" %}

{% page-ref page="../configuration/configure-digit/services-overview/business-services/collection-service/collection-service-v2.md" %}

{% page-ref page="../product/modules/faecal-sludge-management-fsm/fsm-service-configuration/fsm-services.md" %}

{% page-ref page="../product/modules/faecal-sludge-management-fsm/fsm-service-configuration/fsm-vehicle-registry-v1.0.md" %}

{% page-ref page="../product/modules/faecal-sludge-management-fsm/fsm-service-configuration/fsm-vendor-registry-v1.0.md" %}

{% page-ref page="../product/modules/faecal-sludge-management-fsm/fsm-service-configuration/legacy-re-indexing-the-fsm-data.md" %}

{% page-ref page="../configuration/configure-digit/services-overview/municipal-services/turn-io-adapter.md" %}

{% page-ref page="../product/modules/property-tax/property-tax-service/fuzzy-search/" %}

{% page-ref page="../product/modules/property-tax/property-tax-service/fuzzy-search/fuzzy-search-reindexing.md" %}

{% page-ref page="../product/modules/faecal-sludge-management-fsm/fsm-service-configuration/fsm-dss-technical-documentation.md" %}

{% page-ref page="../configuration/configure-digit/services-overview/municipal-services/inbox-service.md" %}

{% page-ref page="../configuration/configure-digit/configuring-digit-services/digit-internal-datamart-deployment-steps.md" %}











 [![Creative Commons License](https://i.creativecommons.org/l/by/4.0/80x15.png)\_\_](http://creativecommons.org/licenses/by/4.0/)_All content on this page by_ [_eGov Foundation_ ](https://egov.org.in/)_is licensed under a_ [_Creative Commons Attribution 4.0 International License_](http://creativecommons.org/licenses/by/4.0/)_._

