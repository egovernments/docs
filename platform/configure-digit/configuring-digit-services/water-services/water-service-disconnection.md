# Water Service Disconnection

## **Overview**

After connection activation or legacy connection, the user can choose to disconnect the connection either temporarily or permanently. This process is based on a defined workflow. Any action is based on defined roles on the action level.&#x20;

## Configuration Details

For disconnecting the connection, the user needs to send extra parameters as below :

1. **disconnectionReason** - to add the reason for disconnection
2. **isDisconnectionTemporary** - Whether the disconnection is temporary or permanent (if the disconnection is temporary then isDisconnectionTemporary will be true else false)
3. **disconnectRequest** - This will always be true for disconnection applications.
4. **disconnectionExecutionDate** - This is the date when the application is disconnected.

and also user needs to upload some supporting documents and mandatory info.

**URLs for the external API references**

* eGov mdms: egov.mdms.host = [https://dev.digit.org](https://dev.digit.org/)/
* eGov -idGen: egov.idgen.host = [https://dev.digit.org](https://dev.digit.org/)/
* localization service: egov.localization.host = [https://dev.digit.org](https://dev.digit.org/)/
* idGen Id formats :\
  egov.idgen.wdcid.name=waterservice.disconnection.id\
  egov.idgen.wdcid.format=WS\_AP/\[CITY.CODE]/\[fy:yyyy-yy]/DC-\[SEQ\_WS\_APP\_\[TENANT\_ID]]

[<img src="https://github.com/fluidicon.png" alt="" data-size="line">egov-mdms-data/IdFormat.json at QA · egovernments/egov-mdms-data](https://github.com/egovernments/egov-mdms-data/blob/QA/data/pb/common-masters/IdFormat.json)

```
{
      "format": "WS_AP/[CITY.CODE]/[fy:yyyy-yy]/DC-[SEQ_WS_APP_[TENANT_ID]]",
      "idname": "waterservice.disconnection.id"
}
```

{% hint style="info" %}
This new feature is developed using the same existing base APIs for new and modified connections. The changes for disconnection follow a similar approach as that of New Connection. The config and persister changes required are mentioned below.
{% endhint %}

**Persister configuration**

Some changes are required in the existing persister files which can be referred to from the following links:

{% embed url="https://github.com/egovernments/configs/blob/UAT/egov-persister/water-persist.yml" %}

{% embed url="https://github.com/egovernments/configs/blob/UAT/egov-persister/water-meter.yml" %}

**Workflow config for edit connection**

Create businessService (workflow configuration) using the  `/businessservice/_create`. Following is the product configuration for editing the water connection.

```
curl --location --request POST 'https://dev.digit.org/egov-workflow-v2/egov-wf/businessservice/_create' \
--header 'Content-Type: application/json' \
--data-raw '{
	"RequestInfo": {
		"apiId": "Rainmaker",
		"action": "",
		"did": 1,
		"key": "",
		"msgId": "20170310130900|en_IN",
		"requesterId": "",
		"ts": 1513579888683,
		"ver": ".01",
		"authToken": "{{Auth_Token}}"
	},
	"BusinessServices": [
		{
			"tenantId": "pb",
			"businessService": "DisconnectWSConnection",
			"business": "ws-services",
			"businessServiceSla": 259200000,
			"states": [
				{
					"sla": null,
					"state": null,
					"applicationStatus": null,
					"docUploadRequired": false,
					"isStartState": true,
					"isTerminateState": false,
					"isStateUpdatable": true,
					"actions": [
						{
							"action": "INITIATE",
							"nextState": "INITIATED",
							"roles": [
								"CITIZEN",
								"WS_CEMP"
							]
						}
					]
				},
				{
					"sla": null,
					"state": "INITIATED",
					"applicationStatus": "INITIATED",
					"docUploadRequired": false,
					"isStartState": false,
					"isTerminateState": false,
					"isStateUpdatable": true,
					"actions": [
						{
							"action": "SUBMIT_APPLICATION",
							"nextState": "PENDING_FOR_DOCUMENT_VERIFICATION",
							"roles": [
								"CITIZEN",
								"WS_CEMP"
							]
						}
					]
				},
				{
					"sla": null,
					"state": "PENDING_FOR_DOCUMENT_VERIFICATION",
					"applicationStatus": "PENDING_FOR_DOCUMENT_VERIFICATION",
					"docUploadRequired": false,
					"isStartState": false,
					"isTerminateState": false,
					"isStateUpdatable": true,
					"actions": [
						{
							"action": "VERIFY_AND_FORWARD",
							"nextState": "PENDING_FOR_FIELD_INSPECTION",
							"roles": [
								"WS_DOC_VERIFIER"
							]
						},
						{
							"action": "SEND_BACK",
							"nextState": "PENDING_FOR_COUNTER_EMPLOYEE_ACTION",
							"roles": [
								"WS_DOC_VERIFIER"
							]
						},
						{
							"action": "SEND_BACK_TO_CITIZEN",
							"nextState": "PENDING_FOR_CITIZEN_ACTION",
							"roles": [
								"WS_DOC_VERIFIER"
							]
						}
					]
				},
				{
					"sla": null,
					"state": "PENDING_FOR_FIELD_INSPECTION",
					"applicationStatus": "PENDING_FOR_FIELD_INSPECTION",
					"docUploadRequired": false,
					"isStartState": false,
					"isTerminateState": false,
					"isStateUpdatable": true,
					"actions": [
						{
							"action": "VERIFY_AND_FORWARD",
							"nextState": "PENDING_APPROVAL_FOR_DISCONNECTION",
							"roles": [
								"WS_FIELD_INSPECTOR"
							]
						},
						{
							"action": "SEND_BACK_FOR_DOCUMENT_VERIFICATION",
							"nextState": "PENDING_FOR_DOCUMENT_VERIFICATION",
							"roles": [
								"WS_FIELD_INSPECTOR"
							]
						},
						{
							"action": "SEND_BACK_TO_CITIZEN",
							"nextState": "PENDING_FOR_CITIZEN_ACTION",
							"roles": [
								"WS_FIELD_INSPECTOR"
							]
						},
						{
							"action": "REJECT",
							"nextState": "REJECTED",
							"roles": [
								"WS_FIELD_INSPECTOR"
							]
						}
					]
				},
				{
					"sla": null,
					"state": "PENDING_APPROVAL_FOR_DISCONNECTION",
					"applicationStatus": "PENDING_APPROVAL_FOR_DISCONNECTION",
					"docUploadRequired": false,
					"isStartState": false,
					"isTerminateState": false,
					"isStateUpdatable": false,
					"actions": [
						{
							"action": "SEND_BACK_FOR_FIELD_INSPECTION",
							"nextState": "PENDING_FOR_FIELD_INSPECTION",
							"roles": [
								"WS_APPROVER"
							]
						},
						{
							"action": "SEND_BACK_TO_CITIZEN",
							"nextState": "PENDING_FOR_CITIZEN_ACTION",
							"roles": [
								"WS_APPROVER"
							]
						},
						{
							"action": "APPROVE_FOR_DISCONNECTION",
							"nextState": "PENDING_FOR_PAYMENT",
							"roles": [
								"WS_APPROVER"
							]
						},
						{
							"action": "REJECT",
							"nextState": "REJECTED",
							"roles": [
								"WS_APPROVER"
							]
						}
					]
				},
				{
					"sla": null,
					"state": "PENDING_FOR_CITIZEN_ACTION",
					"applicationStatus": "PENDING_FOR_CITIZEN_ACTION",
					"docUploadRequired": false,
					"isStartState": false,
					"isTerminateState": false,
					"isStateUpdatable": true,
					"actions": [
						{
							"action": "RESUBMIT_APPLICATION",
							"nextState": "PENDING_FOR_DOCUMENT_VERIFICATION",
							"roles": [
								"CITIZEN",
								"WS_CEMP"
							]
						}
					]
				},
				{
					"sla": null,
					"state": "PENDING_FOR_COUNTER_EMPLOYEE_ACTION",
					"applicationStatus": "PENDING_FOR_COUNTER_EMPLOYEE_ACTION",
					"docUploadRequired": false,
					"isStartState": true,
					"isTerminateState": false,
					"isStateUpdatable": true,
					"actions": [
						{
							"action": "RESUBMIT_APPLICATION",
							"nextState": "PENDING_FOR_DOCUMENT_VERIFICATION",
							"roles": [
								"CITIZEN",
								"WS_CEMP"
							]
						}
					]
				},
				{
					"sla": null,
					"state": "REJECTED",
					"applicationStatus": "REJECTED",
					"docUploadRequired": false,
					"isStartState": false,
					"isTerminateState": true,
					"isStateUpdatable": false,
					"actions": null
				},
				{
					"sla": null,
					"state": "PENDING_FOR_PAYMENT",
					"applicationStatus": "PENDING_FOR_PAYMENT",
					"docUploadRequired": false,
					"isStartState": false,
					"isTerminateState": false,
					"isStateUpdatable": false,
					"actions": [
						{
							"action": "PAY",
							"nextState": "PENDING_FOR_DISCONNECTION_EXECUTION",
							"roles": [
								"CITIZEN",
								"WS_CEMP"
							]
						}
					]
				},
				{
					"sla": null,
					"state": "PENDING_FOR_DISCONNECTION_EXECUTION",
					"applicationStatus": "PENDING_FOR_DISCONNECTION_EXECUTION",
					"docUploadRequired": false,
					"isStartState": false,
					"isTerminateState": false,
					"isStateUpdatable": true,
					"actions": [
						{
							"action": "EXECUTE_DISCONNECTION",
							"nextState": "DISCONNECTION_EXECUTED",
							"roles": [
								"WS_CLERK"
							]
						}
					]
				},
				{
					"sla": null,
					"state": "DISCONNECTION_EXECUTED",
					"applicationStatus": "DISCONNECTION_EXECUTED",
					"docUploadRequired": false,
					"isStartState": false,
					"isTerminateState": true,
					"isStateUpdatable": false,
					"actions": null
				}
			]
		}
	]
}'
```

### **Notifications**

Disconnection notifications will be sent to the property owners and connection holders based on different application states.

### **Capturing Connection Holders**

We can add connection holders to the water connection which will be the owner of the connection. We can fill in the connection holders' details or we can just make the property owner as the connection holder. It goes the same for disconnection applications.

The connection holder will get a notification based on a different state of the application. We are pushing the data of the connection holders in the user service too.

## Integration Steps  <a href="#steps-to-integration" id="steps-to-integration"></a>

1. To integrate, the host of ws-service module should be overwritten in the helm chart.
2. &#x20;`/ws-services/wc/_create` should be added as the create endpoint for creating water application/connection in the system
3. &#x20;`/ws-services/wc/_search` should be added as the search endpoint. This method handles all requests to search existing records depending on different search criteria
4. &#x20;`/ws-services/wc/_update` should be added as the update endpoint. This method is used to update fields in existing records or to update the status of applications based on workflow.

## Reference Docs <a href="#reference-docs" id="reference-docs"></a>

#### API List <a href="#api-list" id="api-list"></a>

| <h4 id="title"><strong>Title</strong> </h4> | **Link**                                                                                                                   |
| ------------------------------------------- | -------------------------------------------------------------------------------------------------------------------------- |
|  _/ws-services/wc/\_create_                 | [https://www.getpostman.com/collections/1d4b9edc95f83a9427eb](https://www.getpostman.com/collections/1d4b9edc95f83a9427eb) |
| _/ws-services/wc/\_update_                  | [https://www.getpostman.com/collections/1d4b9edc95f83a9427eb](https://www.getpostman.com/collections/1d4b9edc95f83a9427eb) |
| _/ws-services/wc/\_search_                  | [https://www.getpostman.com/collections/1d4b9edc95f83a9427eb](https://www.getpostman.com/collections/1d4b9edc95f83a9427eb) |

_(Note: All the APIs are in the same postman collection therefore the same link is added in each row)_\
\
