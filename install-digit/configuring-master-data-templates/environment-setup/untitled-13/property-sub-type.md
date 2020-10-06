# Property Sub Type

## Introduction <a id="Introduction"></a>

The Property Sub Type represents 2nd level classification to the [Property Type](https://digit-discuss.atlassian.net/wiki/spaces/DO/pages/413991251/Property+Type) and provides the option to further classify the property type in sub types. For example property type ‘Built-up’ is further classified into Independent House, A Flat In Apartment and Half Constructed Half Open and considered differently on tax calculation procedure.

## Data Table <a id="Data-Table"></a>

| Sr. No. | Property Sub Type Code\* | Property Sub Type\* \(In English\) | Property Sub Type\* \(In Local Language\) | Property Type Code\* |
| :--- | :--- | :--- | :--- | :--- |
| 1 | SHAREDPROPERTY | Flat / Part of the building | फ्लैट / भवन का हिस्सा | BUILTUP |
| 2 | INDEPENDENTPROPERTY | Independent House / Whole Building | स्वतंत्र घर / पूरी इमारत | BUILTUP |

Note: The data in the above table is sample data.

## Procedure <a id="Procedure"></a>

| Sr. No. | Column Name | Data Type | Data Size | Is Mandatory? | Description |
| :--- | :--- | :--- | :--- | :--- | :--- |
| 1 | Property Sub Type Code | Alphanumeric | 64 | Yes | Unique Identifier for property sub type record |
| 2 | Property Sub Type \(In English\) | Text | 256 | Yes | Nomenclature of “Property Sub Type” in English |
| 3 | Property Sub Type \(In Local Language\) | Text | 256 | Yes | Nomenclature of “Property Sub Type” in local language e.g. Telugu, Hindi etc. |
| 4 | Property Type Code | Reference | 64 | Yes | Property Type code referring to the [Property Type](https://digit-discuss.atlassian.net/wiki/spaces/DO/pages/413991251/Property+Type) |

### Steps to fill data <a id="Steps-to-fill-data"></a>

1. Download the data template attached to this page.
2. Refer to the ‘Data Definition’ section of this document to understand the headers in the template sheet, their data type, size, and definitions.
3. Reach out the person who shared the template for further details or to clear your doubts. Identify if the State/ULB has a provision for capturing pipe size for connections.
4. Identify all the property sub types applicable and fill into the given template.
5. Go through the checklist to verify the data. Make sure that each and every point mentioned in the checklist is covered.

### Checklist <a id="Checklist"></a>

The checklist is a set of activities to be performed one the data is filled into a template to ensure data type, size, and format of data is as per the expectation. These activities have been divided into 2 groups as given below.

### Common Checklist <a id="Common-Checklist"></a>

This checklist covers all the activities which are common across the entities.

| Sr. No. | Checklist Parameter | Example |
| :--- | :--- | :--- |
| 1 | Make sure that each and every point in this reference list has been taken care of | [Checklist](https://digit-discuss.atlassian.net/wiki/spaces/DO/pages/502203140/Checklist) |

### Entity Specific Checklist <a id="Entity-Specific-Checklist"></a>

There is no separate checklist is applicable to this entity.

## Attachments <a id="Attachments"></a>

1. Configurable Data Template - Property Sub Type

\(Refer to “Property Sub Type Fee” tab in the attached file\)

 Configuration Data T...ter.xlsx10 KB

1. Sample Configurable Data- Property Sub Type

