# Building Usage Type

## Introduction <a href="#introduction" id="introduction"></a>

Buildings can be classified into various categories on the basis of their usage. Different fire stations can have different ontology for building usage type but in order to provide citizens and businesses a uniform experience, it is important that the building usage types ontology is standardized at the state level.

For this purpose, the states can also use the National Building Code of India (NBC), a comprehensive building code, which is a national instrument providing guidelines for regulating building construction activities across the country.

## Data Table <a href="#data-table" id="data-table"></a>

| Sr. No. | \*Building Usage Type Code | \*Building Usage Type | \*Building Group (as per NBC) | \*Building Usage Type (as per NBC) |
| ------- | -------------------------- | --------------------- | ----------------------------- | ---------------------------------- |
| 1       | BU01                       | Residential           | Group A                       | Residential                        |
| 2       | BU02                       | Educational Institute | Group B                       | Educational                        |

The data given in the above table is sample data.

## Procedure <a href="#procedure" id="procedure"></a>

### Data Definitions <a href="#data-definitions" id="data-definitions"></a>

| Sr. No. | Column Name                      | Data Type  | Data Size | Mandatory | Description                                                                                                                |
| ------- | -------------------------------- | ---------- | --------- | --------- | -------------------------------------------------------------------------------------------------------------------------- |
| 1       | Building Usage Type Code         | Alphameric | 64        | Yes       | The code is given to the building usage type by the Fire Station. Eg: BU01 for Residential, BU02 for educational institute |
| 2       | Building Usage Type              | Text       | 256       | Yes       | Name of building usage type by the Fire Station. Eg: Residential, Educational Institute                                    |
| 3       | Building Group (as per NBC)      | Text       | 256       | Yes       | The code is given to the building usage type as per NBC. Eg: Group A, Group B                                              |
| 4       | Building Usage Type (as per NBC) | Text       | 256       | Yes       | Name of building usage type as per NBC. Eg: Residential, Educational                                                       |

### How to fill data <a href="#how-to-fill-data" id="how-to-fill-data"></a>

1. Download the data template attached to this page.
2. Get a good understanding of all the headers in the template sheet, their data type, size, and definitions by referring to the ‘Data Definition’ section of this document.
3. In case of any doubt, please reach out to the person who has shared this template with you to discuss and clear your doubts.
4. Identify all the different types of buildings on the basis of their usage that are being catered by the fire station in their area and start filling them in the Building Usage Type column.
5. Next, give each building usage type a unique code and enter the code in the Building Usage Type Code column, next to the Building usage type.
6. Map the data filled in the building usage types column to the building usage type and building groups as per the national building code.
7. Record the appropriate group and building type from NBC in the Building Group (as per NBC) and Building Usage Type (as per NBC) respectively.
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

| Sr. No. | Checklist Parameter                                                                              | Example                                                            |
| ------- | ------------------------------------------------------------------------------------------------ | ------------------------------------------------------------------ |
| 1       | Building Usage Type Codes that are defined by the Fire Station should be alphanumeric and Unique | <p>BU01: Residential</p><p>BU02: Educational Institute</p>         |
| 2       | Building Usage Type should not contain any special characters                                    | <p>Residential : [Allowed]</p><p>#Residential! : [Not allowed]</p> |

## Attachments <a href="#attachments" id="attachments"></a>

{% file src="../../../../.gitbook/assets/Configuration data template - Building Usage Type.xlsx" %}

{% file src="../../../../.gitbook/assets/Sample configuration data - Building Usage Type (1).xlsx" %}

{% file src="../../../../.gitbook/assets/NBC Building Classification.xlsx" %}

[![Creative Commons License](https://i.creativecommons.org/l/by/4.0/80x15.png)](http://creativecommons.org/licenses/by/4.0/)All content on this page by [eGov Foundation ](https://egov.org.in/)is licensed under a [Creative Commons Attribution 4.0 International License](http://creativecommons.org/licenses/by/4.0/).
