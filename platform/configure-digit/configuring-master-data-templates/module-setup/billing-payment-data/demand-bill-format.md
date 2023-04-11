# Demand Bill Format

### Introduction

Bill format can be configured on a module level. Few components on the DIGIT sample bill can be configured on a state level and few at ULB level. Components that can be changed on a module level can be categorized as mentioned:

1. Important messages: Values can be configured on a module level - state level

### Data Table

| Sr. No. | Business      | Category           | Particulars                                                             |
| ------- | ------------- | ------------------ | ----------------------------------------------------------------------- |
| 1       | Water Charges | Important messages | <ol><li>5% rebate to be given on advance payment on the bills</li></ol> |

{% hint style="info" %}
Data given in the table is sample data for reference.
{% endhint %}

### Procedure

#### Data Definition

| Sr. No. | Column Name | Data Type    | Data Size | Mandatory | Description                                                                             |
| ------- | ----------- | ------------ | --------- | --------- | --------------------------------------------------------------------------------------- |
| 1       | Category    | Text         | 64        | Yes       | To list out the components on the bill, every particular can be grouped into a category |
| 2       | Particulars | Alphanumeric | 256       | Yes       | Each category can have multiple entries under it, ie particulars                        |
| 3       | Business    | Text         | 64        | Yes       | The business for which the Bill format is to be configured                              |

#### How to fill data

1. Download the data template attached to this page.
2. Get a good understanding of all the headers in the template sheet, their data type, size, and definitions by referring to the ‘Data Definition’ section of this document.
3. In case of any doubt, please reach out to the person who has shared this template with you to discuss and clear your doubts.
4. Get information about the bill format followed by state
5. Classify the components on the bill and place it under any category
6. Map the particulars under each category with DIGIT sample bill
7. Verify the data once again by going through the checklist and making sure that each and every point mentioned in the checklist is covered.

### Checklist

The checklist is a set of activities to be performed one the data is filled into a template to ensure data type, size, and format of data is as per the expectation. These activities have been divided into 2 groups as given below.

#### Common Checklist

This checklist covers all the activities which are common across the entities.

| Sr. No. | Checklist Parameter                                                               | Example                                    |
| ------- | --------------------------------------------------------------------------------- | ------------------------------------------ |
| 1       | Make sure that each and every point in this reference list has been taken care of | [Checklist](../common-config/checklist.md) |

#### Entity Specific Checklist

Entity Specific Checklist is not required separately.

### Attachments

{% file src="../../../../../.gitbook/assets/configuration-data-template-demand-bill-format.xlsx" %}
Configuration Data Template&#x20;
{% endfile %}

{% file src="../../../../../.gitbook/assets/sample-configuration-data-demand-bill-format.xlsx" %}
Sample Data
{% endfile %}

[![Creative Commons License](https://i.creativecommons.org/l/by/4.0/80x15.png)​](http://creativecommons.org/licenses/by/4.0/)All content on this page by [eGov Foundation](https://egov.org.in/) is licensed under a [Creative Commons Attribution 4.0 International License](http://creativecommons.org/licenses/by/4.0/).
