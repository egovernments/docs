# Stakeholders Type

## Introduction <a href="#introduction" id="introduction"></a>

Stakeholders refer to the technical persons and end-users of the OBPS system. The Stakeholders Type masters list allows the registration of stakeholders in the OBPS system. The list of stakeholders varies from one State/ULB to another.

## Data Table <a href="#data-table" id="data-table"></a>

| Sr. No. | Code\* | Stakeholder Type Name\* | Stakeholder Permit Validity (In Years) | Limitations on construction                                 |
| ------- | ------ | ----------------------- | -------------------------------------- | ----------------------------------------------------------- |
| 1       | BLD    | Builders                | 2                                      | N/A                                                         |
| 2       | ARC    | Architect               | 2                                      | N/A                                                         |
| 3       | TPR    | Town Planner            | 5                                      | Can construct 3 floors building, up to a height of 300 mts. |

The data given in the table is sample data for reference.

## Procedure <a href="#procedure" id="procedure"></a>

### Data Definition <a href="#data-definition" id="data-definition"></a>

| Sr. No. | Column Name                            | Data Type  | Data Size | Is Mandatory? | Description                                                                                                                                                 |
| ------- | -------------------------------------- | ---------- | --------- | ------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------- |
| 1       | Code                                   | Alphameric | 3         | Yes           | Unique Code provided with respect to Stakeholders type. It can be alphabetical, numeric, and alphanumeric as well                                           |
| 2       | Stakeholder Type Name                  | Text       | 64        | Yes           | Name provided for stakeholder type which is ideally the technical qualification of the person registering                                                   |
| 3       | Stakeholder Permit Validity (In Years) | Numeric    | 64        | No            | All the permits (Permits to the stakeholders) have a validity period within which he/she is authorized                                                      |
| 4       | Limitations on construction            | Text       | 612       | No            | Building Bye-laws defines and permits the limitations on the type of construction any technical person can take up to. This field captures such information |

### Steps to fill data <a href="#steps-to-fill-data" id="steps-to-fill-data"></a>

1. Download the data template attached to this page.
2. Refer to the ‘Data Definition’ section of this document to understand the headers in the template sheet, their data type, size, and definitions.
3. Reach out to the person who shared the template for further details or to clear your doubts. Identify if the State/ULB has a provision for capturing pipe size for connections.
4. Identify the stakeholders and fill into the given template. Refer to the [National Bye-Laws](http://mohua.gov.in/upload/uploadfiles/files/Chap-4.pdf) for more details on stakeholder types and defined limitations.
5. Go through the checklist to verify the data. Make sure that each and every point mentioned in the checklist is covered.

## Checklist <a href="#checklist" id="checklist"></a>

The checklist is a set of activities to be performed once the data is filled into a template to ensure data entry requirements are met. These activities have been divided into 2 groups as given below.

### Common Checklist <a href="#common-checklist" id="common-checklist"></a>

This checklist covers all the activities which are common across the entities.

| Sr. No. | Checklist Parameter                                                               | Example                                                                                                                      |
| ------- | --------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------- |
| 1       | Make sure that each and every point in this reference list has been taken care of | ​[Checklist](https://docs.digit.org/configure-digit/configuring-master-data-templates/module-setup/common-config/checklist)​ |

### Entity Specific Checklist <a href="#entity-specific-checklist" id="entity-specific-checklist"></a>

There is no separate entity-specific checklist for this entity.

## Attachments <a href="#attachments" id="attachments"></a>

{% file src="../../../../.gitbook/assets/Configurable Data Template  - Stakeholder Type_V1.xlsx" %}

{% file src="../../../../.gitbook/assets/Sample configuration data - Stakeholder Type.xlsx" %}

[![Creative Commons License](https://i.creativecommons.org/l/by/4.0/80x15.png)](http://creativecommons.org/licenses/by/4.0/)All content on this page by [eGov Foundation ](https://egov.org.in/)is licensed under a [Creative Commons Attribution 4.0 International License](http://creativecommons.org/licenses/by/4.0/).[\
](https://docs.digit.org/configure-digit/configuring-master-data-templates/module-setup/obpas-data/inspection-checklist)
