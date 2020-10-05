# Cross Hierarchy Mapping

## Introduction <a id="Introduction"></a>

This is the 3rd step that comes after the boundary data collection. Cross hierarchy mapping happens in case a child has a relationship with more than 2 parents. This double relationship between the child and parents could happen between different hierarchies as well.

For example: In Admin level boundary hierarchy a mohalla M1\(child\) could be a part of 2 Wards\(parent\) W1 and W2. In such a case a single Mohalla\(child\) has to be mapped to 2 Wards\(parent\).

## Data Table <a id="Data-Table"></a>

Below is the data table for the Boundary:

|  Hierarchy Type |  Hierarchy Type 1\* |  Hierarchy Type 2\* |  |  |
| :--- | :--- | :--- | :--- | :--- |
| Sr.No | Boundary Type\* | Boundary Code\* | Boundary Type\* | Boundary Code\* |
| 1 | Ward | W1 | Mohalla | M1 |
| Ward | W2 | Mohalla | M1 |  |
| 2 | Ward | W3 | Mohalla | M2 |
| Ward | W4 | Mohalla | M2 |  |

## Procedure <a id="Procedure"></a>

### Data Definition <a id="Data-Definition"></a>

| Sr. No. | Column Name | Data Type | Data Size | Is Mandatory? | Definition/ Description |
| :--- | :--- | :--- | :--- | :--- | :--- |
| 1 | Hierarchy Type 1 | Text | 256 | Yes | The type of hierarchy 1 the boundary belongs to which is to be mapped with other boundaries in hierarchy 2. Refer[ Boundary Hierarchies](https://digit-discuss.atlassian.net/wiki/spaces/DO/pages/424542339/Boundary+Hierarchies) |
| 2 | Hierarchy Type 2 | Text | 256 | Yes | The type of hierarchy 2 the boundary belongs to which is to be mapped with other boundary in hierarchy 1. Refer[ Boundary Hierarchies](https://digit-discuss.atlassian.net/wiki/spaces/DO/pages/424542339/Boundary+Hierarchies) |
| 3 | Boundary Type  | Text | 64  | Yes | This is the type of boundary from hierarchy 1. Refer[ Boundary Data](https://digit-discuss.atlassian.net/wiki/spaces/DO/pages/406552674/Boundary+Data) |
| 4 | Boundary Code | Alphanumeric | 64  | Yes | This is the code of the boundary for the boundary from hierarchy 1. Refer[ Boundary Data](https://digit-discuss.atlassian.net/wiki/spaces/DO/pages/406552674/Boundary+Data) |
| 5 |  Boundary Type  | Text | 64  | Yes | This is the type of boundary from hierarchy 2. Refer[ Boundary Data](https://digit-discuss.atlassian.net/wiki/spaces/DO/pages/406552674/Boundary+Data) |
| 6 | Boundary Code | Alphanumeric |  64 | Yes | This is the code of the boundary for the boundary from hierarchy 2. Refer[ Boundary Data](https://digit-discuss.atlassian.net/wiki/spaces/DO/pages/406552674/Boundary+Data) |

### Steps to fill data <a id="Steps-to-fill-data"></a>

1. Download the data template attached to this page.
2. Get a good understanding of all the headers in the template sheet, their data type, size, and definitions by referring to the ‘Data Definition’ section of this document.
3. In case of any doubt, please reach out to the person who has shared this template with you to discuss and clear your doubts.
4. Firstly Identify all the child levels which have a relation with more than 2 parent boundary types and their hierarchy types as well.
5. Fill up the boundary hierarchy \(names/ codes\) types in place of boundary type 1/2.
6. Then along with the codes start filling in one by one with the proper mapping between every child and parent.
7. The Sr. No should be in an incremental order for every new child level.
8. Prepare a new table for every different parent-child relation.
9. Verify the data once again by going through the checklist and taking care of each and every point mentioned in the checklist.

## Checklist <a id="Checklist"></a>

The checklist is a set of activities to be performed one the data is filled into a template to ensure data type, size, and format of data is as per the expectation. These activities have been divided into 2 groups as given below.

### Common Checklist <a id="Common-Checklist"></a>

This checklist covers all the activities which are common across the entities.

| Sr. No. | Checklist Parameter | Example |
| :--- | :--- | :--- |
| 1 | Make sure that each and every point in this reference list has been taken care of | [Checklist](https://digit-discuss.atlassian.net/wiki/spaces/DO/pages/502203140/Checklist) |

### Entity Specific Checklist <a id="Entity-Specific-Checklist"></a>

This checklist covers the activities which are specific to the entity. There is no entity-specific checklist activity applicable here.

## Attachments <a id="Attachments"></a>

1. Configurable Data Template - Cross-Boundary Hierarchy Mapping
2. Configurable Sample Data Template - Cross Hierarchy Mapping

