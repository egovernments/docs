# Structure Sub Type

## Introduction <a id="Introduction"></a>

Structure sub type is the second level of classification of the premises where the trade has to be established and conducted. This is mostly used as management information in the trade detail.

## Data Table <a id="Data-Table"></a>

| Sr. No. | Code\* | Structure Sub Type\* \(In English\) | Structure Sub Type\* \(In Local Language\) | Structure Type Code\* |
| :--- | :--- | :--- | :--- | :--- |
| 1 | PUCCA | Pucca | पक्का | IMMOVABLE |
| 2 | KUTCHA | Kutcha | कच्चा | IMMOVABLE |
| 3 | HDV | Hand Driven Vehicle | हाथ चालित वाहन | MOVABLE |
| 4 | MDV | Motor-Driven Vehicle | मोटर चालित वाहन | MOVABLE |

Note: Data given in the table is a sample data.

## Procedure <a id="Procedure"></a>

### Data Definition <a id="Data-Definition"></a>

| Sr. No. | Column Name | Data Type | Data Size | Is Mandatory? | Definition/ Description |
| :--- | :--- | :--- | :--- | :--- | :--- |
| 1 | Code | Alphanumeric | 64 | Yes | Unique code to identify each and every record uniquely |
| 2 | Structure Sub Type\* \(In English\) | Text | 256 | Yes | Structure sub type in English |
| 3 | Structure Sub Type\* \(In Local Language\) | Text | 256 | Yes | Structure sub type in local language e.g. in Hindi, Telugu etc. |
| 4 | Structure Type Code\* | Reference | 64 | Yes | Unique code of structure type to establish the mapping with[ Structure Type](https://digit-discuss.atlassian.net/wiki/spaces/DO/pages/599261450/Structure+Type) |

###  Steps to fill data <a id="[hardBreak]Steps-to-fill-data"></a>

1. Download the data template attached to this page.
2. Refer to the ‘Data Definition’ section of this document for more details on data type, size, and definitions.
3. Contact the person who shared this template with you to discuss and clear your doubts.
4. Enter the relevant structure sub types with its proper mapping with structure type.
5. Verify the data once again by going through the checklist and making sure that each and every point mentioned in the checklist is covered.

## Checklist <a id="Checklist"></a>

The checklist is a set of activities to be performed once the data is filled into a template to ensure data type, size, and format of data is as per specifications. These activities have been divided into 2 groups as given below.

### Common Checklist <a id="Common-Checklist"></a>

This checklist covers all the activities which are common across the entities.

| Sr. No. | Checklist Parameter | Example |
| :--- | :--- | :--- |
| 1 | Make sure that each and every point in this reference list has been taken care of. | [Checklist](https://digit-discuss.atlassian.net/wiki/spaces/DO/pages/502203140/Checklist) |

### Entity Specific Checklist <a id="Entity-Specific-Checklist"></a>

The separate entity-specific checklist is not needed for this entity data template.

## Attachments <a id="Attachments"></a>

1. Configuration data template - Structure sub type

    2. Sample configuration data - Structure sub type

