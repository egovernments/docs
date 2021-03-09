---
description: 'New release features, enhancements, and fixes'
---

# DIGIT 2.3 Release Notes

### Release Summary <a id="Release-Summary"></a>

DIGIT 2.3 is a release that has got new modules, a few functional changes, and non-functional changes.

* Functional: Faecal Sludge Management module, Bill Amendment module, and Enhancements in HRMS.
* Non-functional: Security fixes.

### New ‌Feature Additions <a id="New-&#x200C;Feature-Additions"></a>

<table>
  <thead>
    <tr>
      <th style="text-align:left"><b>S.No.</b>
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
      <td style="text-align:left">Faecal Sludge Management (FSM)</td>
      <td style="text-align:left">
        <p><b>Citizen</b>
        </p>
        <ul>
          <li>Apply for Emptying of Septic Tank / Pit</li>
          <li>My Applications and View Applications</li>
          <li>Make Online Payment for Emptying of Septic Tank / Pit Charges</li>
          <li>Download Application PDF and Receipt</li>
          <li>Rating the service</li>
        </ul>
        <p><b>Employee</b>
        </p>
        <ul>
          <li>Create a new Emptying of Septic Tank / Pit Application</li>
          <li>Search and View Applications</li>
          <li>Download Application PDF and Receipt</li>
          <li>Inbox</li>
          <li>Update Application/Demand</li>
          <li>Collect Payment</li>
          <li>Assign DSO</li>
          <li>Reassign DSO</li>
          <li>Complete Request on behalf of DSO</li>
        </ul>
        <p><b>Desludging operator</b>
        </p>
        <ul>
          <li>DSO Login</li>
          <li>Assign Vehicle</li>
          <li>Complete Request</li>
          <li>Decline Request</li>
          <li>Search and View Applications</li>
          <li>Inbox</li>
        </ul>
        <p><b>FSTP Operator</b>
        </p>
        <ul>
          <li>Inbox</li>
          <li>Update vehicle log</li>
        </ul>
        <p><b>Backend APIs</b>
        </p>
        <ul>
          <li>Create and Search Vendor/Desludging operator</li>
          <li>Create and Search Vehicle</li>
          <li>Create and Search Billing Slabs</li>
        </ul>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">2</td>
      <td style="text-align:left">Bill Amendment</td>
      <td style="text-align:left">
        <ul>
          <li>Application initiation</li>
          <li>Workflow-based application process</li>
          <li>Reference implementation for Water and Sewerage</li>
          <li>Artefacts
            <ul>
              <li>Credit/ Debit note PDF</li>
              <li>Application Acknowledgement</li>
            </ul>
          </li>
        </ul>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">3</td>
      <td style="text-align:left">HRMS Reports</td>
      <td style="text-align:left">Employee Report</td>
    </tr>
  </tbody>
</table>

### Enhancements <a id="Enhancements"></a>

| **S.No.** | **Updated Feature** | **Description** |
| :--- | :--- | :--- |
| 1 | HRMS Enhancements | Multi-Tenancy support while creating Employee |
| 2 | PGR Reports | Support for PGR v2 |
| 3 | Non-functional | Few of the Security fixes |

### ‌Document Resources and Links <a id="&#x200C;Document-Resources-and-Links"></a>

#### UI Technical Documents

{% file src=".gitbook/assets/bill-amendment.pdf" caption="Bill Amendment" %}

{% file src=".gitbook/assets/bill-amendment-apply.pdf" caption="Bill Amendment Apply" %}

{% file src=".gitbook/assets/create-employee.pdf" caption="Create Employee" %}

{% file src=".gitbook/assets/apply-water-sewerage.pdf" caption="Apply Water & Sewerage" %}

{% file src=".gitbook/assets/digit-ui-manual-r2.pdf" caption="DIGIT UI Manual" %}

{% file src=".gitbook/assets/digit-ui-implementation.pdf" caption="DIGIT UI Implementation" %}

{% file src=".gitbook/assets/fsm-ui-implementation.pdf" caption="FSM UI Implementation" %}

{% file src=".gitbook/assets/pgr-ui-implementation.pdf" caption="PGR UI Implementation" %}

#### Backend Service Documents

{% page-ref page="modules/services-overview/business-services/bill-amendment.md" %}





