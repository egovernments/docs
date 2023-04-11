# Property Amalgamation

## Introduction

**What does amalgamation of properties mean?**

Two or more than two adjacent properties of an owner(s) are merged to form a single property. On merging of properties, merged properties are removed from the assessment registers while the retaining property is modified to add the merged property(ies) dimensions. The retaining and merged properties relationship is maintained for future reference. The combination of properties for which amalgamation can be done is given below.&#x20;

* Building + Building&#x20;
* Building + Vacant Land&#x20;
* Vacant Land + Vacant Land

**How is the amalgamation of properties accomplished on the ground?**

The amalgamation is considered a service and the owner(s) has to apply for it. A single application is created for the amalgamation of properties with details of all the properties and the required documents are produced in support of the application. There is no application/ processing fee associated with the amalgamation of properties.

## Key Metrics&#x20;

Below are state-wise approximate figures of amalgamation applications received and processed in a year.

| Andhra Pradesh    | \[On basis of data available in the property tax system] | 453  |
| ----------------- | -------------------------------------------------------- | ---- |
| Punjab            | \[On the basis of application received manually]         | 3000 |
| Uttarakhand       | \[On the basis of application received manually]         | 1500 |
| Cantonment Boards | \[On the basis of application received manually]         | 1000 |
| Odisha            | \[On the basis of application received manually]         | NA   |

## Proposed Solution&#x20;

**How to achieve this with the DIGIT Platform?**

1. A new application type ‘AMALGAMATION’ is created.&#x20;
2. Application no. format is defined.&#x20;
3. Only one application is created and the record of the same is maintained. All the properties involved in amalgamation are linked to that application.&#x20;
4. Workflow components are integrated and the wf status of retaining and merge properties are maintained as ‘In Workflow’ while the application is in flow.&#x20;
5. Though there are no instances observed where the application fee is charged for amalgamation, the applicability of the application fee is to be made configurable.&#x20;
6. The uniqueness of the owner (Individual) is identified based on the below-given attributes.&#x20;
   * Owner’s Name&#x20;
   * Owner’s Gender&#x20;
   * Owner’s Guardian Name&#x20;
   * Relationship with Guardian&#x20;
7. The uniqueness of the owner (Institutional) is identified based on the below-given attributes.&#x20;
   * Institute Name&#x20;
   * Institute Type&#x20;
   * Authorised Person Name&#x20;
8. No final document is generated as proof of amalgamation.&#x20;
9. Applicant(s) is/are intimated through SMS/ email notifications about the status and completion of the application.&#x20;
10. Any integration impact to be handled.&#x20;
    * Water and sewerage connection with merging properties to be moved to retaining property or to be brought to closure.&#x20;
    * Trade licenses associated with merging properties are to be moved to retaining property or to be brought to closure.&#x20;
11. Modules linked with property tax have to expose the API to check the status of applications in respective modules associated with a property.

## **Validations**

1. All the properties should be active properties, INACTIVE and WORKFLOW properties are not eligible for amalgamation.&#x20;
2. There should be any application in flow for other services as well linked with a merging property. E.g. Water Connection, Sewerage Connection, and Trade License.&#x20;
3. The owner (s) of the retaining property should always be a superset of the owner(s) of the merging property. It means there should not be a case where any owner of the merging property(ies) is not the one from the owners of the retaining property.&#x20;
4. There should not be any due on the properties which are to be merged while there is no such condition for retaining property.&#x20;
5. Dues related to water and sewerage charges for the connections associated with merging properties are not taken care of here.&#x20;
6. The total land area of retaining property = Land area of retaining + Total land area of properties to be merged.&#x20;
7. The total built-up area of retaining property = Built-up area of retaining + Total built-up area of properties to be merged.&#x20;
8. Properties to be merged are deactivated on completion of the process while retaining property remains active.&#x20;
9. Amalgamation will be effective from the date of approval of the application.

## Integrations Impacts&#x20;

### Water and Sewerage

1. There should not be an application related to water connection linked with a merging property in the workflow.&#x20;
2. In the case of water and sewerage connections associated with merging property to be moved to retaining property, it has to be achieved in the WnS module itself by modifying the connection.&#x20;
3. In the case of water and sewerage connections associated with merging property to be closed, it has to be achieved in the WnS module itself by using closure connection activity.

### Trade Licenses

1. In the case of trade licenses associated with merging properties to be moved to retaining property, it has to be achieved in the TL module itself on renewal of trade.&#x20;
2. In the case of trade licenses associated with merging properties to be closed, it has to be achieved in the TL module itself by using the closure of trade features.

### Accounting and Finance&#x20;

Accounting entries are passed for these transactions in terms of demand modifications.

## **User Persona**

| As a \<Role>            | I want \<What>                                        | So that \<Why>                                                                       |
| ----------------------- | ----------------------------------------------------- | ------------------------------------------------------------------------------------ |
| **Employee/Citizen**    | Search a property by unique property ID               | I can create an application for amalgamation of property(ies)                        |
| **Employee/Citizen**    | Search a property by owner’s mobile no.               | I can create an application for amalgamation of property(ies)                        |
| **Employee/Citizen**    | Search a property by owner’s name or by door no.      | I can create an application for amalgamation of property(ies)                        |
| **Employee/Citizen**    | Initiate new application for properties amalgamation  | I can merge adjunct property(ies) into main property.                                |
| **Citizen**             | Notification for my property amalgamation application | I can keep track of my application (notification sent will be according to workflow) |
| **Employee (Workflow)** | Amalgamation application in my inbox                  | I can take appropriate action on the application.                                    |
| **Employee**            | Search application                                    | I can see the application details.                                                   |
| **Citizen**             | My Applications                                       | I can see the application details to keep track of the application.                  |

## Navigation&#x20;

**Employee**&#x20;

Login → Search Property → View Property Details → Select ‘Amalgamation’ Action

**Citizen**&#x20;

Login → Amalgamation Menu → Search Property → Search Result → Select Property.

**Application No. Format**&#x20;

Application No. should follow the given format. PT-\<running sequence>

**User Flow**

Citizen/ Counter Employee - Application is initiated by citizen/ counter employee.&#x20;

Document Verification - The application and documents attached to it are verified by a document verifier.&#x20;

Field Inspection - The field inspector performs the field visit for the physical verification of properties.&#x20;

Approval of Application - The application is approved by the approver and the changes requested in the application come into effect in case the application fee is not applicable.&#x20;

Payment of application fee - In the case the application fee is applicable, the changes related to amalgamation come into effect only after the payment of the application fee.

<figure><img src="../../../../.gitbook/assets/image (444).png" alt=""><figcaption></figcaption></figure>

### **Application Form** <a href="#application-form" id="application-form"></a>

| Field Name                            | Data Type   | Is Mandatory? | Description                                                                               |
| ------------------------------------- | ----------- | ------------- | ----------------------------------------------------------------------------------------- |
| **Property Address**                  |             |               |                                                                                           |
| Pincode                               | Display     | Yes           | Pincode of area property is located.                                                      |
| City                                  | Display     | Yes           | City name of the property.                                                                |
| Locality/Mohalla                      | Display     | Yes           | Locality or mohalla name property is located.                                             |
| Street Name                           | Display     | Yes           | Street name property is located.                                                          |
| Door No./House No.                    | Display     | Yes           | House or door no. of the property.                                                        |
| **Ownership Details**                 |             |               |                                                                                           |
| Ownership Type                        | Display     | Yes           | Display of ownership type.                                                                |
| Institution Name                      | Display     | Yes           | It is applicable for the ownership type institution.                                      |
| Institution Type                      | Display     | Yes           | It is applicable for the ownership type institution.                                      |
| Name                                  | Display     | Yes           | Name of the owner of property or the authorised person in case of institutional property. |
| Guardian Name                         | Display     | Yes           | Name of guardian and applicable for single and multiple ownership type only.              |
| Gender                                | Display     | Yes           | Gender of owner/authorised person of the property.                                        |
| Landline No.                          | Display     | Yes           | Office landline no. in case of institutional ownership.                                   |
| Mobile No.                            | Display     | Yes           | Mobile no. of the owner/ authorised person.                                               |
| Designation                           | Display     | Yes           | Designation of the authorised person                                                      |
| Email                                 | Display     | Yes           | Email address of owner/ authorised person.                                                |
| Corresponding Address                 | Display     | Yes           | Corresponding address of the owner/ authorised person.                                    |
| **Merge Propertie(s)**                |             |               |                                                                                           |
| Property ID                           | Textbox     | Yes           | To search and add the property. A button with the label ‘Search and Add’.                 |
| Search Property                       | Hyperlink   | Yes           | To search the property by other params too and add it to the application.                 |
| **Property 1**                        |             |               |                                                                                           |
| Property ID                           | Display     | Yes           | Unique Property ID.                                                                       |
| Property Address                      | Display     | Yes           | Full address of property.                                                                 |
| Property Owners                       | Display     | Yes           | Comma separated list of property owners.                                                  |
| View Property Details/Remove Property | Hyperlink   | Yes           | To view the completed property details/ remove the added property.                        |
| **Assessment Details**                |             |               |                                                                                           |
| Property Type                         | Drop-down   | Yes           | Type of property                                                                          |
| Property Usage                        | Drop-down   | Yes           | Usage of property, residential, non-residential, or mixed.                                |
| Plot Size (In Sq Ft)                  | Textbox     | Yes           | Total area of land in square feet on which the property is constructed.                   |
| **Unit 1**                            |             |               |                                                                                           |
| Floor No.                             | Drop-down   | Yes           | Floor no. unit is located.                                                                |
| Usage                                 | Drop-down   | Yes           | Usage of unit, residential/ non-residential.                                              |
| Sub-Usage                             | Drop-down   | Yes           | Sub-usage of unit, mandatory in case of non-residential usage.                            |
| Occupancy                             | Drop-down   | Yes           | The type of occupancy of property.                                                        |
| Annual Rent                           | Textbox     | Yes           | Annual rent in INR, in case property is rented out.                                       |
| Built-up Area                         | Textbox     | Yes           | Built-up area of the unit in square feet.                                                 |
| Documents                             | File Picker | Yes           | The documents required to process the request.                                            |
| Timelines                             | Workflow    | Yes           | Display of workflow steps completed.                                                      |

### **Workflow**

| Action               | Role                       | From State                        | To State                          |
| -------------------- | -------------------------- | --------------------------------- | --------------------------------- |
| Initiate Application | Citizen/ Counter Employee  |                                   | Initiated                         |
| Submit Application   | Citizen/ Counter Employee  | Initiated                         | Pending for document verification |
| Verify and Forward   | Document Verifier          | Pending for document verification | Pending for field inspection      |
| Verify and Forward   | Field Inspector            | Pending for field inspection      | Pending approval for amalgamation |
| Send Back            | Document Verifier          | Pending for document verification | Pending for citizen action        |
| Send Back            | Field Inspector            | Pending for field inspection      | Pending for document verification |
| Send Back            | Approver                   | Pending approval for amalgamation | Pending for field inspection      |
| Send Back To Citizen | **\<roles having access>** | **\<Current Status>**             | Pending for citizen action        |
| Re-submit            | Citizen/ Counter Employee  | Pending for citizen action        | Pending for document verification |
| Re-submit            | Document Verifier          | Pending for document verification | Pending for field inspection      |
| Re-submit            | Field Inspector            | Pending for field inspection      | Pending approval for amalgamation |
| Approve              | Approver                   | Pending approval for amalgamation | Approved                          |
| Reject               | **\<roles having access>** | **\<Current Status>**             | Rejected                          |

### Wireframes&#x20;

Please click here to see the wireframes in Figma.&#x20;

Screenshots are attached below.&#x20;

### Citizen (Mobile First)

Apply for amalgamation

<figure><img src="../../../../.gitbook/assets/image (367).png" alt=""><figcaption></figcaption></figure>

Login into the account (If not already logged in)

<figure><img src="../../../../.gitbook/assets/image (438).png" alt=""><figcaption></figcaption></figure>

Select retaining the property for amalgamation&#x20;

The user will be displayed all the properties currently linked with the logged-in account and allowed to select one of them as a retaining property.

<figure><img src="../../../../.gitbook/assets/image (457).png" alt=""><figcaption></figcaption></figure>

The retaining property address and ownership details is displayed on apply.

<figure><img src="../../../../.gitbook/assets/image (449).png" alt=""><figcaption></figcaption></figure>

Select a property to merge&#x20;

The user will be displayed a list of all those properties which are owned by him/ her as a single owner or joint owner and allowed to select a property based on the below conditions.&#x20;

* The owner(s) of the merging property should be a subset of the owner(s) of the retaining property.&#x20;
* There should not be any dues on the property.&#x20;
* The property should be active property, **also there should not be any application in flow for an integrated module associated with the property.**&#x20;
* The property should belong to the same locality as the retaining property.

<figure><img src="../../../../.gitbook/assets/image (442).png" alt=""><figcaption></figcaption></figure>

Modify the assessment details of retaining property&#x20;

* Property Type&#x20;
* Plot Size

<figure><img src="../../../../.gitbook/assets/image (439).png" alt=""><figcaption></figcaption></figure>

* Number of basements&#x20;
* Number of floors

<figure><img src="../../../../.gitbook/assets/image (344).png" alt=""><figcaption></figcaption></figure>

Unit details&#x20;

* Usage&#x20;
* Sub-usage&#x20;
* Occupancy&#x20;
* Built-up Area&#x20;
* Annual Rental

<figure><img src="../../../../.gitbook/assets/image (341).png" alt=""><figcaption></figcaption></figure>

In case the property type is ‘Flat’, flat details are modified.

<figure><img src="../../../../.gitbook/assets/image (434).png" alt=""><figcaption></figcaption></figure>

In the case property type is vacant land, vacant land details are modified.

<figure><img src="https://lh4.googleusercontent.com/drLwE5wx93-H50p5FJZL8JiPBWugfi2BMPaXWAe4kZwdRLx_qUxyx8mA9z2nKve6bgI-irsjd1Gz0wXOL161Pe9ESW_gqharBIdrff-KiAHpMlbGf8Je_gRDUVy3Qwdmes1xnaoFNrL3nSbKvXqkyivOsumYD9hHZ4Rh8nkQHNVVUNarDhfU4pNO" alt=""><figcaption></figcaption></figure>

Documents attachment and summary of the application

<figure><img src="https://lh6.googleusercontent.com/FzYpT4agDDCHYz6kEkSKBgNZhbr4RcEWHqOOyPUA_lnRIGjxlywNFG-vruOy72SERphC7O2ZYfWLg8-xhYSjvt5c20b4GJ62CV09Pz8a6HULDfmz1WSEOlVFVWJqgxsV6_53N02DsJW-35zkXbrFbzVNe3T7CyX1GN-0pmSzGbhRUk5msbfycY22" alt=""><figcaption></figcaption></figure>

![](<../../../../.gitbook/assets/image (371).png>)![](<../../../../.gitbook/assets/image (369).png>)

### Employee

**Apply for amalgamation**

Property is searched and property details are viewed.​​​​

<figure><img src="../../../../.gitbook/assets/image (458).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../../../../.gitbook/assets/image (461).png" alt=""><figcaption></figcaption></figure>

Select the action ‘Amalgamate Property’ from the action list.​​​​​​​​​​

<figure><img src="../../../../.gitbook/assets/image (377).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../../../../.gitbook/assets/image (459).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../../../../.gitbook/assets/image (437).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../../../../.gitbook/assets/image (448).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../../../../.gitbook/assets/image (331).png" alt=""><figcaption></figcaption></figure>

## Use Case Scenarios

**UC 1 - Same Owner’s Residential Properties**

There are two properties A and B, both are residential in nature and belong to the same owner “xyz”.

Illustration: Suppose A is the retaining property while B has to be merged with A.

* Property A address remains unchanged.
* Property A ownership details remain unchanged.

So assessment details of property A are modified according to the assessment details of B. Below given are the activities which can be performed to modify the assessment detail of property A.

* The land area of A is increased to include B into A.
* One more UNIT is added to A representing B.
* An additional floor is added to A representing B.
* The existing UNIT area of A is increased.
* The existing UNIT rental value of A is increased.
* The remaining attributes would remain unchanged. Like Usage, Sub Usage, and Occupancy. Though these also can be edited if required.

Property B is linked with the application which is deactivated on completion.

**UC 2 - Same Owner’s Mixed Properties**

There are two properties A and B, A is residential while B is non-residential and belongs to the same owner “xyz”.Illustration: Suppose A is the retaining property while B has to be merged with A.

* Property A address remains unchanged.
* Property A ownership details remain unchanged.
* So assessment details of property A are modified according to the assessment details of B. Below given are the activities which can be performed to modify the assessment detail of property A.
  * The land area of A is increased to include B into A.
  * Property usage is changed to Mixed.
  * One more UNIT is added to A representing B and UNIT usage and sub-usage is kept according to property B, commercial in this case.
  * An additional floor is added to A representing B.
  * The existing UNIT area of A is increased.
  * The existing UNIT rental value of A is increased.
* Property B is linked with the application which is deactivated on completion.

**UC 3 - Solo Owner Of One Property And Joint Of Others**

There are two properties A and B, “xyz” is the only owner of property A while he/she is the joint owner of property B.Illustration:

* In case, property B is the retaining property, property A is merged according to usage cases #1 and #2.
* In case, property A is the retaining property, property B is first mutated in the name of the owners of property A using the mutation process.

**UC 4 - Properties Of Two Different Owners**

There are two properties A and B, the owner of property A is “xyz” while the owner of property B is “def”.Illustration:

* In case A is going to be retaining property, property B is to be first mutated in the name of “xyz” using the mutation process.
* In case B is going to be retaining property, property A to be first mutated in the name of “def” using the mutation process.

There are two properties A and B, the owner of property A is “xyz” which is institutional ownership while the owner of property B is “def” which is individual ownership.

* It is a similar case to #4, and the property is to be mutated first to initiate amalgamation.



