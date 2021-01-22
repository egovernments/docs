---
description: 'New release features, enhancements, and fixes'
---

# Release Notes DIGIT 2.2

### Release Summary

DIGIT 2.2 is a release that has got a few functional changes and few non-functional standardization changes.

* Functional: PGR v2 \(Revamped UI/UX, Revamped APIs, and Workflow integration\), Water & Sewerage Enhancements \(Public Domain Search, Open Payments, and PT Workflow Config Changes\), Property Enhancements, Search/Cancel Receipts Screen, and Enhancements in HRMS.
* Non-functional: Config Repo baselining \(Indexer and Persister configs sem version and baselining\).

### New ‌Feature Additions

<table>
  <thead>
    <tr>
      <th style="text-align:left"><b>Feature</b>
      </th>
      <th style="text-align:left"><b>Description</b>
      </th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td style="text-align:left">PGR v2 (UI/UX/API revamp and Workflow integration)</td>
      <td style="text-align:left">
        <p><b>Citizen</b>
        </p>
        <ul>
          <li>Create a Complaint</li>
          <li>My Complaints and View Complaints</li>
          <li>Rating and Reopening of the Complaint</li>
        </ul>
        <p><b>CSR</b>
        </p>
        <ul>
          <li>Create a Complaint</li>
          <li>View Complaints</li>
          <li>Reopen Complaints</li>
          <li>Inbox</li>
        </ul>
        <p><b>Grievance Routing Officer</b>
        </p>
        <ul>
          <li>View Complaints</li>
          <li>Assign Complaints</li>
          <li>Reject Complaints</li>
          <li>Inbox</li>
        </ul>
        <p><b>Last Mile Employee</b>
        </p>
        <ul>
          <li>View Complaints</li>
          <li>Assign Complaints</li>
          <li>ReAssign Complaints</li>
          <li>Inbox</li>
        </ul>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">Water and Sewerage</td>
      <td style="text-align:left">
        <ul>
          <li>Public domain search for Water and Sewerage</li>
          <li>Open payment for Water and Sewerage</li>
        </ul>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">Collection</td>
      <td style="text-align:left">
        <ul>
          <li>Search Receipt</li>
          <li>Receipt cancellation and its impact</li>
        </ul>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">HRMS</td>
      <td style="text-align:left">
        <ul>
          <li>Deactivate and activate employee</li>
        </ul>
      </td>
    </tr>
  </tbody>
</table>

### Enhancements

<table>
  <thead>
    <tr>
      <th style="text-align:left"><b>Updated Feature</b>
      </th>
      <th style="text-align:left"><b>Description</b>
      </th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td style="text-align:left">Property Tax</td>
      <td style="text-align:left">
        <ul>
          <li>Payment Notification</li>
          <li>Payment Failure Scenario for Open payment</li>
          <li>Capturing data for better reporting and analysis</li>
          <li>Show the status of the receipt if the receipt is cancelled</li>
          <li>Mutation - Allow Guardian name to change</li>
          <li>Mutation - Multiple owners to single owner change and vice versa</li>
          <li>Tenant and date range wise re-indexing Utility</li>
        </ul>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">Water and Sewerage Enhancements</td>
      <td style="text-align:left">
        <ul>
          <li>Property Workflow Config Changes for Water and Sewerage</li>
        </ul>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">Collection Enhancements</td>
      <td style="text-align:left">
        <ul>
          <li>Tenant and date range wise re-indexing Utility</li>
          <li>Zero payment changes</li>
        </ul>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">HRMS Enhancements</td>
      <td style="text-align:left">
        <ul>
          <li>Employee Create and Search Enhancements</li>
          <li>Other minor enhancements and validations</li>
        </ul>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">UI and backend Enhancements</td>
      <td style="text-align:left">
        <ul>
          <li>Pagination on process instance search API</li>
          <li>Pagination in Employee Inbox</li>
          <li>Addition of spinners in all the UI screens</li>
          <li>DSS improvements to enable/disable module configs in MDMS and table headings
            Localization</li>
          <li>PGR migration from v1 to v2 including the workflow data and reindexing</li>
          <li>DSS config changes to support PGR v2</li>
          <li>SENDBACKTOCITIZEN send&#x2019;s application back to the user&#x2019;s
            with a registered Mobile Number</li>
        </ul>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">Non-functional enhancements</td>
      <td style="text-align:left">
        <ul>
          <li>Config Repo baselining (Indexer and Persister configs sem version and
            baselining)
            <ul>
              <li>Improvement in Loading localization data in UI - module wise localization
                caching</li>
            </ul>
          </li>
        </ul>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">eDCR Enhancements</td>
      <td style="text-align:left">
        <ul>
          <li>Road Reserve area captured</li>
          <li>Height of Room - The colour codes are used to identify the type of room</li>
          <li>Vehicle Ramp captured and slope auto calculated</li>
          <li>Floor Unit - Colour codes used to differentiate the different type of
            dwelling unit</li>
        </ul>
      </td>
    </tr>
  </tbody>
</table>

### Document Resources and Links

#### UI Technical Documents

{% file src="../../.gitbook/assets/dss-features-enhancements-v2-technical-document-for-ui.pdf" caption="DSS Feature Enhancements" %}

{% file src="../../.gitbook/assets/search-property-tax.pdf" caption="Search Property Tax" %}

{% file src="../../.gitbook/assets/view-property-details.pdf" caption="View Property Details" %}

{% file src="../../.gitbook/assets/property-and-mutation-workflow.pdf" caption="Property & Mutation Workflow" %}

{% file src="../../.gitbook/assets/property-tax.pdf" caption="Property Tax - Add New Property" %}

{% file src="../../.gitbook/assets/update-existing-property.pdf" caption="Update Existing Property" %}

{% file src="../../.gitbook/assets/transfer-ownership.pdf" caption="Transfer Of Ownership" %}

{% file src="../../.gitbook/assets/connection-holder-details.pdf" caption="Connection Holder" %}

{% file src="../../.gitbook/assets/edit-connection-flow.pdf" caption="Edit Connection Flow" %}

#### Backend Service Documents

{% file src="../../.gitbook/assets/water-service-technical-doc.pdf" caption="Water Service Technical Document" %}

{% file src="../../.gitbook/assets/sewerage-service.pdf" caption="Sewerage Service Technical Document" %}

{% file src="../../.gitbook/assets/water-calculator-service.pdf" caption="Water Calculator Service Technical Document" %}

{% file src="../../.gitbook/assets/sewerage-calculator-service.pdf" caption="Sewerage Calculator Service Technical Document" %}

{% file src="../../.gitbook/assets/w-and-s-promotion.pdf" caption="W&S Promotion Doc v2.2" %}

{% file src="../../.gitbook/assets/dss-backend-configuration-manual.pdf" caption="DSS Backend Configuration Manual" %}

{% file src="../../.gitbook/assets/property-registry-migration.pdf" caption="Property Registry Migration" %}

{% file src="../../.gitbook/assets/chatbot-service.pdf" caption="Chatbot Service" %}

{% file src="../../.gitbook/assets/promotion-doc-whatsapp.pdf" caption="Promotion Doc Whatsapp PGR Chatbot" %}

{% file src="../../.gitbook/assets/kafka.pdf" caption="Kafka-Connect Commands for DSS and Collection Live Indexing" %}

{% file src="../../.gitbook/assets/noc-promotion-document.pdf" caption="NOC Promotion Document" %}

#### Infra/Deployment Documents

* [MDMS \(Master Data Management Service\)](https://docs.digit.org/modules-features/technical-documentation/core-service/mdms-master-data-management-service)
* [Setting Up Workflows](https://app.gitbook.com/@egov-digit/s/home/install-digit/configuring-workflows/setting-up-workflow)
* [Configuring Workflows For New Product/Entity](https://app.gitbook.com/@egov-digit/s/home/v/v2.1/install-digit/configuring-workflows/configuring-workflow-for-an-entity)
* [PDF Generation Service](https://app.gitbook.com/@egov-digit/s/home/v/v2.1/modules-features/technical-documentation/core-service/pdf-generation-service)
* [Customizing PDF Receipts & Certificates](https://app.gitbook.com/@egov-digit/s/home/v/v2.1/install-digit/configuring-digit-services/customizing-pdf-notices-and-certificates/customizing-pdf-receipts-and-certificates)
* [Integration of PDF in UI for download and print PDF](https://app.gitbook.com/@egov-digit/s/home/v/v2.1/install-digit/configuring-digit-services/customizing-pdf-notices-and-certificates/integration-of-pdf-in-ui-for-download-and-print-pdf)
* [API Do's and Don'ts](https://app.gitbook.com/@egov-digit/s/home/v/v2.1/install-digit/configuring-digit-services/api-dos-and-donts)
* [Writing a new Consumer](https://app.gitbook.com/@egov-digit/s/home/v/v2.1/customizing-digit/digit-customization/writing-a-new-customer)
* [Workflow Service](https://app.gitbook.com/@egov-digit/s/home/v/v2.1/modules-features/technical-documentation/core-service/workflow-service)
* [User Service](../technical-documentation/core-service/user-service.md)
* [Access Control Service](https://app.gitbook.com/@egov-digit/s/home/v/v2.1/modules-features/technical-documentation/core-service/access-control-service)
* [Payment Gateway Service](https://app.gitbook.com/@egov-digit/s/home/v/v2.1/modules-features/technical-documentation/core-service/payment-gateway-service)
* [Location Service](https://app.gitbook.com/@egov-digit/s/home/v/v2.1/modules-features/technical-documentation/core-service/location-service)
* [Trade License Service](https://app.gitbook.com/@egov-digit/s/home/v/v2.1/modules-features/technical-documentation/municipal-service/trade-license-service)
* [PGR Services v2.0](https://app.gitbook.com/@egov-digit/s/home/v/v2.1/modules-features/technical-documentation/municipal-service/pgr-services)

{% file src="../../.gitbook/assets/bpa-service.pdf" caption="BPA Service" %}

{% file src="../../.gitbook/assets/noc-services.pdf" caption="NOC Services" %}

