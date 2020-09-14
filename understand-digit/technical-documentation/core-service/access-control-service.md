# Access Control Service

### Overview <a id="Overview"></a>

DIGIT is API based Platform here each API is denoting to a DIGIT resource. Access Control Service \(ACS\) primary job is to authorise end user based on their roles and provide access of the DIGIT platform resources. Access control functionality basically works based on below points:

**Actions:** Actions are events which is performed by an user. This can be a api end-point or Frontend event. This is MDMS master

**Roles:** Role are assigned to user, a user can hold multiple roles. Roles are defined in MDMS masters.

**Role-Action:** Role actions are mapping b/w Actions and Roles. Based on Role,Action  mapping access control service identifies applicable action for role.

### Pre-requisites <a id="Pre-requisites"></a>

Before you proceed with the configuration, make sure the following pre-requisites are met -

* _Java 8_
*  MDMS service is up and running

### Key Functionalities <a id="Key-Functionalities"></a>

* Serve the applicable actions for a user based on user role \(To print menu three\).
* On each action which is performed by an user, access control look at the roles for the user and validate actions mapping with the role.
* Support tenant level role-action. \(eg: An employee from Amritsar can have a role of APPROVER for other ULB like Jalandhar and hence will be authorised to act as APPROVER in Jalandhar.\)

### Deployment Details <a id="Deployment-Details"></a>

1. Deploy the latest version of Access Control Service
2. Deploy MDMS service to fetch the Role Action Mappings

### Configuration Details <a id="Configuration-Details"></a>

1. Define the roles :`1 2 3 4 5` `{ "code": "EMPLOYEE", "name": "Employee", "description": "Default role for all employees" }`
2. Add the Actions \(URL\) :`1 2 3 4 5 6 7 8 9 10 11 12` `{ "id": {{ACTION_ID}}, "name": "Create TradeLicense", "url": "/tl-services/v1/_create", "parentModule": "", "displayName": "Create TradeLicense", "orderNumber": 0, "enabled": false, "serviceCode": "tl-services", "code": "null", "path": "" }`
3. Add the role action mapping:`1 2 3 4 5 6` `{ "rolecode": "EMPLOYEE", "actionid": {{ACTION_ID}}, "actioncode": "", "tenantId": "pb" }`

_\(The details about the fields in the configuration can be found in the swagger contract\)_

### Integration <a id="Integration"></a>

#### Integration Scope <a id="Integration-Scope"></a>

Any micro micro service which requires authorisation can leverage  the functionalities provided by access control service.

#### Integration Benefits <a id="Integration-Benefits"></a>

Any new micro service that is to be added in the platform won’t have to worry about authorisation. It can just add it’s role action mapping in the master data and Access Control Service will perform authorisation whenever API for the micro service is called .

#### Steps to Integration <a id="Steps-to-Integration"></a>

1. To integrate with Access Control Service the role action mapping has to be configured\(added\) in the MDMS service.
2. The service needs to call /actions/\_authorize API of Access Control Service to check for authorisation of any request

#### Interaction Diagram:  <a id="Interaction-Diagram:"></a>

![](../../../.gitbook/assets/image%20%2876%29.png)

### Reference Docs <a id="Reference-Docs"></a>

#### Doc Links <a id="Doc-Links"></a>

| **Title**  | **Link** |
| :--- | :--- |
|  API Contract |  [https://raw.githubusercontent.com/egovernments/egov-services/master/docs/egov-accesscontrol/contracts/v1-0-1.yml](https://raw.githubusercontent.com/egovernments/egov-services/master/docs/egov-accesscontrol/contracts/v1-0-1.yml) |
|  MDMS Service | [Core Services](https://digit-discuss.atlassian.net/wiki/spaces/DD/pages/647299090/Core+Services)  \[MDMS LINK HAS TO BE UPDATED\] |

#### API List <a id="API-List"></a>

|  | **Link** |
| :--- | :--- |
|  /actions/\_authorize |  \[LINK TO BE UPDATED\] |
|  |  |

\(\*POSTMAN COLLECTION HAS TO BE UPDATED\)

