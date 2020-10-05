# Trade Type

## Introduction <a id="Introduction"></a>

Once the [Trade Categories](https://digit-discuss.atlassian.net/wiki/spaces/DO/pages/450887718/Trade+Category) are defined, the next task is to -

* Define Trade Types
*  Map Trade Category to listed Trade Types

The Trade Type can be defined as the next \(2nd\) level classification of Trade. There can be multiple trade types and the list may vary from one State/ULB to another.

## Data Table <a id="Data-Table"></a>

| Sr. No. | Trade Type Code\* | Trade Type Name\* \(In English\) | Trade Type Name\* \(In Local Language\) | Trade Category Code\* |
| :--- | :--- | :--- | :--- | :--- |
| 1 | TRADE\_TYPE\_MEDICAL | Hospital | अस्पताल | TC1 |
| 2 | TRADE\_TYPE\_HOTEL | Hotels | होटल | TC2 |

Note: The table above contains sample Trade Type data.

## Procedure <a id="Procedure"></a>

### Data Definition <a id="Data-Definition"></a>

| Sr. No. | Column Name | Data Type | Data Size | Is Mandatory? | Description |
| :--- | :--- | :--- | :--- | :--- | :--- |
| 1 | Trade Type Code | Alphanumeric | 64 | Yes | The Code assigned to the Trade Type. Eg: TRADE\_TYPE\_MEDICAL is assigned to Hospitals |
| 3 | Trade Type Name \(In English\) | Text | 256  | Yes | Name of the Trade Type in English. Eg: Goods, Services etc. |
| 3 | Trade Type Name \(In Local Language\) | Text | 256  | Yes | Name of the Trade Type in Local Language \(as decided\). Eg: Service is described as “सर्विस” in Hindi |
| 4 | Trade Category Code | Reference |  64 | Yes | The Code assigned to the [Trade Category.](https://digit-discuss.atlassian.net/wiki/spaces/DO/pages/450887718/Trade+Category) Eg: TC1 For Goods, TC2 for Services |

### Steps to fill data <a id="Steps-to-fill-data"></a>

1. Download the data template attached to this page.
2. Refer to the ‘Data Definition’ section of this document to learn more about the template sheet, data type, size, and definitions.
3. Select the relevant Trade Category Code from the available drop-down list of Trade Category. This will map the listed Trade Type to the corresponding Trade Category.
4. Enter a unique Trade Type Code to identify the type of trade.
5. Enter a Trade Type Name \(In English\).
6. Enter the Trade Type Name \(In Local Language\).

## Checklist <a id="Checklist"></a>

The checklist contains a set of activities to be performed once the data is filled into a template to ensure data entry requirements are met. These activities have been divided into 2 groups as given below.

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
      <td style="text-align:left">The format of the Trade Type Code defined should be alphanumeric and unique</td>
      <td
      style="text-align:left">
        <p>TRADE_TYPE_MEDICAL</p>
        <p>TRADE_TYPE_HOTELS</p>
        </td>
    </tr>
    <tr>
      <td style="text-align:left">2</td>
      <td style="text-align:left">Trade Type Name (in either language) should not contain any special characters</td>
      <td
      style="text-align:left">
        <p>Hospital: [Allowed]</p>
        <p>#Hospital! : [Not allowed]</p>
        </td>
    </tr>
  </tbody>
</table>

## Attachments <a id="Attachments"></a>

Configurable Data Template -Trade License Type

\(Refer to “Trade Type” tab in the attached file\)

Sample Configurable Data- Trade License Type  


