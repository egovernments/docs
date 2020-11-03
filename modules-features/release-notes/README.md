---
description: 'New release features, enhancements, and fixes'
---

# Release Notes DIGIT 2.1

### Release Summary

DIGIT 2.1 is a release that has got a few functional changes and few non-functional standardization changes.

* Functional: Introducing Water and Sewerage edit connection and Connection holder feature, DSS enhancements, Edit \(send back to Citizen\) property enhancements, and PGR APIs redesign along with workflow integration and reports.
* Non-functional: Baselining Actions, Role action mapping, and English Localization data.

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
      <td style="text-align:left">Water and Sewerage edit connection and Connection holder feature</td>
      <td
      style="text-align:left">
        <p></p>
        <ul>
          <li>Edit existing water or sewerage connection information using a workflow
            approval process.</li>
          <li>Associate a non-owner (connection holder) of the property to any connection.</li>
        </ul>
        </td>
    </tr>
    <tr>
      <td style="text-align:left">PGR API Contracts and APIs redesign</td>
      <td style="text-align:left">
        <p></p>
        <ul>
          <li>PGR APIs redesign along with workflow integration.</li>
          <li>New reports
            <ul>
              <li>ULB Report</li>
              <li>Description Report</li>
              <li>LME Performance Report</li>
              <li>GRO Performance Report</li>
            </ul>
          </li>
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
      <td style="text-align:left">DSS v1.2 Enhancements</td>
      <td style="text-align:left">
        <ul>
          <li>Graphs</li>
          <li>Pie Charts</li>
          <li>Typography</li>
          <li>Time Filter</li>
          <li>Comparison Indicators in Tables</li>
          <li>Breadcrumbs</li>
          <li>Event Duration Graphs</li>
          <li>Drilldown and Drillthroughs</li>
        </ul>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">Property Enhancements</td>
      <td style="text-align:left">
        <ul>
          <li>Edit (Send Back to citizen) in Property Create, Update, and Mutation workflow</li>
          <li>Workflow configuration to support Data Entry and Data migration in Property
            Service</li>
          <li>Payer information on citizen side in open payments</li>
        </ul>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">UI and backend Enhancements</td>
      <td style="text-align:left">
        <ul>
          <li>Searcher Ignore case for user input fields</li>
          <li>DOB range Validation in HRMS and Trade License</li>
          <li>Create a user for an unregistered mobile number as part of the Billing
            service</li>
          <li>Added Deserialization Error Handler in Persister</li>
          <li>Localization caching in the application (module wise - within the module)</li>
          <li>Addition of spinner in all PT, TL, and Common pay screens</li>
        </ul>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">Non-functional enhancements</td>
      <td style="text-align:left">
        <ul>
          <li>Actions and Roleaction mapping - Product baseline</li>
          <li>Baseline English Localisation data</li>
          <li>Readme and Localsetup documentations for all the services</li>
          <li>Technical Enablement and other Tech documentations</li>
        </ul>
      </td>
    </tr>
  </tbody>
</table>

### Document Resources and Links

<table>
  <thead>
    <tr>
      <th style="text-align:left"><b>UI Technical Documents</b>
      </th>
      <th style="text-align:left"><b>Backend Service Documents</b>
      </th>
      <th style="text-align:left"><b>Infra/Deployment Documents</b>
      </th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td style="text-align:left">
        <ul>
          <li><a href="https://digit-discuss.atlassian.net/wiki/spaces/EPE/pages/772178266/DSS++Features+Enhancements+V2+Technical+Document+for+UI">DSS Features Enhancements V2 Technical Document for UI</a>
          </li>
          <li><a href="https://digit-discuss.atlassian.net/wiki/spaces/EGR/pages/408485900/Search+Property+Tax">Search Property Tax</a>
          </li>
          <li><a href="https://digit-discuss.atlassian.net/wiki/spaces/EGR/pages/408945038/View+Property+Details%2C+Transfer+Ownership+and+View+History">View Property Details, Transfer Ownership and View History</a>
          </li>
          <li><a href="https://digit-discuss.atlassian.net/wiki/spaces/EGR/pages/408945299/Property+and+Mutation+Workflow">Property and Mutation Workflow</a>
          </li>
          <li><a href="https://digit-discuss.atlassian.net/wiki/spaces/EGR/pages/441450614/Property+Tax+-+Add+New+Property">Property Tax - Add New Property</a>
          </li>
          <li><a href="https://digit-discuss.atlassian.net/wiki/spaces/EGR/pages/443351062/Property+-+Update+Existing+Property">Property - Update Existing Property</a>
          </li>
          <li><a href="https://digit-discuss.atlassian.net/wiki/spaces/EGR/pages/443744285/Property+-+Transfer+of+Ownership">Property - Transfer of Ownership</a>
          </li>
          <li><a href="https://digit-discuss.atlassian.net/wiki/spaces/EGR/pages/554992509/Connection+Holder+Details">Connection Holder Details</a>
          </li>
          <li><a href="https://digit-discuss.atlassian.net/wiki/spaces/EGR/pages/561348711/Edit+Connection+Flow">Edit Connection Flow</a>
          </li>
        </ul>
      </td>
      <td style="text-align:left">
        <ul>
          <li><a href="https://digit-discuss.atlassian.net/wiki/spaces/EPE/pages/328925216/Water+Service+-+Technical+Document?atlOrigin=eyJpIjoiNDM4Yjc3MmJmNDBiNDViZGEwZjJmYTg2MzVhNDdkOTgiLCJwIjoiYyJ9">Water Service - Technical Document</a>
          </li>
          <li><a href="https://digit-discuss.atlassian.net/l/c/PM2Ho3A1">Sewerage Service - Technical Document</a>
          </li>
          <li><a href="https://digit-discuss.atlassian.net/l/c/p3MGjvPw">Water Calculator Service - Technical Document</a>
          </li>
          <li><a href="https://digit-discuss.atlassian.net/l/c/o0gRiR1n">Sewerage Calculator Service - Technical Document</a>
          </li>
          <li><a href="https://digit-discuss.atlassian.net/wiki/spaces/EPE/pages/566984722/W+S+Promotion+Document+v2.2?atlOrigin=eyJpIjoiZThlMzRkNDUxNjcyNGJhZmEyMmMxODhkYzJjMGU4YTMiLCJwIjoiYyJ9">W&amp;S Promotion Document v2.2</a>
          </li>
          <li><a href="https://digit-discuss.atlassian.net/wiki/spaces/EPE/pages/117244081/DSS+Backend+Configuration+Manual">DSS Backend Configuration Manual</a>
          </li>
          <li><a href="https://digit-discuss.atlassian.net/wiki/spaces/EPE/pages/222494721/Property+Registry+Migration">Property Registry Migration</a>
          </li>
          <li><a href="https://digit-discuss.atlassian.net/wiki/spaces/EPE/pages/313360447/Chatbot-service">Chatbot-service</a>
          </li>
          <li><a href="https://digit-discuss.atlassian.net/wiki/spaces/EPE/pages/579436651/Promotion+Doc+whatsapp-PGR+chatbot">Promotion Doc whatsapp-PGR chatbot</a>
          </li>
          <li><a href="https://digit-discuss.atlassian.net/wiki/spaces/EPE/pages/638550096/Kafka-connect+commands+for+DSS+and+Collection+live+indexing">Kafka-connect commands for DSS and Collection live indexing</a>
          </li>
          <li><a href="https://digit-discuss.atlassian.net/l/c/XEWFAfnS">NOC Promotion Document</a>
          </li>
        </ul>
      </td>
      <td style="text-align:left">
        <ul>
          <li><a href="https://digit-discuss.atlassian.net/wiki/spaces/DD/pages/723189807">MDMS (Master Data Management Service)</a>
          </li>
          <li><a href="https://digit-discuss.atlassian.net/wiki/spaces/DD/pages/644546619/Setting+Up+Workflows">Setting Up Workflows</a>
          </li>
          <li><a href="https://digit-discuss.atlassian.net/wiki/spaces/DD/pages/644481051">Configuring Workflows For New Product/Entity</a>
          </li>
          <li><a href="https://digit-discuss.atlassian.net/wiki/spaces/DD/pages/717979679/PDF+Generation+Service">PDF Generation Service</a>
          </li>
          <li><a href="https://digit-discuss.atlassian.net/wiki/spaces/DD/pages/720306189">Customizing PDF Receipts &amp; Certificates</a>
          </li>
          <li><a href="https://digit-discuss.atlassian.net/wiki/spaces/DD/pages/720470017/Integration+of+PDF+in+UI+for+download+and+print+PDF">Integration of PDF in UI for download and print PDF</a>
          </li>
          <li><a href="https://digit-discuss.atlassian.net/wiki/spaces/DD/pages/686719019/API+Do+s+and+Don+ts">API Do&apos;s and Don&apos;ts</a>
          </li>
          <li><a href="https://digit-discuss.atlassian.net/wiki/spaces/DD/pages/751140901/Writing+a+new+Consumer">Writing a new Consumer</a>
          </li>
          <li><a href="https://digit-discuss.atlassian.net/wiki/spaces/DD/pages/664174657/Workflow+Service">Workflow Service</a>
          </li>
          <li><a href="https://digit-discuss.atlassian.net/wiki/spaces/DD/pages/669450371/User+Service">User Service</a>
          </li>
          <li><a href="https://digit-discuss.atlassian.net/wiki/spaces/DD/pages/695664711/Access+Control+Service">Access Control Service</a>
          </li>
          <li><a href="https://digit-discuss.atlassian.net/wiki/spaces/DD/pages/745701377/Payment+Gateway+Service">Payment Gateway Service</a>
          </li>
          <li><a href="https://digit-discuss.atlassian.net/wiki/spaces/DD/pages/664338482/Location+Service">Location Service</a>
          </li>
          <li><a href="https://digit-discuss.atlassian.net/wiki/spaces/DD/pages/669614102/Trade-License+Service">Trade License Service</a>
          </li>
          <li><a href="https://digit-discuss.atlassian.net/wiki/spaces/DD/pages/684392464/pgr-services">PGR Services v2.0</a>
          </li>
          <li><a href="https://digit-discuss.atlassian.net/l/c/stF7suXA">BPA Service</a>
          </li>
          <li><a href="https://digit-discuss.atlassian.net/l/c/Mj6mhaXL">Noc Services</a>
          </li>
        </ul>
      </td>
    </tr>
  </tbody>
</table>

