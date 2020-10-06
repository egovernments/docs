# Fire NOC Fee

## Introduction <a id="Introduction"></a>

After the building usage and sub usage ontology has been defined for all the Firestations, the next step is to collect the Fire NOC fee that the citizens have to pay to obtain the certificate.

The Fire NOC fee is dependent on the following parameters:

1. Fire Station
2. Building Usage type
3. Building Sub usage type
4. Fire NOC type

## Data Table <a id="Data-Table"></a>

| Sr. No. | \*Fire Station Code | \*Building Usage Type Code | \*Sub Type Code | \*Fire NOC Fee |  |  |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| New | Provisional | Renew |  |  |  |  |
| 1 | FS01 |  BU01 | BSU01 | 1000 | 200 | 800 |
| 2 | FS02 |  BU01 | BSU02 | 2000 | 1000 | 2000 |

## Procedure <a id="Procedure"></a>

### Data Definitions <a id="Data-Definitions"></a>

| Sr. No. | Column Name | Data Type | Data Size | Mandatory | Description |
| :--- | :--- | :--- | :--- | :--- | :--- |
| 1 | Fire Station Code | Reference | 64 | Yes | The code given to each Fire station in the [Fire Station masters](https://digit-discuss.atlassian.net/wiki/spaces/DO/pages/414089217/Fire+Station+Master) |
| 2 | Building Usage Code | Reference | 64 | Yes | The code given to each Fire station in the [Fire Usage Type Master](https://digit-discuss.atlassian.net/wiki/spaces/DO/pages/422412337/Building+Usage+Type) |
| 3 | Building Sub Usage Code | Reference | 64 | Yes | The code given to each Fire station in the [Fire Sub Usage Type Master](https://digit-discuss.atlassian.net/wiki/spaces/DO/pages/408946786/Building+Sub+Usage+Type) |
| 4 | Fire NOC Fee | Integer | 6 | Yes | The amount that will be charged for each Fire NOC type. For Eg: 2000 for new, 0 for Provisional and 1000 for renew |

### How to fill data <a id="How-to-fill-data"></a>

1. Download the data template attached to this page.
2. Get a good understanding of all the headers in the template sheet, their data type, size, and definitions by referring to the ‘Data Definition’ section of this document.
3. In case of any doubt, please reach out to the person who has shared this template with you to discuss and clear your doubts.
4. Enter the Fire station codes of all the fire stations that are there in the Fire Station master, in the ‘Fire Station Code Column’.
5. Next, enter the Building usage types codes and building sub usage type codes that being catered by the fire station, next to the Fire Station Code.
6. Identify the fees that the fire stations are charging to issuing a new, provisional, or renewed Fire NOC for every building usage and sub usage combination.
7. Verify the data once again by going through the checklist and making sure that each and every point mentioned in the checklist is covered.

### Common Checklist <a id="Common-Checklist"></a>

This checklist covers all the activities which are common across the entities.

| Sr. No. | Checklist Parameter | Example |
| :--- | :--- | :--- |
| 1 | Make sure that each and every point in this reference list has been taken care of | [Checklist](https://digit-discuss.atlassian.net/wiki/spaces/DO/pages/502203140/Checklist) |

### Entity Specific Checklist <a id="Entity-Specific-Checklist"></a>

This checklist covers the activities which are specific to the entity.

<table>
  <thead>
    <tr>
      <th style="text-align:left">Sr. No.</th>
      <th style="text-align:left">Checklist Parameter</th>
      <th style="text-align:left">Example</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td style="text-align:left">1</td>
      <td style="text-align:left">Fire station codes, Building Usage code, and Sub usage Codes have to be
        similar to the codes entered in their respective masters</td>
      <td style="text-align:left">
        <ol>
          <li><a href="https://digit-discuss.atlassian.net/wiki/spaces/DO/pages/414089217/Fire+Station+Master">Fire Station Master</a>
          </li>
          <li><a href="https://digit-discuss.atlassian.net/wiki/spaces/DO/pages/422412337/Building+Usage+Type">Building Usage Type</a>
          </li>
          <li><a href="https://digit-discuss.atlassian.net/wiki/spaces/DO/pages/408946786/Building+Sub+Usage+Type">Building Sub Usage Type</a>
          </li>
        </ol>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">2</td>
      <td style="text-align:left">The Fire NOC fee should be an integer, without having any alphabet or
        symbol preceding or succeeding it</td>
      <td style="text-align:left">
        <p>2000: [Allowed]</p>
        <p>Rs. 2000 : [Not allowed]</p>
        <p>2000 Rs. : [Not allowed]</p>
      </td>
    </tr>
  </tbody>
</table>

### Attachments <a id="Attachments"></a>

1. Configuration data template - Fire NOC Fee
2. Sample configuration data - Fire NOC Fee

