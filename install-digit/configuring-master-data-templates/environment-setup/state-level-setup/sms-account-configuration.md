# SMS Account Configuration

## Introduction <a id="Introduction"></a>

The SMS service is a way of communicating necessary information/updates to the users on there various transactions on DIGIT applications.

In order to update the users, there is a certain notification which has been configured at various steps in the application process which can be changed/ configured based upon the requirements.

## Data Table <a id="Data-Table"></a>

We have the below-mentioned parameters which we use for configuration:

| Sr. No. | Parameter | Value |
| :--- | :--- | :--- |
| 1 | sms.provider.url | www.xyz.com |
| 2 | sms.username.parameter | mnsbihar@001 |
| 3 | sms.username.value | \*\*\* |

Note: The data given in the above table is sample data. The parameters and its values are SMS service provided specific and may vary accordingly.

## Procedure <a id="Procedure"></a>

For the SMS service to be integrated there are various things for which the vendor more or less guides us for the steps to be followed but below mentioned are a few basic steps and the generic data definitions which could be followed.

### Data Definition <a id="Data-Definition"></a>

Below mentioned are the descriptions of the parameters which are needed for configuration:

| Sr. No. | Column Name | Data Type | Data Size | Mandatory | Description |
| :--- | :--- | :--- | :--- | :--- | :--- |
| 1 | Parameter | Alphanumeric | 64 | Yes | The parameter required to be configured |
| 2 | Value | Alphanumeric | 64 | Yes | The corresponding value of the parameter |

Note: Parameter names could differ from vendor to vendor.

### Steps to fill Data <a id="Steps-to-fill-Data"></a>

Since the SMS service is a vendor delivered service for which the below steps would have to be followed:

1. Download the data template attached to this page.
2. Get a good understanding of all the headers in the template sheet, their data type, size, and definitions by referring to the ‘Data Definition’ section of this document.
3. In case of any doubt, please reach out to the person who has shared this template with you to discuss and clear your doubts.
4. The SMS vendor has to provide the data in the data template attached.
5. Verify the data once again by going through the checklist and making sure that each and every point mentioned in the checklist is covered.

## Checklist <a id="Checklist"></a>

The checklist is a set of activities to be performed one the data is filled into a template to ensure data type, size, and format of data is as per the expectation. These activities have been divided into 2 groups as given below.

### Common Checklist <a id="Common-Checklist"></a>

This checklist covers all the activities which are common across the entities.

| Sr. No. | Checklist Parameter | Example |
| :--- | :--- | :--- |
| 1 | Make sure that each and every point in this reference list has been taken care of. | [Checklist](https://digit-discuss.atlassian.net/wiki/spaces/DO/pages/502203140/Checklist) |

### Entity Specific Checklist <a id="Entity-Specific-Checklist"></a>

This checklist covers the activities which are specific to the entity.

| Sr. No. | Checklist Parameter | Example |
| :--- | :--- | :--- |
| 1 | Make sure that the vendor should support multiple language functionality and especially the local language of the state. | - |

## Attachments <a id="Attachments"></a>

1. Configurable Data Template - SMS Configuration

    2. Sample Configurable Data - SMS Configuration

