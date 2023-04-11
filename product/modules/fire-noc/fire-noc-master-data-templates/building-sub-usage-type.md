# Building Sub Usage Type

## Introduction <a href="#introduction" id="introduction"></a>

After the building usage types are identified, the next activity is to identify the building sub usage types.

Buildings types can be further classified into various subcategories to go into the granular level of their usage details. The National Building Code of India (NBC) also classifies the building's usage type into the sub usage types which can be seen in the attachment.

## Data Table <a href="#data-table" id="data-table"></a>

| Sr. No. | \*Building Usage Type Code | \*Sub Type Code | \*Building Sub Usage Type | \*Sub Divison (as per NBC) | \*Building Sub Usage Type (as per NBC) |
| ------- | -------------------------- | --------------- | ------------------------- | -------------------------- | -------------------------------------- |
| 1       | BU01                       | BSU01           | Hotel                     | A4                         | Hotel                                  |
| 2       | BU01                       | BSU02           | Apartment                 | A5                         | Apartment House                        |

The data given in the above table is sample data.

## Procedure <a href="#procedure" id="procedure"></a>

### Data Definitions <a href="#data-definitions" id="data-definitions"></a>

| Sr. No. | Column Name                          | Data Type  | Data Size | Mandatory | Description                                                                                                           |
| ------- | ------------------------------------ | ---------- | --------- | --------- | --------------------------------------------------------------------------------------------------------------------- |
| 1       | Building Usage Type Code             | Reference  | 64        | Yes       | The codes are given to the building usage type in the [building usage type master](building-usage-type.md)​           |
| 2       | Sub Type Code                        | Alphameric | 64        | Yes       | The code is given to the building sub usage type by the Fire Station. Eg: BSU01 for Hotel, BSU02 for Apartment Houses |
| 3       | Building Sub Usage Type              | Text       | 256       | Yes       | Name of subcategories within each building usage type as per the fire station. Eg: Hotel, Apartment Houses            |
| 4       | Sub Divison (as per NBC)             | Alphameric | 64        | Yes       | The code is given to the building sub usage type as per NBC. Eg: Subdivision A4, A5                                   |
| 5       | Building Sub Usage Type (as per NBC) | Text       | 256       | Yes       | Name of subcategories within each building usage type as per NBC. Eg: Hotel, Apartment House                          |

### How to fill data <a href="#how-to-fill-data" id="how-to-fill-data"></a>

1. Download the data template attached to this page.
2. Get a good understanding of all the headers in the template sheet, their data type, size, and definitions by referring to the ‘Data Definition’ section of this document.
3. In case of any doubt, please reach out to the person who has shared this template with you to discuss and clear your doubts.
4. Identify and add all the different sub usage types for each building group that are being catered by the fire station in the Building Sub Usage Type column.
5. Next, give each building Sub Usage type a unique code and enter the code in the Sub Usage Type Code column, next to the Building Sub Usage type.
6. Map the data filled in the building sub usage type column to the building sub usage type and Subdivision as per the national building code.
7. Record the appropriate subdivision and building sub usage type from NBC in the Subdivision (as per NBC) and Building Sub Usage Type (as per NBC) respectively.
8. Verify the data once again by going through the checklist and making sure that each and every point mentioned in the checklist is covered.

## Checklist <a href="#checklist" id="checklist"></a>

The checklist is a set of activities to be performed once the data is filled into a template to ensure data type, size, and format of data is as per the expectation. These activities have been divided into 2 groups as given below.

### Common Checklist <a href="#common-checklist" id="common-checklist"></a>

This checklist covers all the activities which are common across the entities.

| Sr. No. | Checklist Parameter                                                               | Example                                                                                                                      |
| ------- | --------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------- |
| 1       | Make sure that each and every point in this reference list has been taken care of | ​[Checklist](https://docs.digit.org/configure-digit/configuring-master-data-templates/module-setup/common-config/checklist)​ |

### Entity Specific Checklist <a href="#entity-specific-checklist" id="entity-specific-checklist"></a>

This checklist covers the activities which are specific to the entity.

| Sr. No. | Checklist Parameter                                                                                                            | Example                                                |
| ------- | ------------------------------------------------------------------------------------------------------------------------------ | ------------------------------------------------------ |
| 1       | The Building Usage Type Code should be similar to the ones defined in the [building usage type master](building-usage-type.md) | <p>BU01: Residential</p><p>BU02: Educational</p>       |
| 2       | Building Sub Usage Type Codes that are defined by the Fire Station should be alphanumeric and unique                           | <p>BSU01: Hotel</p><p>BSU02: Apartment</p>             |
| 3       | Building Sub Usage Type should not contain any special characters                                                              | <p>Hotel : [Allowed]</p><p>#Hotel! : [Not allowed]</p> |

## Attachments <a href="#attachments" id="attachments"></a>

[Configuration Data Templateconfiguration-data-template-building-sub-usage-type.xlsx - 9KB](https://firebasestorage.googleapis.com/v0/b/gitbook-28427.appspot.com/o/assets%2F-MERG\_iQW5oN4ukgXP8K%2Fsync%2F97afee0e22e6fafc7c707075ff235a7a4385b57b.xlsx?generation=1602050608459482\&alt=media)

[Sample Datasample-configuration-data-building-sub-usage-type.xlsx - 8KB](https://firebasestorage.googleapis.com/v0/b/gitbook-28427.appspot.com/o/assets%2F-MERG\_iQW5oN4ukgXP8K%2Fsync%2Ffbbaabc0c9c40b491b41903c96ddb520c5eeef84.xlsx?generation=1602050608348444\&alt=media)

[NBC Classificationnbc-building-sub-usage-type.xlsx - 11KB](https://firebasestorage.googleapis.com/v0/b/gitbook-28427.appspot.com/o/assets%2F-MERG\_iQW5oN4ukgXP8K%2Fsync%2Fe84a9b3e51ae8419e39c714cda68726f5bc45121.xlsx?generation=1602050608421311\&alt=media)

[![Creative Commons License](https://i.creativecommons.org/l/by/4.0/80x15.png)](http://creativecommons.org/licenses/by/4.0/)All content on this page by [eGov Foundation ](https://egov.org.in/)is licensed under a [Creative Commons Attribution 4.0 International License](http://creativecommons.org/licenses/by/4.0/).
