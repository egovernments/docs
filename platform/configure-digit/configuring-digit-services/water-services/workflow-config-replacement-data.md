---
description: Migration Document for Bill Amendment W&S
---

# Workflow Config-Replacement Data

## Overview

This document contains the steps to create new workflow configs specific to WS and SW modules for Bill Amendment.

## Steps

Create the new Workflow configs in the same tenant-Id as the one you want to replace in the applications.\
\
New configs for WS and SW bill amendment are as follows:

**Curl for WS Bill Amendment Config:**

```
curl --location --request POST 'https://egov-micro-qa.egovernments.org/egov-workflow-v2/egov-wf/businessservice/_create' \
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
        "authToken": "",
        "userInfo": {
            "id": 73,
            "userName": null,
            "name": null,
            "type": "EMPLOYEE",
            "mobileNumber": null,
            "emailId": null,
            "roles": [
                {
                    "id": 2,
                    "name": "Customer Support Representative",
                    "code": null,
                    "tenantId": null
                }
            ],
            "tenantId": null,
            "uuid": "uuid"
        }
    },
    "BusinessServices": [
        {
            "tenantId": "pb.amritsar",
            "businessService": "WS.AMENDMENT",
            "business": "WS",
            "businessServiceSla": 0,
            "states": [
                {
                    "tenantId": "pb.amritsar",
                    "sla": null,
                    "state": null,
                    "applicationStatus": "INWORKFLOW",
                    "docUploadRequired": false,
                    "isStartState": true,
                    "isTerminateState": false,
                    "isStateUpdatable": false,
                    "actions": [
                        {
                            "tenantId": "pb.amritsar",
                            "action": "OPEN",
                            "nextState": "APPROVALPENDING",
                            "roles": [
                                "CITIZEN",
                                "SW_CEMP",
                                "WS_CEMP"
                            ],
                            "active": true
                        }
                    ]
                },
                {
                    "uuid": "APPROVALPENDING",
                    "tenantId": "pb.amritsar",
                    "sla": null,
                    "state": "APPROVALPENDING",
                    "applicationStatus": "INWORKFLOW",
                    "docUploadRequired": false,
                    "isStartState": true,
                    "isTerminateState": false,
                    "isStateUpdatable": false,
                    "actions": [
                        {
                            "tenantId": "pb.amritsar",
                            "currentState": "APPROVALPENDING",
                            "action": "APPROVE",
                            "nextState": "APPROVED",
                            "roles": [
                                "WS_APPROVER",
                                "SW_APPROVER"
                            ],
                            "active": true
                        },
                        {
                            "tenantId": "pb.amritsar",
                            "currentState": "APPROVALPENDING",
                            "action": "REJECT",
                            "nextState": "REJECTED",
                            "roles": [
                                "WS_APPROVER",
                                "SW_APPROVER"
                            ],
                            "active": true
                        },
                        {
                            "tenantId": "pb.amritsar",
                            "currentState": "APPROVALPENDING",
                            "action": "SEND_BACK",
                            "nextState": "PENDING_FOR_CITIZEN_ACTION",
                            "roles": [
                                "WS_APPROVER",
                                "SW_APPROVER"
                            ],
                            "active": true
                        }
                    ]
                },
                {
                    "tenantId": "pb.amritsar",
                    "sla": null,
                    "state": "REJECTED",
                    "applicationStatus": "INACTIVE",
                    "docUploadRequired": false,
                    "isStartState": false,
                    "isTerminateState": true,
                    "isStateUpdatable": false,
                    "actions": null
                },
                {
                    "tenantId": "pb.amritsar",
                    "sla": null,
                    "state": "APPROVED",
                    "applicationStatus": "ACTIVE",
                    "docUploadRequired": false,
                    "isStartState": false,
                    "isTerminateState": true,
                    "isStateUpdatable": false,
                    "actions": null
                },
                {
                    "uuid": "PENDING_FOR_CITIZEN_ACTION",
                    "tenantId": "pb.amritsar",
                    "sla": null,
                    "state": "PENDING_FOR_CITIZEN_ACTION",
                    "applicationStatus": "INWORKFLOW",
                    "docUploadRequired": false,
                    "isStartState": false,
                    "isTerminateState": false,
                    "isStateUpdatable": true,
                    "actions": [
                        {
                            "tenantId": "pb.amritsar",
                            "currentState": "PENDING_FOR_CITIZEN_ACTION",
                            "action": "RE-SUBMIT",
                            "nextState": "APPROVALPENDING",
                            "roles": [
                                "CITIZEN",
                                "SW_CEMP",
                                "WS_CEMP"
                            ],
                            "active": true
                        }
                    ]
                }
            ]
        }
    ]
}'
```

**Curl for SW Bill Amendment Config:**

```
curl --location --request POST 'https://egov-micro-qa.egovernments.org/egov-workflow-v2/egov-wf/businessservice/_create' \
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
        "authToken": "",
        "userInfo": {
            "id": 73,
            "userName": null,
            "name": null,
            "type": "EMPLOYEE",
            "mobileNumber": null,
            "emailId": null,
            "roles": [
                {
                    "id": 2,
                    "name": "Customer Support Representative",
                    "code": null,
                    "tenantId": null
                }
            ],
            "tenantId": null,
            "uuid": "uuid"
        }
    },
    "BusinessServices": [
        {
            "tenantId": "pb.amritsar",
            "businessService": "SW.AMENDMENT",
            "business": "SW",
            "businessServiceSla": 0,
            "states": [
                {
                    "tenantId": "pb.amritsar",
                    "sla": null,
                    "state": null,
                    "applicationStatus": "INWORKFLOW",
                    "docUploadRequired": false,
                    "isStartState": true,
                    "isTerminateState": false,
                    "isStateUpdatable": false,
                    "actions": [
                        {
                            "tenantId": "pb.amritsar",
                            "action": "OPEN",
                            "nextState": "APPROVALPENDING",
                            "roles": [
                                "CITIZEN",
                                "SW_CEMP",
                                "WS_CEMP"
                            ],
                            "active": true
                        }
                    ]
                },
                {
                    "uuid": "APPROVALPENDING",
                    "tenantId": "pb.amritsar",
                    "sla": null,
                    "state": "APPROVALPENDING",
                    "applicationStatus": "INWORKFLOW",
                    "docUploadRequired": false,
                    "isStartState": true,
                    "isTerminateState": false,
                    "isStateUpdatable": false,
                    "actions": [
                        {
                            "tenantId": "pb.amritsar",
                            "currentState": "APPROVALPENDING",
                            "action": "APPROVE",
                            "nextState": "APPROVED",
                            "roles": [
                                "WS_APPROVER",
                                "SW_APPROVER"
                            ],
                            "active": true
                        },
                        {
                            "tenantId": "pb.amritsar",
                            "currentState": "APPROVALPENDING",
                            "action": "REJECT",
                            "nextState": "REJECTED",
                            "roles": [
                                "WS_APPROVER",
                                "SW_APPROVER"
                            ],
                            "active": true
                        },
                        {
                            "tenantId": "pb.amritsar",
                            "currentState": "APPROVALPENDING",
                            "action": "SEND_BACK",
                            "nextState": "PENDING_FOR_CITIZEN_ACTION",
                            "roles": [
                                "WS_APPROVER",
                                "SW_APPROVER"
                            ],
                            "active": true
                        }
                    ]
                },
                {
                    "tenantId": "pb.amritsar",
                    "sla": null,
                    "state": "REJECTED",
                    "applicationStatus": "INACTIVE",
                    "docUploadRequired": false,
                    "isStartState": false,
                    "isTerminateState": true,
                    "isStateUpdatable": false,
                    "actions": null
                },
                {
                    "tenantId": "pb.amritsar",
                    "sla": null,
                    "state": "APPROVED",
                    "applicationStatus": "ACTIVE",
                    "docUploadRequired": false,
                    "isStartState": false,
                    "isTerminateState": true,
                    "isStateUpdatable": false,
                    "actions": null
                },
                {
                    "uuid": "PENDING_FOR_CITIZEN_ACTION",
                    "tenantId": "pb.amritsar",
                    "sla": null,
                    "state": "PENDING_FOR_CITIZEN_ACTION",
                    "applicationStatus": "INWORKFLOW",
                    "docUploadRequired": false,
                    "isStartState": false,
                    "isTerminateState": false,
                    "isStateUpdatable": true,
                    "actions": [
                        {
                            "tenantId": "pb.amritsar",
                            "currentState": "PENDING_FOR_CITIZEN_ACTION",
                            "action": "RE-SUBMIT",
                            "nextState": "APPROVALPENDING",
                            "roles": [
                                "CITIZEN",
                                "SW_CEMP",
                                "WS_CEMP"
                            ],
                            "active": true
                        }
                    ]
                }
            ]
        }
    ]
}'
```

eg:--

List all the states from the process instances of the old workflow(business service) config.\
**select uuid,state  from eg\_wf\_state\_v2 where businessserviceid=(select UUID from eg\_wf\_businessservice\_v2 where businessservice='BS.AMENDMENT' and tenantid='pb');**

| **uuid**                             | **state**                     |
| ------------------------------------ | ----------------------------- |
| 94055bb3-210c-4184-93ac-99e288ab00d9 |                               |
| b0fc6007-8b02-4753-8e50-1fdb29e559da | APPROVALPENDING               |
| b9ea9101-09ff-4a8e-97c1-d43b3311af73 | REJECTED                      |
| ea5668ee-d8db-4c16-839b-64299e12f8fc | APPROVED                      |
| 468ce854-e19d-4a0f-97a0-66745f2034af | PENDING\_FOR\_CITIZEN\_ACTION |

List the states from the new business service created for replacement using this query\
_**SELECT UUID, state FROM eg\_wf\_state where businessService='WS.AMENDMENT' AND business='WS**_' _**AND tenantid='pb'**_

_**SELECT UUID, state FROM eg\_wf\_state where businessService='SW.AMENDMENT' AND business='SW**_' _**AND tenantid='pb'**_

| **uuid** | **state**                     |
| -------- | ----------------------------- |
| New uuid |                               |
| New uuid | APPROVALPENDING               |
| New uuid | REJECTED                      |
| New uuid | APPROVED                      |
| New uuid | PENDING\_FOR\_CITIZEN\_ACTION |

&#x20;Replace the state-ids of the old workflow in the **eg\_wf\_processinstance** table with stateids of the new workflow.

Write an update query **(one for each state UUID)** to rewrite the process-instance table, as shown above - \
_**update eg\_wf\_processinstance\_v2 set status={new state uuid} AND businessservice={WS.AMENDMENT}  and modulename={WS} where businessservice={BS.AMENDMENT} and status={old state uuid}  and businessid like '%WS%';**_

_**update eg\_wf\_processinstance\_v2 set status={new state uuid} AND businessservice={SW.AMENDMENT}  and modulename={SW} where businessservice={BS.AMENDMENT} and status={old state uuid}  and businessid like '%SW%';**_\


<figure><img src="../../../../.gitbook/assets/image (159).png" alt=""><figcaption></figcaption></figure>

{% hint style="info" %}
**Note:** businessid like '%SW% or businessid like '%WS% will be used depending on the New businessService that you are using. moduleName in the above query would take WS or SW in sync with the new businessService
{% endhint %}

* _The **status** and **businessservice** columns should be set to the new values from the newly created business-service master create based on the old status and id of the process-Instance._
* Rename or delete the old business service **(BS.AMENDMENT)** to avoid any of the applications using it wrongly in future. \
  {update eg\_wf\_businessservice set businessservice='**BS.AMENDMENT**-**deprecated**' where businessservice='**BS.AMENDMENT**'}
* UI/BACKEND will have to replace their configs to fetch the workflow configs for WS and SW.\
  Changes required from UI:\
  _Bill Amendment Workflow \_create and \_update APIs_ - replace _**businessservice**_ **BS.AMENDMENT** with **WS.AMENDMENT**/**SW.AMENDMENT** and _**moduleName**_ **BS** with **WS/SW** as per the requirement.\
  _Bill Amendment Inbox_ - replace _**businessservice**_ **BS.AMENDMENT** with **WS.AMENDMENT**/**SW.AMENDMENT** as per the requirement.

\
