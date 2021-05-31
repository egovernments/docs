---
description: 'New release features, enhancements, and fixes'
---

# Release Notes

### Release Summary <a id="Release-Summary"></a>

DIGIT 2.4 is a release that has got new modules, a few functional changes, and non-functional changes.

* Functional: eChallan module, WhatsApp Bill Payment, Property Tax Citizen flow UI/UX revamp Arrears Breakup in Property Tax Due, and Send back to Citizen feature in Fire NOC.
* Non-functional: Platform Security Audit fixes, Hindi Localization, QA Automaton of APIs, and Technical improvements.

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
      <td style="text-align:left">eChallan module</td>
      <td style="text-align:left">
        <p></p>
        <ol>
          <li>Generate <b>e-challans / bill</b> for all miscellaneous / Adhoc services
            which citizens avail from ULBs</li>
          <li>Edit/Cancel e-challan/bill</li>
          <li>The ability for ULBs to Notify citizens about the outstanding payments
            - Online(email &amp; SMS) and offline.</li>
          <li>Enable Digital payments for citizens - QR code, payment link in notifications,
            etc.</li>
        </ol>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">2</td>
      <td style="text-align:left">WhatsApp Bill Payment and PGR v2 integration with redesigned Chatbot (xState)</td>
      <td
      style="text-align:left">
        <p></p>
        <p><b>Bill Payment:</b>
        </p>
        <ol>
          <li><b>Search and View Bill `</b>
            <ol>
              <li>View my Bills</li>
              <li>Search Bills Based on
                <ol>
                  <li>Consumer Number</li>
                  <li>Application Number</li>
                  <li>Mobile Number etc</li>
                </ol>
              </li>
              <li>View Bill
                <ol>
                  <li>Amount Due</li>
                  <li>Bill copy (PDF)</li>
                </ol>
              </li>
            </ol>
          </li>
          <li><b>Payment </b>
            <ol>
              <li>Pay bills through quick payment links</li>
              <li>Payment confirmation/failure notification</li>
              <li>Payment receipt (PDF) on successful payment</li>
            </ol>
          </li>
          <li><b>Multi-Language Support</b>
            <ol>
              <li>Hindi Localization (For Chats)</li>
            </ol>
          </li>
        </ol>
        <p><b>PGR:</b>
        </p>
        <ol>
          <li>Geo-Location tagging</li>
          <li>Two steps complaint category and type</li>
          <li>Hindi Localization (For Chats)</li>
          <li>PGR v1 &amp; v2 support</li>
        </ol>
        </td>
    </tr>
    <tr>
      <td style="text-align:left">3</td>
      <td style="text-align:left">Property Tax Citizen flow UI/UX revamp</td>
      <td style="text-align:left">
        <p></p>
        <p>Updated workflows and user interface changes in the following business
          cases -</p>
        <ul>
          <li>PT - Quick Pay</li>
          <li>Create Property</li>
          <li>My Properties</li>
          <li>My Applications</li>
        </ul>
      </td>
    </tr>
  </tbody>
</table>

### Enhancements <a id="Enhancements"></a>

<table>
  <thead>
    <tr>
      <th style="text-align:left"><b>S.No.</b>
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
      <td style="text-align:left">Fire NOC Enhancements</td>
      <td style="text-align:left">Send back to Citizen in Fire NOC</td>
    </tr>
    <tr>
      <td style="text-align:left">2</td>
      <td style="text-align:left">Property Tax Enhancements</td>
      <td style="text-align:left">Arrears Breakup in Property Tax Due</td>
    </tr>
    <tr>
      <td style="text-align:left">3</td>
      <td style="text-align:left">Hindi Localization</td>
      <td style="text-align:left">Hindi Localization of all labels, messages, notifications, and MDMS drop-down
        data of all the modules</td>
    </tr>
    <tr>
      <td style="text-align:left">4</td>
      <td style="text-align:left">QA Automaton of APIs</td>
      <td style="text-align:left">
        <p></p>
        <p>APIs automation for</p>
        <ul>
          <li>Core Services</li>
          <li>Business Services</li>
          <li>Municipal Services
            <ul>
              <li>End to End APIs automation for Property Tax, Trade License, mCollect,
                Water &amp; Sewerage, Fire NOC, Building Plan Approval, FSM, and PGR.</li>
            </ul>
          </li>
          <li>Here is the <a href="bill-amendment-release-notes.md">document </a>with
            the details of services automated and README documentation which details
            the detailed steps to execute the automation</li>
        </ul>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">5</td>
      <td style="text-align:left">Platform Security Audit fixes</td>
      <td style="text-align:left">
        <p></p>
        <p><b>Backend Audit </b>
        </p>
        <ul>
          <li>Sensitive Information in URL</li>
          <li>Standard pseudo-random number generators cannot withstand cryptographic
            attacks</li>
          <li>Improper Neutralization of CRLF Sequences in HTTP Headers (&apos;HTTP
            Response Splitting&apos;)</li>
          <li>Avoid Exception, Runtime Exception or Throwable in the catch or Throw
            Statements</li>
          <li>Avoid sensitive information exposure through error messages</li>
          <li>Size Validations</li>
        </ul>
        <p><b>Frontend Audit</b>
        </p>
        <ul>
          <li>Insecure Direct Object References (IDOR)</li>
          <li>Sensitive Information in URL</li>
          <li>Clickjacking</li>
          <li>It was observed that the application uses eval(code).</li>
          <li>Do not use dangerouslySetInnerHTML property in React components</li>
          <li>Do not release debuggable apps
            <ul>
              <li>Avoid post cross-document messages with an overly permissive target origin</li>
            </ul>
          </li>
        </ul>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">6</td>
      <td style="text-align:left">Technical Improvements</td>
      <td style="text-align:left">
        <p></p>
        <ul>
          <li>PDF service refactoring for Localization API calls optimization</li>
          <li>Timezone configuration support for all the services</li>
          <li>Standard product Workflow bundling as part of the product</li>
        </ul>
      </td>
    </tr>
  </tbody>
</table>

### ‌Document Resources and Links <a id="&#x200C;Document-Resources-and-Links"></a>

#### UI Technical Documents



#### Backend Service Documents



#### Tech Enablement Documents





 [![Creative Commons License](https://i.creativecommons.org/l/by/4.0/80x15.png)](http://creativecommons.org/licenses/by/4.0/)All content on this page by [eGov Foundation ](https://egov.org.in/)is licensed under a [Creative Commons Attribution 4.0 International License](http://creativecommons.org/licenses/by/4.0/).

