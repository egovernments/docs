# Configuring Tenants

### Overview <a id="Overview"></a>

Tenant represents a body in a system. In municipal system, a state and its ULBs \(Urban local bodies\) are tenants . ULB represents a city or a town in a state. Tenant configuration is done in mdms.

### Pre-requisites <a id="Pre-requisites"></a>

Before proceeding with the configuration, the following pre-requisites are met -

* Knowledge of json and how to write a json is required.
* Knowledge of MDMS is required.
* User with permissions to edit the git repository where MDMS data is configured.

### Key Functionalities <a id="Key-Functionalities"></a>

* For login page city name selection is required. Tenant added in MDMS shows in city drop-down of login page.
* In reports or in the employee inbox page the details related to ULB is displayed from the fetched ulb data which is added in MDMS.
* Modules i.e., TL,PT,MCS can be enabled based on the requirement for tenant.

### Deployment Details <a id="Deployment-Details"></a>

1. After adding the new tenant, the MDMS service needs to be restarted to read the newly added data.

### Configuration Details <a id="Configuration-Details"></a>



1. Tenant is added in tenant.json. In MDMS, file **tenant.json**, under **tenant** folder holds the details of state and ULBs  to be added in that state.   `1 2 3 4 5 6 7 8 9 10 11 12 13 14 15 16 17 18 19 20 21 22 23 24 25 26 27 28 29 30 31 32 33` `{ "tenantId": "uk", //<ReplaceWithDesiredTenantId> "moduleName": "tenant", "tenants": [ { "code": "uk.citya", //<state.ulbname> "name": "City A", //<name of the ulb> "description": "City A", //<ulb description> "logoId": "https://s3.ap-south-1.amazonaws.com/uk-egov-assets/uk.citya/logo.png", //<ulb logo path - To display ulb logo on login> "imageId": null, "domainUrl": "", //<ulb website url> "type": "CITY", "twitterUrl": null, "facebookUrl": null, "emailId": "complaints.citya@gmail.com", //<ulb email id> "OfficeTimings": { "Mon - Sat": "10.00 AM - 5.00 PM" }, "city": { "name": "City A", "localName": null, "districtCode": "CITYA", "districtName": null, "regionName": null, "ulbGrade": "Municipal Corporation", "longitude": 78.0322, "latitude": 30.3165, "shapeFileLocation": null, "captcha": null, "code": "248430" }, "address": "City A Municipal Cornoration Address", "contactNumber": "91 (135) 2653572" }]}`

Note: 



* To enable tenant the above data should be pushed in tenant.json file. Here "ULB Grade" and City  "Code" are important fields. **ULB Grade** can have a set of allowed values that determines the ULB type, \([Municipal corporation \(Nagar Nigam\)](https://en.wikipedia.org/wiki/Municipal_Corporations_in_India), Municipality \(municipal council, municipal board, municipal committee\) \(Nagar Parishad\), etc\). City "**Code**" has to be unique to each tenant.  This city-specific code is used in all transactions. Not permissible to change the code. If changed we will lose the data of the previous transactions done.
* Naming Convention for **Tenants Code**

**“Code”:“uk.citya”** is **StateTenantId.ULBTenantName"**

* **"logoId": "**[**https://s3.ap-south-1.amazonaws.com/uk-egov-assets/uk.citya/logo.png**](https://s3.ap-south-1.amazonaws.com/pb-egov-assets/pb.citya/logo.png)**",**  Here the last section of the path should be "/&lt;tenantId&gt;/logo.png". If we use anything else, logo will not be displayed on the UI. **&lt;tenantId&gt;** is the tenant code ie **“uk.citya”.**

2. Localization should be pushed for ulb grade and ulb name.  Format is given below.  
 **Localization for ULB Grade :**`1 2 3 4 5 6`  `{     "code": "ULBGRADE_MUNICIPAL_CORPORATION",     "message": "MUNICIPAL CORPORATION",     "module": "rainmaker-common",     "locale": "en_IN"   }`

  **Localization for ULB Name :** `1 2 3 4 5 6` `{     "code": "TENANT_TENANTS_UK_HALDWANI",         "message": "Haldwani",     "module": "rainmaker-tl",     "locale": "en_IN" }`

Format of localization code for tenant name : &lt;**MDMS\_State\_Tenant\_Folder\_Name**&gt;\_&lt;**Tenants\_Fille\_Name**&gt;\_&lt;**Tenant\_Code**&gt;\(replace dot with underscore\)

2.Boundary data should be added for the new tenant.

### Reference Docs <a id="Reference-Docs"></a>

#### Doc Links <a id="Doc-Links"></a>

| **Title**  | **Link** |
| :--- | :--- |
| tenant json file | [![](https://github.githubassets.com/favicon.ico)tenants.json](https://github.com/egovernments/ukd-mdms-data/blob/master/data/uk/tenant/tenants.json) |
| content | [MDMS Configuration:](https://digit-discuss.atlassian.net/wiki/spaces/DOPS/pages/110952456) |



