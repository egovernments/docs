# Workflow Service

### Overview <a id="Overview"></a>

Workflows are a series of steps that moves a process from one state to another state by actions performed by different kind of Actors - Humans, Machines, Time based events etc. to achieve a goal like on boarding an employee, or approve an application or grant a resource etc. The _egov-workflow-v2_ is a workflow engine which helps in performing this operations seamlessly using a predefined configuration.

### Pre-requisites <a id="Pre-requisites"></a>

Before you proceed with the documentation, make sure the following pre-requisites are met -

* _Java 8_
* Kafka server is up and running
* egov-persister service is running and has workflow persister config path added in it
* PSQL server is running and database is created to store workflow configuration and data

### Key Functionalities <a id="Key-Functionalities"></a>

* Always allow anyone with a role in the workflow state machine to view the workflow instances and comment on it
* On the creation of workflow it will appear in the inbox of all employees that have roles that can perform any state transitioning actions in this state.
* Once an instance is marked to an individual employee it will appear only in that employees inbox although point 1 will still hold true and all others participating in the workflow can still search it and act if they have necessary action available to them
* If the instance is marked to a person who cannot perform any state transitioning action, they can still comment/upload and mark to anyone else.
* **Overall SLA :** SLA for the complete processing of the application/Entity
* **State level SLA:** SLA for a particular state in the workflow  

| **Environment Variables** | **Description** |
| :--- | :--- |
| egov.wf.default.offset | The default value of offset in search |
| egov.wf.default.limit | The default value of limit in search |
| egov.wf.max.limit | Maximum number of records that are returned in search response |
| egov.wf.inbox.assignedonly | Boolean flag if set to _true_ default search will return records assigned to the user only, if _false_ it will return all the records based on user’s role. _\(default search is the search call when no query params are sent and based on the RequestInfo of the call, records are returned, it’s used to show applications in employee inbox\)_ |
| egov.wf.statelevel | Boolean flag set to _true_ if statelevel workflow is required |

### Interaction Diagram: <a id="Interaction-Diagram:"></a>

![](blob:https://digit-discuss.atlassian.net/448394c3-ba08-49e2-b7f2-b0a91b9b58db#media-blob-url=true&id=00a48d7e-a191-463b-8a2d-94819a5e083e&collection=contentId-664174657&contextId=664174657&mimeType=image%2Fpng&name=Screen%20Shot%202019-01-23%20at%202.59.24%20AM.png&size=176193&width=1540&height=1058)

### Deployment Details <a id="Deployment-Details"></a>

1. Deploy latest version of egov-workflow-v2 service
2. Add businessService persister yaml path in persister configuration
3. Add Role-Action mapping for BusinessService API’s
4. Overwrite the egov.wf.statelevel flag \( _true_ for state level and _false_ for tenant level\)
5. Create businessService \(workflow configuration\) according to product requirements
6. Add Role-Action mapping for _/processInstance/\_search_ API
7.  Add workflow persister yaml path in persister configuration

### Configuration Details <a id="Configuration-Details"></a>

For Configuration details please refer to the links in Reference Docs

### Integration  <a id="Integration"></a>

#### Integration Scope <a id="Integration-Scope"></a>

The workflow configuration can be used by any module which performs a sequence of operations on an application/Entity. It can be used to simulate and track processes in organisations to make it more efficient to and increase the accountability.

#### Integration Benefits <a id="Integration-Benefits"></a>

* Role based workflow.
* Easy way of writing rule.
* File movement within workflow roles.

#### Steps to Integration <a id="Steps-to-Integration"></a>

1. To integrate, host of egov-workflow-v2 should be overwritten in helm chart
2. /process/\_search should be added as the search endpoint for searching workflow processsInstance object .
3. /process/\_transition should be added to perform an action on a application._\(It’s for internal use in modules and should not be added in Role-Action mapping\)_
4. The workflow configuration can be fetched by calling _\_search_ API to check if data can be updated or not in the current state

### Reference Docs <a id="Reference-Docs"></a>

#### Doc Links <a id="Doc-Links"></a>

| **Title**  | **Link** |
| :--- | :--- |
| Configuring Workflows For New Product/Entity |  [Configuring Workflows For New Product/Entity](https://digit-discuss.atlassian.net/wiki/spaces/DD/pages/644481051) |
|  Setting Up Workflows |  [Setting Up Workflows](https://digit-discuss.atlassian.net/wiki/spaces/DD/pages/644546619/Setting+Up+Workflows) |
| API Swagger Documentation | [Swagger Documentation](https://raw.githubusercontent.com/egovernments/core-services/master/docs/worfklow-2.0) |
| Migration to Workflow 2.0 | [Workflow 2.0 Configuration doc](https://digit-discuss.atlassian.net/wiki/spaces/EPE/pages/120619031/Workflow+2.0+Configuration+doc) |

#### API List <a id="API-List"></a>

|  | **Link** |
| :--- | :--- |
|  _/businessservice/\_create_ | [https://www.getpostman.com/collections/8552e3de40c819e34190](https://www.getpostman.com/collections/8552e3de40c819e34190) |
|  _/businessservice/\_update_ |  [https://www.getpostman.com/collections/8552e3de40c819e34190](https://www.getpostman.com/collections/8552e3de40c819e34190) |
| _/businessservice/\_search_ | [https://www.getpostman.com/collections/8552e3de40c819e34190](https://www.getpostman.com/collections/8552e3de40c819e34190) |
| _/process/\_transition_ | [https://www.getpostman.com/collections/8552e3de40c819e34190](https://www.getpostman.com/collections/8552e3de40c819e34190) |
| _/process/\_search_ | [https://www.getpostman.com/collections/8552e3de40c819e34190](https://www.getpostman.com/collections/8552e3de40c819e34190) |

_\(Note: All the API’s are in the same postman collection therefore same link is added in each row\)_

