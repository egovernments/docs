# Workflow Process

### Introduction

The workflow process is a set of steps through which information flows in sequence and the [workflow roles](https://digit-discuss.atlassian.net/wiki/spaces/DO/pages/537624711/Workflow+Actions) which derives the actors are assigned to a step to complete the work defined for that [level](https://digit-discuss.atlassian.net/wiki/spaces/DO/pages/537690461/Workflow+Levels). The states of each level are derived based on the information received from the previous step.

### Data Table

<table><thead><tr><th width="108">Sr. No.</th><th width="151">Current State</th><th>Workflow Actions</th><th>Next State</th><th>Role Name</th><th>SLA</th></tr></thead><tbody><tr><td>1</td><td></td><td>Create and Approve</td><td>Approved</td><td>Assistant</td><td>NA</td></tr><tr><td>2</td><td></td><td>Forward</td><td>Pending for Approval</td><td>Assistant</td><td>NA</td></tr><tr><td>3</td><td>Pending for Approval</td><td>Verify and Approve</td><td>Approved</td><td>Supervisor</td><td>NA</td></tr><tr><td>4</td><td>Pending for Approval</td><td>Save</td><td>Pending for Approval</td><td>Supervisor</td><td>NA</td></tr><tr><td>5</td><td>Pending for Approval</td><td>Reject</td><td>Rejected</td><td>Supervisor</td><td>NA</td></tr><tr><td>6</td><td>Pending for Approval</td><td>Send Back to Assistant</td><td>Rejected for Review</td><td>Supervisor</td><td>NA</td></tr><tr><td>7</td><td>Rejected for Review</td><td>Forward</td><td>Pending for Approval</td><td>Assistant</td><td>NA</td></tr><tr><td>8</td><td>Rejected for Review</td><td>Cancel</td><td>Rejected</td><td>Assistant</td><td>NA</td></tr></tbody></table>

{% hint style="info" %}
Data given in the above table is sample data.
{% endhint %}

### Procedure

#### Data Definition

<table><thead><tr><th width="95">Sr. No.</th><th>Column Name</th><th width="93">Data Type</th><th width="95">Data Size</th><th width="78">Is Mandatory?</th><th>Definition/ Description</th></tr></thead><tbody><tr><td>1</td><td>Current State</td><td>Text</td><td>256</td><td>Yes</td><td>The Current State indicates the stage at which the process of the workflow in progress</td></tr><tr><td>2</td><td>Action</td><td>Reference</td><td>64</td><td>Yes</td><td>The Action indicates the activity that can be performed at the respective stage in the workflow. This refers to Workflow Actions</td></tr><tr><td>3</td><td>Next State</td><td>Text</td><td>256</td><td>Yes</td><td>The Next State is the state in the workflow that gets updated to in the respective stage on performing the action. (Example: assigning the for approval from one person to next person)</td></tr><tr><td>4</td><td>Role Name</td><td>Reference</td><td>64</td><td>Yes</td><td>The role is the different hierarchy of people with designation who are authorized to initiate, approval or rejecting the process. It refers to Workflow Levels</td></tr><tr><td>5</td><td>SLA</td><td>Integer</td><td>2</td><td>No</td><td>The SLA indicates the time-frame within which the action to be completed</td></tr></tbody></table>

#### Step to fill data

1. Download the data template attached to this page.
2. Have it open and go through all the headers and understand their meaning of them by referring 'Data Definition' section.
3. Make sure all the headers, data type, field size and definition/ description are understood properly. In case of any doubt, please reach out to the person who has shared this document with you to discuss the same and clear out the doubts.
4. Start filling the data starting from serial no. and complete a record at once. repeat this exercise until the entire data is filled into a template.
5. Verify the data once again by going through the checklist and taking care of each and every point mentioned in the checklist.

### Checklist

The checklist is a set of activities to be performed once the data is filled into a template to ensure data type, size, and format of data is as per the expectation. These activities have been divided into 2 groups as given below.

#### Common Checklist

This checklist covers all the activities which are common across the entities.

| Sr. No | Checklist Parameter                                                               | Example                                    |
| ------ | --------------------------------------------------------------------------------- | ------------------------------------------ |
| 1      | Make sure that each and every point in this reference list has been taken care of | [Checklist](../common-config/checklist.md) |

#### Entity Specific Checklist

Please discuss this with a relevant department head before finalizing the workflow.
