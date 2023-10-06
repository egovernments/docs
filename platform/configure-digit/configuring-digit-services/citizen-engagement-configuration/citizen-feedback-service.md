---
description: Citizen feedback service configuration details
---

# Citizen Feedback Service

## Overview

This document is a guide to create a new Survey as well as to create Responses.

## Sample Configuration

To create a new survey, use following **\_create** api:

```
curl --location 'http://localhost:8280/service-request/service/definition/v1/_create' \
--header 'Content-Type: application/json' \
--data '{
    "RequestInfo": {
        "apiId": "Rainmaker",
        "authToken": "f1737fa6-8ae3-4476-8279-b966406c6066",
        "userInfo": {
            "id": 12033,
            "uuid": "5b0db5f1-5695-4ce4-ab81-f185a28bfa62",
            "userName": "QAWSCE",
            "name": "WS Counter Employee",
            "type": "EMPLOYEE",
            "roles": [
                {
                    "name": "PT Counter Employee",
                    "code": "PT_CEMP",
                    "tenantId": "pb.amritsar"
                },
                {
                    "name": "WS Counter Employee",
                    "code": "WS_CEMP",
                    "tenantId": "pb.amritsar"
                },
                {
                    "name": "SW Counter Employee",
                    "code": "SW_CEMP",
                    "tenantId": "pb.amritsar"
                }
            ],
            "tenantId": "pb.amritsar"
        },
        "msgId": "1669381536763|en_IN",
        "plainAccessRequest": {}
    },
    "ServiceDefinition": {
        "tenantId": "pb.amritsar",
        "code": "PT_PAYMENT",
        "module": "PT",
        "isActive": true,
        "attributes": [
            {
                "tenantId": "pb.amritsar",
                "code": "consumerCode",
                "dataType": "String",
                "values": null,
                "required": true,
                "isActive": true,
                "regex": null,
                "order": "1",
                "additionalDetails": {}
            },
            {
                "tenantId": "pb.amritsar",
                "code": "referenceId",
                "dataType": "String",
                "values": null,
                "required": true,
                "isActive": true,
                "reGex": null,
                "order": "2",
                "additionalDetails": {}
            },
            {
                "tenantId": "pb.amritsar",
                "code": "rating",
                "dataType": "Number",
                "values": null,
                "required": true,
                "isActive": true,
                "reGex": "^[1-5]*$",
                "order": "3",
                "additionalDetails": {}
            },
            {
                "tenantId": "pb.amritsar",
                "code": "comments",
                "dataType": "Text",
                "values": null,
                "required": true,
                "isActive": true,
                "reGex": null,
                "order": "4",
                "additionalDetails": {}
            },
            {
                "tenantId": "pb.amritsar",
                "code": "channel",
                "dataType": "SingleValueList",
                "values": ["Sms", "Online", "InApp"],
                "required": true,
                "isActive": true,
                "reGex": null,
                "order": "5",
                "additionalDetails": {}
            }
        ],
        "additionalDetails": {
        },
        "clientId": "f1737fa6-8ae3-4476-8279-b966406c6066"
    }
}'
```

The `ServiceDefinition` object requires following properties:

* _**"tenantId"**_ => Takes tenantid
* _**"code": "PT\_PAYMENT"**_ => This shall contain the name of the survey, usually corresponding to the name of the flow for which the survey is being created,
* _**"module": "PT"**_ => This denotes the module name for which the survey is to be created,
* _**"isActive": true**_ => This would tell if the survey is isActive or not,
* _**"attributes "**_ => This would contain multiple objects each of which will be a linked to a Question/ property. This question would be mentioned in the `"code"` property.

Currently Surveys have been created for PT module. We have 4 surveys : PT\_CREATE, PT\_UPDATE, PT\_MUTATION, PT\_PAYMENT.



#### Creating New Survey Response: <a href="#creating-new-survey-response" id="creating-new-survey-response"></a>

To create a survey response(i.e. user response to survey), use following **\_create** api:

```
curl --location 'http://localhost:8280/service-request/service/v1/_create' \
--header 'Content-Type: application/json' \
--data '{
    "RequestInfo": {
        "apiId": "Rainmaker",
        "authToken": "f1737fa6-8ae3-4476-8279-b966406c6066",
        "userInfo": {
            "id": 12033,
            "uuid": "5b0db5f1-5695-4ce4-ab81-f185a28bfa62",
            "userName": "QAWSCE",
            "name": "WS Counter Employee",
            "type": "EMPLOYEE",
            "roles": [
                {
                    "name": "PT Counter Employee",
                    "code": "PT_CEMP",
                    "tenantId": "pb.amritsar"
                },
                {
                    "name": "WS Counter Employee",
                    "code": "WS_CEMP",
                    "tenantId": "pb.amritsar"
                },
                {
                    "name": "SW Counter Employee",
                    "code": "SW_CEMP",
                    "tenantId": "pb.amritsar"
                }
            ],
            "tenantId": "pb.amritsar"
        },
        "msgId": "1669381536763|en_IN",
        "plainAccessRequest": {}
    },
    "Service": {
        "tenantId": "pb.amritsar",
        "serviceDefId": "7fe72b01-32fc-4baa-8024-166f5367a93a",
        "isActive": true,
        "attributes": [
            {
                "attributeCode": "consumerCode",
                "value": "PB-PT-1234",
                "additionalDetails": {}
            },
            {
                "attributeCode": "referenceId",
                "value": "REF-1",
                "additionalDetails": {}
            },
            {
                "attributeCode": "rating",
                "value": 4,
                "additionalDetails": {}
            },
            {
                "attributeCode": "comments",
                "value": "10256",
                "additionalDetails": {}
            },
            {
                "attributeCode": "channel",
                "value": "Online",
                "additionalDetails": {}
            }
        ],
        "additionalDetails": {
        },
        "accountId" : "5b0db5f1-5695-4ce4-ab81-f185a28bfa62"
    }
}'
```

The `Service` object requires following properties:

* _**"tenantId"**_ => Takes tenantid
* _**"serviceDefId": "7fe72b01-32fc-4baa-8024-166f5367a93a"**_ => This takes the id of the survey for which the response has to be created,
* _**"isActive": true**_ => This would tell if the survey is active or not,
* _**"attributes "**_ => This would contain multiple objects related to the answer to the questions in the survey.

## Reference Docs

For searching existing surveys or their response use \_search APIS from the below collection.

Postman-collection : [https://api.postman.com/collections/19481088-f3d5018c-aad2-46de-a5a9-609d2acb1e6e?access\_key=PMAT-01GVN63T0S1B6G641TD5DWF12P](https://api.postman.com/collections/19481088-f3d5018c-aad2-46de-a5a9-609d2acb1e6e?access\_key=PMAT-01GVN63T0S1B6G641TD5DWF12P)

