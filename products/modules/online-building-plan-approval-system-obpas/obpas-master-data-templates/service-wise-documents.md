# Service-Wise Documents

## Introduction <a href="#introduction" id="introduction"></a>

Service-wise documents list tells about the documents required for processing of listed services. Citizens can view the checklist based on the selected service. States/ULBs can configure the list of supporting documents required for each service.

## Data Table <a href="#data-table" id="data-table"></a>

| Sr. No. | Service Code\* | Service Name     | Document Name\* | Is Mandatory?\* |
| ------- | -------------- | ---------------- | --------------- | --------------- |
| 1       | NC             | New Construction | Aadhar Card     | No              |
| 2       | NC             | New Construction | Fire NOC        | Yes             |

The data given in the table is sample data for reference.

## Procedure <a href="#procedure" id="procedure"></a>

### Data Definition <a href="#data-definition" id="data-definition"></a>

| Sr. No. | Column Name     | Data Type    | Data Size | Is Mandatory? | Description                                                                                |
| ------- | --------------- | ------------ | --------- | ------------- | ------------------------------------------------------------------------------------------ |
| 1       | Service Code    | Alphanumeric | 64        | Yes           | Code of service - Refer to the [service list ](list-of-services.md)to understand in detail |
| 2       | Service Name    | Text         | 64        | No            | Name of service - Refer to the [service list](list-of-services.md) to understand in detail |
| ​       | Document Name\* | Text         | 256       | Yes           | Name of documents which are needed to avail the service                                    |
| 3       | Is Mandatory?   | Text         | 3         | Yes           | It indicates if the provided document is mandatory or not to avail the service             |

### Steps to fill data <a href="#steps-to-fill-data" id="steps-to-fill-data"></a>

1. Download the data template attached to this page.
2. Refer to the ‘Data Definition’ section of this document to understand the headers in the template sheet, their data type, size, and definitions.
3. Reach out to the person who shared the template for further details or to clear your doubts. Identify if the State/ULB has a provision for capturing pipe size for connections.
4. Identify the documents which are needed to avail the services and fill into the given template.
5. Go through the checklist to verify the data. Make sure that each and every point mentioned in the checklist is covered.

## Checklist <a href="#checklist" id="checklist"></a>

The checklist is a set of activities to be performed once the data is filled into a template to ensure data entry requirements are met. These activities have been divided into 2 groups as given below.

### Common Checklist <a href="#common-checklist" id="common-checklist"></a>

This checklist covers all the activities which are common across the entities.

| Sr. No. | Checklist Parameter                                                               | Example                                                                                     |
| ------- | --------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------- |
| 1       | Make sure that each and every point in this reference list has been taken care of | ​[Checklist](https://digit-discuss.atlassian.net/wiki/spaces/DO/pages/502203140/Checklist)​ |

### Entity Specific Checklist <a href="#entity-specific-checklist" id="entity-specific-checklist"></a>

There is no separate entity-specific checklist for this entity.

## Attachments <a href="#attachments" id="attachments"></a>

{% file src="../../../../.gitbook/assets/Configuration data template - Service Documents_V1.xlsx" %}

{% file src="../../../../.gitbook/assets/Sample configuration data - Service Documents.xlsx" %}

[![Creative Commons License](https://i.creativecommons.org/l/by/4.0/80x15.png)](http://creativecommons.org/licenses/by/4.0/)All content on this page by [eGov Foundation ](https://egov.org.in/)is licensed under a [Creative Commons Attribution 4.0 International License](http://creativecommons.org/licenses/by/4.0/).[\
](https://docs.digit.org/configure-digit/configuring-master-data-templates/module-setup/obpas-data/list-of-services)
