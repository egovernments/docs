# Workflow Levels

### Introduction

Workflow levels are defined as a service with Rights/Roles to perform a set of Workflow Actions. There would be one or more than one level involved in a workflow process. This page helps to understand and then define all the levels with their job description and fill in a standard template.

### Data Table

<table><thead><tr><th width="106">Sr. No.</th><th>Module</th><th>Service</th><th>Workflow Level</th><th>Task</th><th>Role</th></tr></thead><tbody><tr><td>1</td><td>Finance</td><td>Bill Accounting</td><td>Level 1</td><td>Create Bill</td><td>Accounts Clerk</td></tr><tr><td>2</td><td>Finance</td><td>Bill Accounting</td><td>Level 2</td><td>Create and Approve</td><td>Accounts Clerk</td></tr><tr><td>3</td><td>Finance</td><td>Bill Accounting</td><td>Level 3</td><td>Forward for Approval</td><td>Chief Accountant</td></tr><tr><td>4</td><td>Finance</td><td>Bill Accounting</td><td>Level 4</td><td>Verify the Bill</td><td>Chief Accountant</td></tr><tr><td>5</td><td>Finance</td><td>Bill Accounting</td><td>Level 5</td><td>Approval</td><td>Approver</td></tr></tbody></table>

{% hint style="info" %}
Data given in the above table is sample data.
{% endhint %}

### Procedure

#### Data Definition

<table><thead><tr><th width="101">Sr. No.</th><th width="147">Column Name</th><th>Data Type</th><th>Data Size</th><th>Is Mandatory?</th><th>Definition/ Description</th></tr></thead><tbody><tr><td>1</td><td>Module</td><td>Text</td><td>64</td><td>Yes</td><td>The module indicates for which the user would be mapped for a specific module to perform the action</td></tr><tr><td>2</td><td>Service</td><td>Text</td><td>64</td><td>Yes</td><td>The service indicates the type of process which the user performs in a particular module</td></tr><tr><td>3</td><td>Workflow Level</td><td>Integer</td><td>2</td><td>Yes</td><td>The workflow level indicates when a process has executed the level at which the flow of the process in progress</td></tr><tr><td>4</td><td>Task</td><td>Text</td><td>64</td><td>Yes</td><td>The task refers to which state the action is in progress during the workflow</td></tr><tr><td>5</td><td>Job Description</td><td>Text</td><td>256</td><td>Yes</td><td>A short description provided for the role (Example: Designation of the Role)</td></tr></tbody></table>

#### Step to fill data

1. Download the data template attached to this page.
2. Have it open and go through all the headers and understand their meaning of them by referring 'Data Definition' section.
3. Make sure all the headers, data type, field size and definition/ description are understood properly. In case of any doubt, please reach out to the person who has shared this document with you to discuss the same and clear out the doubts.
4. Identify all different types of services on the basis of ULB’s functions to create a workflow.
5. Start filling the data starting from serial no. and complete a record at once. repeat this exercise until the entire data is filled into a template.
6. Verify the data once again by going through the checklist and taking care of each and every point mentioned in the checklist.

### Checklist

The checklist is a set of activities to be performed once the data is filled into a template to ensure data type, size, and format of data is as per the expectation. These activities have been divided into 2 groups as given below.

#### Common Checklist

This checklist covers all the activities which are common across the entities.

<table><thead><tr><th width="133.33333333333331">Sr. No</th><th>Checklist Parameter</th><th>Example</th></tr></thead><tbody><tr><td>1</td><td>Make sure that each and every point in this reference list has been taken care of</td><td><a href="https://digit-discuss.atlassian.net/wiki/spaces/DO/pages/502203140/Checklist">Checklist</a></td></tr></tbody></table>

#### Entity Specific Checklist

Please discuss this with a relevant department head before finalizing the workflow.
