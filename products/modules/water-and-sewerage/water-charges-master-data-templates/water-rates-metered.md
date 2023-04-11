# Water Rates (Metered)

## Introduction <a href="#introduction" id="introduction"></a>

Water Charges are levied for metered connections based on consumption. The rate for calculation of water charges varies widely and is dependent upon various parameters. In the DIGIT W\&S module, water charges defined are based on actual consumption and property usage type.

## Data Table <a href="#data-table" id="data-table"></a>

| Sr. No. | \*Property Usage Type | \*Water consumed value from (units) | \*Water consumed value to (units) | \*Rate (in Rs/ unit) |
| ------- | --------------------- | ----------------------------------- | --------------------------------- | -------------------- |
| 1       | Residential           | 1                                   | 150                               | 3                    |
| 2       | Residential           | 151                                 | 300                               | 4                    |

The data given in the table is sample data for reference.

## Procedure <a href="#procedure" id="procedure"></a>

### Data Definition <a href="#data-definition" id="data-definition"></a>

| Sr. No. | Column Name               | Data Type    | Data Size | Mandatory | Description                                                                                        |
| ------- | ------------------------- | ------------ | --------- | --------- | -------------------------------------------------------------------------------------------------- |
| 1       | Property usage type       | Alphanumeric | 64        | Yes       | Refer [Usage Category Major](../../property-tax/pt-master-data-templates/usage-category-major.md)​ |
| 2       | Water consumed value from | Decimal      | (5,3)     | Yes       | From value for water consumed                                                                      |
| 3       | Water consumed value to   | Decimal      | (5,3)     | Yes       | To value for water consumed                                                                        |
| 4       | Rate                      | Decimal      | (3,3)     | Yes       | Consumption charges per unit corresponding to the usage type                                       |

### Steps to fill data <a href="#steps-to-fill-data" id="steps-to-fill-data"></a>

1. Download the data template attached to this page.
2. Refer to the ‘Data Definition’ section of this document to learn more about the template sheet, data type, size, and definitions.
3. Please reach out to the person who has shared this template with you to discuss and clear your doubts.
4. Select the property type from the drop-down list available in the Property Usage Type column.
5. Enter the Slab (water consumed) range details in the From and To Value for water consumed.
6. Enter the Rate for the specified slab range and property type.
7. Verify the data once again by going through the checklist and making sure that each and every point mentioned in the checklist is covered.

## Checklist <a href="#checklist" id="checklist"></a>

The checklist is a set of activities to be performed once the data is filled into a template to ensure data type, size, and format of data is as per the expectation. These activities have been divided into 2 groups as given below.

### Common Checklist <a href="#common-checklist" id="common-checklist"></a>

This checklist covers all the activities which are common across the entities.

| Sr. No. | Checklist Parameter                                                               | Example                                                                                                                      |
| ------- | --------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------- |
| 1       | Make sure that each and every point in this reference list has been taken care of | ​[Checklist](https://docs.digit.org/configure-digit/configuring-master-data-templates/module-setup/common-config/checklist)​ |

### Entity Specific Checklist <a href="#entity-specific-checklist" id="entity-specific-checklist"></a>

A separate Entity Specific Checklist is not required for this module data.

## Attachments <a href="#attachments" id="attachments"></a>

{% file src="../../../../.gitbook/assets/Configuration data template - Water rates (metered).xlsx" %}

{% file src="../../../../.gitbook/assets/Sample configuration data - Water rates (metered).xlsx" %}

[![Creative Commons License](https://i.creativecommons.org/l/by/4.0/80x15.png)](http://creativecommons.org/licenses/by/4.0/)All content on this page by [eGov Foundation ](https://egov.org.in/)is licensed under a [Creative Commons Attribution 4.0 International License](http://creativecommons.org/licenses/by/4.0/).
