# Trade License Documents Attachment

### Introduction <a id="Introduction"></a>

Along with the [rates](https://digit-discuss.atlassian.net/wiki/spaces/DO/pages/409141313/Trade+License+Fee), the Trade License application process does require certain documents as an attachment of proof. The proof can be defined by a set of documents ranging from

* Identification Proof \(Drivers License/ Voter Card/ Adhaar/ Pan etc.\)
* Trade Premises Proof \(Lease Agreement, Electricity Bills, etc\).
* Misc Documents \(Affidavit, Self- Declaration, etc\).

The Number and the Documents required could vary across the State, ULB\(s\), and might be dependent on Trade Subtypes, all of which are totally configurable on DIGIT.

### Data Table <a id="Data-Table"></a>

| Sr. No. | \*Trade Subtype Code | \*Trade Subtype Name \(In English\) | \*Application Type | \*Document 1 | \*Document 2 |
| :--- | :--- | :--- | :--- | :--- | :--- |
| 1 | TRADE\_SMALL\_BAKERY | Small Bakery | New | PAN/VOTER ID | LAND LEASE |
| 2 | TRADE\_SMALL\_BAKERY | Small Bakery | Renewal | PAN/VOTER ID | ELEC BILL |

\(Note: The Rows in the above table consists of Sample Data\)

## Procedure <a id="Procedure"></a>

| Sr. No. | Column Name | Data Type | Data Size | Is Mandatory? | Description |
| :--- | :--- | :--- | :--- | :--- | :--- |
| 1 | Trade Sub Type Code | Reference | 64 | Yes | The Code assigned to the [Trade Sub Type.](https://digit-discuss.atlassian.net/wiki/spaces/DO/pages/451346455/Trade+Sub+type) Eg: TRADE\_SMALL\_BAKERY is assigned to Bakery |
| 2 | Trade Sub Type Name \(English\) | Text | 256  | Yes | Name of the Trade Sub Type in English. Eg: Clinic |
| 3 | Application Type | Text | 256  | Yes | Type of application for which the documents related to trade are configured. It can either be new or renewal |
| 4 | Document 1 | Reference | 256 | Yes | The primary document required as a verification parameter. It refers to[ Standard Document List](https://digit-discuss.atlassian.net/wiki/spaces/DO/pages/502334137/Standard+Document+List) |
| 5 | Document 2 | Reference | 256 | Yes | The Secondary Document Required as a verification parameter. It refers to[ Standard Document List](https://digit-discuss.atlassian.net/wiki/spaces/DO/pages/502334137/Standard+Document+List) |

### How to fill data <a id="How-to-fill-data"></a>

1. Download the data template attached to this page.
2. Get a good understanding of all the headers in the template sheet, their data type, size, and definitions by referring to the ‘Data Definition’ section of this document.
3. In case of any doubt, please reach out to the person who has shared this template with you to discuss and clear your doubts.
4. Identify the “[Trade Sub Types](https://digit-discuss.atlassian.net/wiki/spaces/DO/pages/edit-v2/451346455)” that exists at a ULB/ State level.
5. Collect the above information and feed it below the “Trade Sub Type Name” column accordingly. The Description of Trade Sub Type Name must be provided as per the language specified in the respective column.
6. Add the “Trade Sub Type Code” respectively against the identified trade type\(s\).
7. Fill in the \*Document 1 & \*Document 2 columns respectively.  

## Checklist <a id="Checklist"></a>

The checklist is a set of activities to be performed one the data is filled into a template to ensure data type, size, and format of data is as per the expectation. These activities have been divided into 2 groups as given below.

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
      <td style="text-align:left">Trade Sub Type Name (In either Language) should not contain any special
        characters</td>
      <td style="text-align:left">
        <p>Small Bakery: [Allowed]</p>
        <p>#Small_Bakery! : [Not allowed]</p>
      </td>
    </tr>
  </tbody>
</table>

## Attachments <a id="Attachments"></a>

1. Configurable Data Template -Trade Documents

 \(Refer to “Trade Documents” tab in the attached file\)

 2. Sample Configurable Data- Trade Documents

