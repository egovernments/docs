---
description: Browse details on configuring master data template
---

# Grievance Type

## Introduction <a href="#introduction" id="introduction"></a>

A grievance is a formal complaint submitted to a ULB. Something wrong or something believed to cause distress in services provided by the ULB is considered as grounds for complaint. Grievances that are closely associated with ULB’s functions classified into different buckets, that different sections of ULB deal with are known as grievance types.

## Data Table <a href="#data-table" id="data-table"></a>

| Sr. No. | Grievance Type Code\* | Grievance Type\* (In English) | Grievance Type\* (In Local Language) |
| ------- | --------------------- | ----------------------------- | ------------------------------------ |
| 1       | SLS                   | Street Lights                 | स्ट्रीट लाइट                         |
| 2       | GBG                   | Garbage                       | कचरा                                 |
| 3       | DRN                   | Drains                        | नाली                                 |

The data given in the table is sample data.

## Procedure <a href="#procedure" id="procedure"></a>

### Data Definition <a href="#data-definition" id="data-definition"></a>

| Sr. No. | Column Name                          | Data Type    | Data Size | Is Mandatory? | Definition/ Description                                                                                                                                                                                                   |
| ------- | ------------------------------------ | ------------ | --------- | ------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| 1       | Grievance Type Code\*                | Alphanumeric | 64        | Yes           | Unique code is given to the grievance type. This code is used to uniquely identify the complaint type and as a reference in the child record. E.g. SLS given above in data table to identify Street Lights complaint type |
| 2       | Grievance Type\* (In English)        | Text         | 256       | Yes           | This is the text or string stating grievance type in English                                                                                                                                                              |
| 3       | Grievance Type\* (In Local Language) | Text         | 256       | Yes           | This the text or string stating the grievance type in local language like Hindi, Telugu etc. whatever is applicable                                                                                                       |

### Step to fill data <a href="#step-to-fill-data" id="step-to-fill-data"></a>

1. Download the data template attached to this page.
2. Have it open and go through all the headers and understand the meaning of them by referring 'Data Definition' section.
3. Make sure all the headers, its data type, field size and its definition/ description is understood properly. In case of any doubt, please reach out to the person who has shared this document with you to discuss the same and clear out the doubts.
4. Identify all different types of grievances on the basis of ULB’s functions.
5. Start filling the data starting from serial no. and complete a record at once. repeat this exercise until the entire data is filled into a template.
6. Verify the data once again by going through the checklist and taking care of each and every point mentioned in the checklist.

## Checklist <a href="#checklist" id="checklist"></a>

The checklist is a set of activities to be performed once the data is filled into a template to ensure data type, size, and format of data is as per the expectation. These activities have been divided into 2 groups as given below.

### Common Checklist <a href="#common-checklist" id="common-checklist"></a>

This checklist covers all the activities which are common across the entities.

To see a common checklist refer to the page [Checklist](https://docs.digit.org/install-digit/configuring-master-data-templates/module-setup/untitled-1/checklist) consisting of all the activities which are to be followed to ensure completeness and quality of data.

### Entity Specific Checklist <a href="#entity-specific-checklist" id="entity-specific-checklist"></a>

This checklist covers the activities which are specific to the entity.

| Sr. No. | Activity                                                                                            | Example                                                                  |
| ------- | --------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------ |
| 1       | Grievance type code should not have any special characters other than ‘-', and '\_’                 | <p>SLS - [Allowed]</p><p>SLS1 - [Allowed]</p><p>SL#1 - [Not Allowed]</p> |
| 2       | Grievance type should be text and should not contain special characters other than ‘-', '\_', SPACE | <p>Street Light - [Allowed]</p><p>Street_Light# -[Not allowed]</p>       |

## Attachments <a href="#attachments" id="attachments"></a>

{% file src="../../../../.gitbook/assets/Configuration data template - Grievance Type_V1.xlsx" %}

{% file src="../../../../.gitbook/assets/Sample configuraion data - Grievance Type and Subtype.xlsx" %}

[![Creative Commons License](https://i.creativecommons.org/l/by/4.0/80x15.png)](http://creativecommons.org/licenses/by/4.0/)All content on this page by [eGov Foundation ](https://egov.org.in/)is licensed under a [Creative Commons Attribution 4.0 International License](http://creativecommons.org/licenses/by/4.0/).
