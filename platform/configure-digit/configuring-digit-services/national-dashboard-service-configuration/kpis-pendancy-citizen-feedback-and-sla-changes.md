---
description: New properties added for property tax module
---

# KPIs: Pendancy, Citizen Feedback & SLA Changes

## Overview

This page provides the DevOps details for new properties added to the property tax module. Follow the steps given in the section below to add the new properties to the module.

## Steps

**Step 1:** Add the following properties in the PT index: pt-national-dashboard:

```
"PT":{"transactions":"array::number","todaysTotalApplications":"number","todaysClosedApplications":"number","assessments":"number","assessedProperties":"array::number","propertiesRegistered":"array::number","todaysCollection":"array::number","propertyTax":"array::number","cess":"array::number","rebate":"array::number","penalty":"array::number","interest":"array::number","noOfPropertiesPaidToday":"number","todaysApplicationsWithinSLA":"number","todaysMovedApplications":"array::number"}
```

Here “todaysApplicationsWithinSLA": "number", "todaysMovedApplications": "array::number" need to be added.\
[Click here](https://github.com/egovernments/DIGIT-DevOps/blob/e27ebd66f344e461d4c3ccfd0e3edf1a14aa0ea2/deploy-as-code/helm/environments/uat.yaml#L341) for the reference link.

{% hint style="info" %}
**Note**: For other modules, the property _“todaysClosedApplications”_ may be missing. Make sure to add that as well.
{% endhint %}

**Step 2: Add the groupby mapping** for todaysMovedApplications i.e. applicationStatus\
"PT":{"financialYear", "usageCategory", "<mark style="color:red;">applicationStatus</mark>"}. Add the one marked in red.\
\
[Click here](https://github.com/egovernments/DIGIT-DevOps/blob/e27ebd66f344e461d4c3ccfd0e3edf1a14aa0ea2/deploy-as-code/helm/environments/uat.yaml#L343) for the reference link.&#x20;

## Definitions

* _**todaysApplicationsWithinSLA**_: It denotes the number of applications that have been closed/ have completed the workflow today.
* _**todaysMovedApplications**_: It is an array of application statuses moved today.
* _**todaysMovedApplicationsForApplicationStatus**_: It represents the number of applications(total count) that have been moved today for a particular application status.
* _**applicationStatus**_: It is a string value that contains the current status of the application. Eg:\
  ”applicationStatus” : “APPROVED“

## **Citizen-Feedback-National-Dashboard - Changes**

**Step 1: Add module-index-mapping** for the citizen-feedback-national-dashboard index in both places given below.

* [https://github.com/egovernments/DIGIT-DevOps/blob/b8a15d760b91314399c2f31f25931fa5cb053928/deploy-as-code/helm/environments/uat.yaml#L339](https://github.com/egovernments/DIGIT-DevOps/blob/b8a15d760b91314399c2f31f25931fa5cb053928/deploy-as-code/helm/environments/uat.yaml#L339)
* [https://github.com/egovernments/DIGIT-DevOps/blob/b8a15d760b91314399c2f31f25931fa5cb053928/deploy-as-code/helm/charts/core-services/national-dashboard-kafka-pipeline/values.yaml#L14](https://github.com/egovernments/DIGIT-DevOps/blob/b8a15d760b91314399c2f31f25931fa5cb053928/deploy-as-code/helm/charts/core-services/national-dashboard-kafka-pipeline/values.yaml#L14)

**Step 2: Add module-fields-mapping**

**Reference:** [https://github.com/egovernments/DIGIT-DevOps/blob/b8a15d760b91314399c2f31f25931fa5cb053928/deploy-as-code/helm/environments/uat.yaml#L341](https://github.com/egovernments/DIGIT-DevOps/blob/b8a15d760b91314399c2f31f25931fa5cb053928/deploy-as-code/helm/environments/uat.yaml#L341)

**Step 3: Add master-module-fields-mapping**

**Reference:** [https://github.com/egovernments/DIGIT-DevOps/blob/b8a15d760b91314399c2f31f25931fa5cb053928/deploy-as-code/helm/environments/uat.yaml#L342](https://github.com/egovernments/DIGIT-DevOps/blob/b8a15d760b91314399c2f31f25931fa5cb053928/deploy-as-code/helm/environments/uat.yaml#L342)

**Step 3: Add groupby mapping** _for_ Channel

`"CF":{"channel"}`

**Reference:** [https://github.com/egovernments/DIGIT-DevOps/blob/b8a15d760b91314399c2f31f25931fa5cb053928/deploy-as-code/helm/environments/uat.yaml#L343](https://github.com/egovernments/DIGIT-DevOps/blob/b8a15d760b91314399c2f31f25931fa5cb053928/deploy-as-code/helm/environments/uat.yaml#L343)

### **Index changes**

* **Pt-national-dashboard:** Update pt-national-dashboard index mapping so as to add 2 new properties_**:**_ todaysApplicationsWithinSLA, todaysMovedApplicationsForApplicationStatus

{% code lineNumbers="true" %}
```
PUT pt-national-dashboard/_mapping/nss
{
  "properties" : {
          "applicationStatus" : {
            "type" : "text",
            "fields" : {
              "keyword" : {
                "type" : "keyword",
                "ignore_above" : 256
              }
            }
          },
          "assessedPropertiesForUsageCategory" : {
            "type" : "long"
          },
          "assessments" : {
            "type" : "long"
          },
          "avgTaxCollectedPerProperty" : {
            "type" : "long"
          },
          "cessForUsageCategory" : {
            "type" : "long"
          },
          "createdBy" : {
            "type" : "text",
            "fields" : {
              "keyword" : {
                "type" : "keyword",
                "ignore_above" : 256
              }
            }
          },
          "createdTime" : {
            "type" : "long"
          },
          "date" : {
            "type" : "date",
            "format" : "dd-MM-yyyy HH:mm:ss||dd-MM-yyyy||epoch_millis||dd-MM-yyyy'T'HH:mm:ss.SSSZ"
          },
          "financialYear" : {
            "type" : "text",
            "fields" : {
              "keyword" : {
                "type" : "keyword",
                "ignore_above" : 256
              }
            }
          },
          "interestForUsageCategory" : {
            "type" : "long"
          },
          "lastModifiedBy" : {
            "type" : "text",
            "fields" : {
              "keyword" : {
                "type" : "keyword",
                "ignore_above" : 256
              }
            }
          },
          "lastModifiedTime" : {
            "type" : "long"
          },
          "module" : {
            "type" : "text",
            "fields" : {
              "keyword" : {
                "type" : "keyword",
                "ignore_above" : 256
              }
            }
          },
          "noOfPropertiesPaidToday" : {
            "type" : "long"
          },
          "nonTaxCollections" : {
            "type" : "text",
            "fields" : {
              "keyword" : {
                "type" : "keyword",
                "ignore_above" : 256
              }
            }
          },
          "penaltyForUsageCategory" : {
            "type" : "long"
          },
          "propertiesRegisteredForFinancialYear" : {
            "type" : "long"
          },
          "propertyTaxForUsageCategory" : {
            "type" : "long"
          },
          "rebateForUsageCategory" : {
            "type" : "long"
          },
          "region" : {
            "type" : "text",
            "fields" : {
              "keyword" : {
                "type" : "keyword",
                "ignore_above" : 256
              }
            }
          },
          "state" : {
            "type" : "text",
            "fields" : {
              "keyword" : {
                "type" : "keyword",
                "ignore_above" : 256
              }
            }
          },
          "taxCollections" : {
            "type" : "text",
            "fields" : {
              "keyword" : {
                "type" : "keyword",
                "ignore_above" : 256
              }
            }
          },
          "todaysApplicationsWithinSLA" : {
            "type" : "long"
          },
          "todaysClosedApplications" : {
            "type" : "long"
          },
          "todaysCollectionForNonTaxCollections" : {
            "type" : "long"
          },
          "todaysCollectionForTaxCollections" : {
            "type" : "long"
          },
          "todaysCollectionForUsageCategory" : {
            "type" : "long"
          },
          "todaysMovedApplications" : {
            "type" : "long"
          },
          "todaysMovedApplicationsForApplicationStatus" : {
            "type" : "long"
          },
          "todaysTotalApplications" : {
            "type" : "long"
          },
          "totalApplicationsPaidTheTax" : {
            "type" : "long"
          },
          "transactionsForUsageCategory" : {
            "type" : "long"
          },
          "ulb" : {
            "type" : "text",
            "fields" : {
              "keyword" : {
                "type" : "keyword",
                "ignore_above" : 256
              }
            }
          },
          "usageCategory" : {
            "type" : "text",
            "fields" : {
              "keyword" : {
                "type" : "keyword",
                "ignore_above" : 256
              }
            }
          },
          "ward" : {
            "type" : "text",
            "fields" : {
              "keyword" : {
                "type" : "keyword",
                "ignore_above" : 256
              }
            }
          }
        }
}
```
{% endcode %}

Ingest API -

* Port-forward national dashboard ingest service and hit the below curl.
* This should result in the ingestion of data for the date provided in the request body.

{% code lineNumbers="true" %}
```
curl --location 'http://localhost:8081/national-dashboard/metric/_ingest' \
--header 'Content-Type: application/json' \
--data '{
    "RequestInfo": {
        "apiId": "asset-services",
        "ver": null,
        "ts": null,
        "action": null,
        "did": null,
        "key": null,
        "msgId": "search with from and to values",
        "authToken": "f5f22a04-ba52-4616-9e13-734bce63a15c",
        "userInfo": {
            "id": 11227,
            "uuid": "151cb3c7-3713-4e15-b9a1-3babd6d5e5a9",
            "userName": "UATPTSU",
            "name": "PT Super User",
            "mobileNumber": "8990877667",
            "emailId": "",
            "locale": null,
            "type": "EMPLOYEE",
            "roles": [
                {
                    "name": "NDA SYSTEM",
                    "code": "NDA_SYSTEM",
                    "tenantId": "pg.citya"
                },
                {
                    "name": "PT Counter Employee",
                    "code": "PT_CEMP",
                    "tenantId": "pg.citya"
                },
                {
                    "name": "Property Approver",
                    "code": "PROPERTY_APPROVER",
                    "tenantId": "pg.citya"
                },
                {
                    "name": "PT Doc Verifier",
                    "code": "PT_DOC_VERIFIER",
                    "tenantId": "pg.citya"
                },
                {
                    "name": "Property Tax Receipt Cancellator",
                    "code": "CR_PT",
                    "tenantId": "pg.citya"
                },
                {
                    "name": "PT Counter Approver",
                    "code": "PT_APPROVER",
                    "tenantId": "pg.citya"
                },
                {
                    "name": "PT Field Inspector",
                    "code": "PT_FIELD_INSPECTOR",
                    "tenantId": "pg.citya"
                },
                {
                    "name": "Property Verifier",
                    "code": "PROPERTY_VERIFIER",
                    "tenantId": "pg.citya"
                }
            ],
            "active": true,
            "tenantId": "pg.citya",
            "permanentCity": null
        }
    },
    "Data": [
        {
            "date": "03-04-2023",
            "module": "PT",
            "ward": "Block 1",
            "ulb": "pb.amritsar",
            "region": "Amritsar-MC",
            "state": "Punjab",
            "metrics": {
                "assessments": 29,
                "todaysTotalApplications": 62,
                "todaysClosedApplications": 21,
                "noOfPropertiesPaidToday": 10,
                "todaysApplicationsWithinSLA" : 12,
                "propertiesRegistered": [
                    {
                        "groupBy": "financialYear",
                        "buckets": [
                            {
                                "name": "2018-19",
                                "value": 12
                            },
                            {
                                "name": "2019-20",
                                "value": 18
                            },
                            {
                                "name": "2020-21",
                                "value": 21
                            },
                            {
                                "name": "2021-22",
                                "value": 43
                            },
                            {
                                "name": "2022-23",
                                "value": 64
                            }
                        ]
                    }
                ],
                "assessedProperties": [
                    {
                        "groupBy": "usageCategory",
                        "buckets": [
                            {
                                "name": "RESIDENTIAL",
                                "value": 21
                            },
                            {
                                "name": "COMMERCIAL",
                                "value": 11
                            },
                            {
                                "name": "INDUSTRIAL",
                                "value": 13
                            }
                        ]
                    }
                ],
                "transactions": [
                    {
                        "groupBy": "usageCategory",
                        "buckets": [
                            {
                                "name": "RESIDENTIAL",
                                "value": 19
                            },
                            {
                                "name": "COMMERCIAL",
                                "value": 13
                            },
                            {
                                "name": "INDUSTRIAL",
                                "value": 13
                            }
                        ]
                    }
                ],
                "todaysCollection": [
                    {
                        "groupBy": "usageCategory",
                        "buckets": [
                            {
                                "name": "RESIDENTIAL",
                                "value": 16000
                            },
                            {
                                "name": "COMMERCIAL",
                                "value": 22500
                            },
                            {
                                "name": "INDUSTRIAL",
                                "value": 26000
                            }
                        ]
                    }
                ],
                "todaysMovedApplications": [
                    {
                        "groupBy": "applicationStatus",
                        "buckets": [
                            {
                                "name": "APPROVED",
                                "value": 21
                            },
                            {
                                "name": "CORRECTIONPENDING",
                                "value": 12
                            },
                            {
                                "name": "DOCVERIFIED",
                                "value": 5
                            },
                            {
                                "name": "FIELDVERIFIED",
                                "value": 2
                            },
                            {
                                "name": "OPEN",
                                "value": 11
                            },
                            {
                                "name": "PAID",
                                "value": 3
                            },
                            {
                                "name": "REJECTED",
                                "value": 2
                            },
                            {
                                "name": "INITIATED",
                                "value": 6
                            }
                        ]
                    }
                ],
                "propertyTax": [
                    {
                        "groupBy": "usageCategory",
                        "buckets": [
                            {
                                "name": "RESIDENTIAL",
                                "value": 1200
                            },
                            {
                                "name": "COMMERCIAL",
                                "value": 2100
                            },
                            {
                                "name": "INDUSTRIAL",
                                "value": 100
                            }
                        ]
                    }
                ],
                "cess": [
                    {
                        "groupBy": "usageCategory",
                        "buckets": [
                            {
                                "name": "RESIDENTIAL",
                                "value": 1300
                            },
                            {
                                "name": "COMMERCIAL",
                                "value": 1900
                            },
                            {
                                "name": "INDUSTRIAL",
                                "value": 1000
                            }
                        ]
                    }
                ],
                "rebate": [
                    {
                        "groupBy": "usageCategory",
                        "buckets": [
                            {
                                "name": "RESIDENTIAL",
                                "value": -500
                            },
                            {
                                "name": "COMMERCIAL",
                                "value": -1200
                            },
                            {
                                "name": "INDUSTRIAL",
                                "value": -900
                            }
                        ]
                    }
                ],
                "penalty": [
                    {
                        "groupBy": "usageCategory",
                        "buckets": [
                            {
                                "name": "RESIDENTIAL",
                                "value": 1300
                            },
                            {
                                "name": "COMMERCIAL",
                                "value": 1500
                            },
                            {
                                "name": "INDUSTRIAL",
                                "value": 1500
                            }
                        ]
                    }
                ],
                "interest": [
                    {
                        "groupBy": "usageCategory",
                        "buckets": [
                            {
                                "name": "RESIDENTIAL",
                                "value": 1900
                            },
                            {
                                "name": "COMMERCIAL",
                                "value": 1800
                            },
                            {
                                "name": "INDUSTRIAL",
                                "value": 600
                            }
                        ]
                    }
                ]
            }
        }
    ]
}'
```
{% endcode %}

### **Citizen-feedback-national-dashboard**

A new national dashboard index for citizen feedback is created.&#x20;

{% code lineNumbers="true" %}
```
PUT citizen-feedback-national-dashboard
{} 

PUT citizen-feedback-national-dashboard/_mapping/nss
{
  "properties": {
    "ulb": {
      "type": "text",
      "fields": {
        "keyword": {
          "type": "keyword",
          "ignore_above": 256
        }
      }
    },
    "state": {
      "type": "text",
      "fields": {
        "keyword": {
          "type": "keyword",
          "ignore_above": 256
        }
      }
    },
    "ward": {
      "type": "text",
      "fields": {
        "keyword": {
          "type": "keyword",
          "ignore_above": 256
        }
      }
    },
    "region": {
      "type": "text",
      "fields": {
        "keyword": {
          "type": "keyword",
          "ignore_above": 256
        }
      }
    },
    "module":{
      "type": "text",
      "fields": {
        "keyword": {
          "type": "keyword",
          "ignore_above": 256
        }
      }
    },
    "serviceType":{
      "type": "text",
      "fields": {
        "keyword": {
          "type": "keyword",
          "ignore_above": 256
        }
      }
    },
    "serviceModule":{
      "type": "text",
      "fields": {
        "keyword": {
          "type": "keyword",
          "ignore_above": 256
        }
      }
    },
    "channel": {
      "type": "text",
      "fields": {
        "keyword": {
          "type": "keyword",
          "ignore_above": 256
        }
      }
    },
    "todaysNoOfCitizenResponsesForChannel": {
      "type": "long"
    },
    "todaysAverageCitizenRating": {
      "type": "long"
    },
    "date": {
      "type": "date",
      "format": "dd-MM-yyyy HH:mm:ss||dd-MM-yyyy||epoch_millis||dd-MM-yyyy'T'HH:mm:ss.SSSZ"
    }
  }
}

```
{% endcode %}

Refer to the document [National Dashboard Ingest Service](national-dashboard-ingest-service/) to set up ingest API for Citizen Feedback National Dashboard Index.

Ingest API -

* Port-forward national dashboard ingest service and hit the below curl.
* This should result in the ingestion of data for the date provided in the request body.

{% code lineNumbers="true" %}
```
curl --location 'http://localhost:8081/national-dashboard/metric/_ingest' \
--header 'Content-Type: application/json' \
--data '{
    "RequestInfo": {
        "apiId": "asset-services",
        "ver": null,
        "ts": null,
        "action": null,
        "did": null,
        "key": null,
        "msgId": "search with from and to values",
        "authToken": "641ab660-3057-4593-b68b-95ea2ac6f653",
        "userInfo": {
            "id": 11227,
            "uuid": "151cb3c7-3713-4e15-b9a1-3babd6d5e5a9",
            "userName": "UATPTSU",
            "name": "PT Super User",
            "mobileNumber": "8990877667",
            "emailId": "",
            "locale": null,
            "type": "EMPLOYEE",
            "roles": [
                {
                    "name": "NDA SYSTEM",
                    "code": "NDA_SYSTEM",
                    "tenantId": "pg.citya"
                },
                {
                    "name": "PT Counter Employee",
                    "code": "PT_CEMP",
                    "tenantId": "pg.citya"
                },
                {
                    "name": "Property Approver",
                    "code": "PROPERTY_APPROVER",
                    "tenantId": "pg.citya"
                },
                {
                    "name": "PT Doc Verifier",
                    "code": "PT_DOC_VERIFIER",
                    "tenantId": "pg.citya"
                },
                {
                    "name": "Property Tax Receipt Cancellator",
                    "code": "CR_PT",
                    "tenantId": "pg.citya"
                },
                {
                    "name": "PT Counter Approver",
                    "code": "PT_APPROVER",
                    "tenantId": "pg.citya"
                },
                {
                    "name": "PT Field Inspector",
                    "code": "PT_FIELD_INSPECTOR",
                    "tenantId": "pg.citya"
                },
                {
                    "name": "Property Verifier",
                    "code": "PROPERTY_VERIFIER",
                    "tenantId": "pg.citya"
                }
            ],
            "active": true,
            "tenantId": "pg.citya",
            "permanentCity": null
        }
    },
    "Data": [
        {
            "date": "01-04-2023",
            "module": "CF",
            "ward": "Block 1",
            "ulb": "pb.amritsar",
            "region": "Amritsar-MC",
            "state": "Punjab",
            "metrics": {
                "serviceModule":"PT",
                "serviceType": "PT_CREATE",
                "todaysNoOfCitizenResponses": [
                    {
                        "groupBy": "channel",
                        "buckets": [
                            {
                                "name": "ONLINE",
                                "value": 12
                            },
                            {
                                "name": "COUNTER",
                                "value": 5
                            }
                        ]
                    }
                ],
                "todaysAverageCitizenRating": 4.5
            }
        }
    ]
}'
```
{% endcode %}

## **Configuration Details**

ChartApiConfigs.json: MasterChart\
Add the following configs.

{% code lineNumbers="true" %}
```
"nssPtSlaAchieved": {
    "chartName": "NATIONAL_DSS_PT_SLA_ACHIEVED",
    "queries": [
      {
        "module": "PT",
        "requestQueryMap": "{\"state\" : \"state.keyword\",\"ulb\" : \"ulb.keyword\",\"ward\" : \"ward.keyword\"}",
        "dateRefField": "date",
        "indexName": "pt-national-dashboard",
        "aggrQuery": "{\"aggs\":{\"AGGR\":{\"filter\":{\"bool\":{\"must\":[{\"term\":{\"applicationStatus.keyword\":\"APPROVED\"}}]}},\"aggs\":{\"stateApplicationsWithinSla\":{\"terms\":{\"field\":\"state.keyword\"},\"aggs\":{\"intermediateAggrULB\":{\"terms\":{\"field\":\"ulb.keyword\"},\"aggs\":{\"intermediateAggrWard\":{\"terms\":{\"field\":\"ward.keyword\"},\"aggs\":{\"days\":{\"terms\":{\"field\":\"date\"},\"aggs\":{\"applicationsSubmittedWithInSla\":{\"avg\":{\"field\":\"todaysApplicationsWithinSLA\"}}}},\"wardapplications\":{\"sum_bucket\":{\"buckets_path\":\"days.applicationsSubmittedWithInSla\"}}}},\"ulbApplications\":{\"sum_bucket\":{\"buckets_path\":\"intermediateAggrWard.wardapplications\"}}}},\"stateApplications\":{\"sum_bucket\":{\"buckets_path\":\"intermediateAggrULB.ulbApplications\"}}}},\"Total_Applications_Within_SLA\":{\"sum_bucket\":{\"buckets_path\":\"stateApplicationsWithinSla.stateApplications\"}},\"stateMovedApplications\":{\"terms\":{\"field\":\"state.keyword\"},\"aggs\":{\"intermediateAggrULB\":{\"terms\":{\"field\":\"ulb.keyword\"},\"aggs\":{\"intermediateAggrWard\":{\"terms\":{\"field\":\"ward.keyword\"},\"aggs\":{\"days\":{\"terms\":{\"field\":\"date\"},\"aggs\":{\"totalMovedApplications\":{\"avg\":{\"field\":\"todaysMovedApplicationsForApplicationStatus\"}}}},\"wardapplications\":{\"sum_bucket\":{\"buckets_path\":\"days.totalMovedApplications\"}}}},\"ulbApplications\":{\"sum_bucket\":{\"buckets_path\":\"intermediateAggrWard.wardapplications\"}}}},\"stateApplications\":{\"sum_bucket\":{\"buckets_path\":\"intermediateAggrULB.ulbApplications\"}}}},\"Total_Moved_Applications\":{\"sum_bucket\":{\"buckets_path\":\"stateMovedApplications.stateApplications\"}}}}}}"
      }
    ],
    "chartType": "metric",
    "valueType": "percentage",
    "drillChart": "none",
    "documentType": "nss",
    "action": "percentage",
    "isRoundOff": true,
    "aggregationPaths": [
      "Total_Applications_Within_SLA",
      "Total_Moved_Applications"
    ],
    "insight": {
      "chartResponseMap" : "nssPtSlaAchieved",
      "action" : "differenceOfNumbers",
      "upwardIndicator" : "positive",
      "downwardIndicator" : "negative",
      "textMessage" : "$indicator$value% than last $insightInterval",
      "colorCode" : "#228B22",
      "insightInterval" : "year",
      "isRoundOff": true
    },
    "_comment": " "
  },

  "nssPtPendancy": {
    "chartName": "NATIONAL_DSS_PT_PENDANCY",
    "queries": [
      {
        "module": "PT",
        "requestQueryMap": "{\"state\" : \"state.keyword\",\"ulb\" : \"ulb.keyword\",\"ward\" : \"ward.keyword\"}",
        "dateRefField": "date",
        "indexName": "pt-national-dashboard",
        "aggrQuery": "{\"aggs\":{\"all_matching_docs\":{\"filters\":{\"filters\":{\"all\":{\"match_all\":{}}}},\"aggs\":{\"stateClosedApplications\":{\"terms\":{\"field\":\"state.keyword\"},\"aggs\":{\"intermediateAggrULB\":{\"terms\":{\"field\":\"ulb.keyword\"},\"aggs\":{\"intermediateAggrWard\":{\"terms\":{\"field\":\"ward.keyword\"},\"aggs\":{\"days\":{\"terms\":{\"field\":\"date\"},\"aggs\":{\"applications\":{\"avg\":{\"field\":\"todaysClosedApplications\"}}}},\"wardapplications\":{\"sum_bucket\":{\"buckets_path\":\"days.applications\"}}}},\"ulbApplications\":{\"sum_bucket\":{\"buckets_path\":\"intermediateAggrWard.wardapplications\"}}}},\"stateApplications\":{\"sum_bucket\":{\"buckets_path\":\"intermediateAggrULB.ulbApplications\"}}}},\"Total_Closed_Applications\":{\"sum_bucket\":{\"buckets_path\":\"stateClosedApplications.stateApplications\"}},\"stateTotalApplications\":{\"terms\":{\"field\":\"state.keyword\"},\"aggs\":{\"intermediateAggrULB\":{\"terms\":{\"field\":\"ulb.keyword\"},\"aggs\":{\"intermediateAggrWard\":{\"terms\":{\"field\":\"ward.keyword\"},\"aggs\":{\"days\":{\"terms\":{\"field\":\"date\"},\"aggs\":{\"applications\":{\"avg\":{\"field\":\"todaysTotalApplications\"}}}},\"wardapplications\":{\"sum_bucket\":{\"buckets_path\":\"days.applications\"}}}},\"ulbApplications\":{\"sum_bucket\":{\"buckets_path\":\"intermediateAggrWard.wardapplications\"}}}},\"stateApplications\":{\"sum_bucket\":{\"buckets_path\":\"intermediateAggrULB.ulbApplications\"}}}},\"Total_Applications\":{\"sum_bucket\":{\"buckets_path\":\"stateTotalApplications.stateApplications\"}},\"Applications_Pending\":{\"bucket_script\":{\"buckets_path\":{\"total\":\"Total_Applications\",\"closed\":\"Total_Closed_Applications\"},\"script\":\"(params.total - params.closed) \"}}}}}}"
      }
    ],
    "chartType": "metric",
    "valueType": "percentage",
    "drillChart": "none",
    "documentType": "nss",
    "action": "percentage",
    "isRoundOff": true,
    "aggregationPaths": [
      "Applications_Pending",
      "Total_Applications"
    ],
    "insight": {
      "chartResponseMap" : "nssPtPendancy",
      "action" : "differenceOfNumbers",
      "upwardIndicator" : "positive",
      "downwardIndicator" : "negative",
      "textMessage" : "$indicator$value% than last $insightInterval",
      "colorCode" : "#228B22",
      "insightInterval" : "year",
      "isRoundOff": true
    },
    "_comment": " "
  },

  "nssOverviewPendancy": {
    "chartName": "NATIONAL_DSS_OVERVIEW_PENDANCY",
    "queries": [
      {
        "module": "PT",
        "requestQueryMap": "{\"state\" : \"state.keyword\",\"ulb\" : \"ulb.keyword\",\"ward\" : \"ward.keyword\"}",
        "dateRefField": "date",
        "indexName": "pt-national-dashboard",
        "aggrQuery": "{\"aggs\":{\"all_matching_docs\":{\"filters\":{\"filters\":{\"all\":{\"match_all\":{}}}},\"aggs\":{\"stateClosedApplications\":{\"terms\":{\"field\":\"state.keyword\"},\"aggs\":{\"intermediateAggrULB\":{\"terms\":{\"field\":\"ulb.keyword\"},\"aggs\":{\"intermediateAggrWard\":{\"terms\":{\"field\":\"ward.keyword\"},\"aggs\":{\"days\":{\"terms\":{\"field\":\"date\"},\"aggs\":{\"applications\":{\"avg\":{\"field\":\"todaysClosedApplications\"}}}},\"wardapplications\":{\"sum_bucket\":{\"buckets_path\":\"days.applications\"}}}},\"ulbApplications\":{\"sum_bucket\":{\"buckets_path\":\"intermediateAggrWard.wardapplications\"}}}},\"stateApplications\":{\"sum_bucket\":{\"buckets_path\":\"intermediateAggrULB.ulbApplications\"}}}},\"Total_Closed_Applications\":{\"sum_bucket\":{\"buckets_path\":\"stateClosedApplications.stateApplications\"}},\"stateTotalApplications\":{\"terms\":{\"field\":\"state.keyword\"},\"aggs\":{\"intermediateAggrULB\":{\"terms\":{\"field\":\"ulb.keyword\"},\"aggs\":{\"intermediateAggrWard\":{\"terms\":{\"field\":\"ward.keyword\"},\"aggs\":{\"days\":{\"terms\":{\"field\":\"date\"},\"aggs\":{\"applications\":{\"avg\":{\"field\":\"todaysTotalApplications\"}}}},\"wardapplications\":{\"sum_bucket\":{\"buckets_path\":\"days.applications\"}}}},\"ulbApplications\":{\"sum_bucket\":{\"buckets_path\":\"intermediateAggrWard.wardapplications\"}}}},\"stateApplications\":{\"sum_bucket\":{\"buckets_path\":\"intermediateAggrULB.ulbApplications\"}}}},\"Total_Applications\":{\"sum_bucket\":{\"buckets_path\":\"stateTotalApplications.stateApplications\"}},\"Applications_Pending\":{\"bucket_script\":{\"buckets_path\":{\"total\":\"Total_Applications\",\"closed\":\"Total_Closed_Applications\"},\"script\":\"(params.total - params.closed) \"}}}}}}"
      },
      {
        "module": "TL",
        "requestQueryMap": "{\"state\" : \"state.keyword\",\"ulb\" : \"ulb.keyword\",\"ward\" : \"ward.keyword\"}",
        "dateRefField": "date",
        "indexName": "tl-national-dashboard",
        "aggrQuery": "{\"aggs\":{\"all_matching_docs\":{\"filters\":{\"filters\":{\"all\":{\"match_all\":{}}}},\"aggs\":{\"stateClosedApplications\":{\"terms\":{\"field\":\"state.keyword\"},\"aggs\":{\"intermediateAggrULB\":{\"terms\":{\"field\":\"ulb.keyword\"},\"aggs\":{\"intermediateAggrWard\":{\"terms\":{\"field\":\"ward.keyword\"},\"aggs\":{\"days\":{\"terms\":{\"field\":\"date\"},\"aggs\":{\"applications\":{\"avg\":{\"field\":\"todaysClosedApplications\"}}}},\"wardapplications\":{\"sum_bucket\":{\"buckets_path\":\"days.applications\"}}}},\"ulbApplications\":{\"sum_bucket\":{\"buckets_path\":\"intermediateAggrWard.wardapplications\"}}}},\"stateApplications\":{\"sum_bucket\":{\"buckets_path\":\"intermediateAggrULB.ulbApplications\"}}}},\"Total_Closed_Applications\":{\"sum_bucket\":{\"buckets_path\":\"stateClosedApplications.stateApplications\"}},\"stateTotalApplications\":{\"terms\":{\"field\":\"state.keyword\"},\"aggs\":{\"intermediateAggrULB\":{\"terms\":{\"field\":\"ulb.keyword\"},\"aggs\":{\"intermediateAggrWard\":{\"terms\":{\"field\":\"ward.keyword\"},\"aggs\":{\"days\":{\"terms\":{\"field\":\"date\"},\"aggs\":{\"applications\":{\"avg\":{\"field\":\"todaysApplications\"}}}},\"wardapplications\":{\"sum_bucket\":{\"buckets_path\":\"days.applications\"}}}},\"ulbApplications\":{\"sum_bucket\":{\"buckets_path\":\"intermediateAggrWard.wardapplications\"}}}},\"stateApplications\":{\"sum_bucket\":{\"buckets_path\":\"intermediateAggrULB.ulbApplications\"}}}},\"Total_Applications\":{\"sum_bucket\":{\"buckets_path\":\"stateTotalApplications.stateApplications\"}},\"Applications_Pending\":{\"bucket_script\":{\"buckets_path\":{\"total\":\"Total_Applications\",\"closed\":\"Total_Closed_Applications\"},\"script\":\"(params.total - params.closed) \"}}}}}}"
      }
    ],
    "chartType": "metric",
    "valueType": "percentage",
    "drillChart": "none",
    "documentType": "nss",
    "action": "percentage",
    "isRoundOff": true,
    "aggregationPaths": [
      "Applications_Pending",
      "Total_Applications"
    ],
    "insight": {
      "chartResponseMap" : "nssOverviewPendancy",
      "action" : "differenceOfNumbers",
      "upwardIndicator" : "positive",
      "downwardIndicator" : "negative",
      "textMessage" : "$indicator$value% than last $insightInterval",
      "colorCode" : "#228B22",
      "insightInterval" : "year",
      "isRoundOff": true
    },
    "_comment": " "
  },

  "nssPtCitizenFeedbackScore": {
    "chartName": "NATIONAL_DSS_PT_CITIZEN_FEEDBACK_SCORE",
    "queries": [
      {
        "module": "CF",
        "requestQueryMap": "{\"state\" : \"state.keyword\",\"ulb\" : \"ulb.keyword\",\"ward\" : \"ward.keyword\"}",
        "dateRefField": "date",
        "indexName": "citizen-feedback-national-dashboard",
        "aggrQuery": "{\"aggs\":{\"AGGR\":{\"filter\":{\"bool\":{\"must\":[{\"term\":{\"serviceModule.keyword\":\"PT\"}}]}},\"aggs\":{\"Total Feedback Score\":{\"sum\":{\"script\":{\"lang\":\"painless\",\"inline\":\"doc['todaysAverageCitizenRating'].value * doc['todaysNoOfCitizenResponsesForChannel'].value\"}}},\"Total Number of Responses\":{\"sum\":{\"field\":\"todaysNoOfCitizenResponsesForChannel\"}}}}}}"
      }
    ],
    "chartType": "metric",
    "valueType": "number",
    "drillChart": "none",
    "documentType": "nss",
    "action": "division",
    "isRoundOff": true,
    "aggregationPaths": [
      "Total Feedback Score",
      "Total Number of Responses"
    ],
    "insight": {
      "chartResponseMap" : "nssPtCitizenFeedbackScore",
      "action" : "differenceOfNumbers",
      "upwardIndicator" : "positive",
      "downwardIndicator" : "negative",
      "textMessage" : "$indicator$value% than last $insightInterval",
      "colorCode" : "#228B22",
      "insightInterval" : "year",
      "isRoundOff": true
    },
    "_comment": " "
  },
  
  "nssOverviewCitizenFeedbackScore": {
    "chartName": "NATIONAL_DSS_OVERVIEW_CITIZEN_FEEDBACK_SCORE",
    "queries": [
      {
        "module": "CF",
        "requestQueryMap": "{\"state\" : \"state.keyword\",\"ulb\" : \"ulb.keyword\",\"ward\" : \"ward.keyword\"}",
        "dateRefField": "date",
        "indexName": "citizen-feedback-national-dashboard",
        "aggrQuery": "{\"aggs\":{\"AGGR\":{\"filter\":{\"bool\":{\"must\":[{\"term\":{\"serviceModule.keyword\":\"PT\"}}]}},\"aggs\":{\"Total Feedback Score\":{\"sum\":{\"script\":{\"lang\":\"painless\",\"inline\":\"doc['todaysAverageCitizenRating'].value * doc['todaysNoOfCitizenResponsesForChannel'].value\"}}},\"Total Number of Responses\":{\"sum\":{\"field\":\"todaysNoOfCitizenResponsesForChannel\"}}}}}}"
      }
    ],
    "chartType": "metric",
    "valueType": "number",
    "drillChart": "none",
    "documentType": "nss",
    "action": "division",
    "isRoundOff": true,
    "aggregationPaths": [
      "Total Feedback Score",
      "Total Number of Responses"
    ],
    "insight": {
      "chartResponseMap" : "nssOverviewCitizenFeedbackScore",
      "action" : "differenceOfNumbers",
      "upwardIndicator" : "positive",
      "downwardIndicator" : "negative",
      "textMessage" : "$indicator$value% than last $insightInterval",
      "colorCode" : "#228B22",
      "insightInterval" : "year",
      "isRoundOff": true
    },
    "_comment": " "
  },
  
   "nssPtCitizenServiceDeliveryIndex": {
    "chartName": "NATIONAL_DSS_PT_CITIZEN_SERVICE_DELIVERY_INDEX",
    "queries": [
      {
        "module": "PT",
        "requestQueryMap": "{\"state\" : \"state.keyword\",\"ulb\" : \"ulb.keyword\",\"ward\" : \"ward.keyword\"}",
        "dateRefField": "date",
        "indexName": "pt-national-dashboard",
        "aggrQuery": "{\"aggs\": {\"all_matching_docs\": {\"filters\": {\"filters\": {\"all\": {\"match_all\": {}}}},\"aggs\": {\"state\":{\"terms\": {\"field\": \"state.keyword\",\"size\": 10000},\"aggs\": {\"ulb\": {\"terms\": {\"field\": \"ulb.keyword\",\"size\": 10000},\"aggs\": {\"ward\": {\"terms\": {\"field\": \"ward.keyword\",\"size\": 10000},\"aggs\": {\"SlaintermediateAggr\": {\"terms\": {\"field\": \"date\",\"size\": 10000},\"aggs\": {\"applicationsSubmittedWithInSla\": {\"avg\": {\"field\": \"todaysApplicationsWithinSLA\"}}}},\"Total_Applications_Within_SLA\": {\"sum_bucket\": {\"buckets_path\": \"SlaintermediateAggr.applicationsSubmittedWithInSla\"}},\"app\": {\"filter\": {\"bool\": {\"must\":[{\"match\":{\"applicationStatus.keyword\" : \"APPROVED\"}}]}},\"aggs\": {\"totalapplication\": {\"sum\": {\"field\": \"todaysMovedApplicationsForApplicationStatus\"}}}},\"aggregatedsla\": {\"bucket_script\": {\"buckets_path\": {\"total\": \"app.totalapplication\",\"withinsla\": \"Total_Applications_Within_SLA\"},\"script\": \"((params.withinsla / params.total) * 100)*0.5\"}}}}}}}}}}}}"
      },
      {
        "module": "CF",
        "requestQueryMap": "{\"state\" : \"state.keyword\",\"ulb\" : \"ulb.keyword\",\"ward\" : \"ward.keyword\"}",
        "dateRefField": "date",
        "indexName": "citizen-feedback-national-dashboard",
        "aggrQuery": "{\"aggs\":{\"AGGR\":{\"filter\":{\"bool\": {\"must\": [{\"term\": {\"serviceModule.keyword\": \"PT\"}}]}},\"aggs\": {\"all_matching_docs\": {\"filters\": {\"filters\": {\"all\": {\"match_all\": {}}}},\"aggs\": {\"state\": {\"terms\": {\"field\": \"state.keyword\",\"size\": 10000},\"aggs\": {\"ulb\": {\"terms\": {\"field\": \"ulb.keyword\",\"size\": 10000},\"aggs\": {\"ward\": {\"terms\": {\"field\": \"ward.keyword\",\"size\": 10000},\"aggs\": {\"TotalFeedbackScore\": {\"sum\": {\"script\": {\"lang\": \"painless\",\"inline\": \"doc['todaysAverageCitizenRating'].value * doc['todaysNoOfCitizenResponsesForChannel'].value\"}}},\"TotalNumberofResponses\": {\"sum\": {\"field\": \"todaysNoOfCitizenResponsesForChannel\"}},\"avgfeedback\": {\"bucket_script\": {\"buckets_path\": {\"response\": \"TotalNumberofResponses\",\"feedbak\": \"TotalFeedbackScore\"},\"script\": \"((params.response / params.feedbak) * 100)*0.5\"}}}}}}}}}}}}}}"
      }
    ],
    "chartType": "metric",
    "valueType": "number",
    "drillChart": "none",
    "documentType": "nss",
    "action": "",
    "isRoundOff": true,
    "aggregationPaths": [
      "aggregatedsla",
      "avgfeedback"
    ],
    "insight": {
      "chartResponseMap" : "nssPtCitizenServiceDeliveryIndex",
      "action" : "differenceOfNumbers",
      "upwardIndicator" : "positive",
      "downwardIndicator" : "negative",
      "textMessage" : "$indicator$value% than last $insightInterval",
      "colorCode" : "#228B22",
      "insightInterval" : "year",
      "isRoundOff": true
    },
    "_comment": " "
  }
```
{% endcode %}

MasterDashboardConfig.json

* [Landing Screen](https://github.com/egovernments/configs/blob/c43b8f46884194bf50bfccb99e089a90df9e7bfd/egov-dss-dashboards/dashboard-analytics/MasterDashboardConfig.json#L8525-L8548)
* [Overview Screen](https://github.com/egovernments/configs/blob/c43b8f46884194bf50bfccb99e089a90df9e7bfd/egov-dss-dashboards/dashboard-analytics/MasterDashboardConfig.json#L496-L519)
* [PT Screen](https://github.com/egovernments/configs/blob/c43b8f46884194bf50bfccb99e089a90df9e7bfd/egov-dss-dashboards/dashboard-analytics/MasterDashboardConfig.json#L1303-L1334)

### Landing Page

<figure><img src="../../../../.gitbook/assets/image (585).png" alt=""><figcaption></figcaption></figure>

### Overview Page

<div align="left">

<figure><img src="../../../../.gitbook/assets/image (586).png" alt="" width="398"><figcaption></figcaption></figure>

</div>

### PT National Dashboard

<div align="left">

<figure><img src="../../../../.gitbook/assets/image (587).png" alt="" width="401"><figcaption></figcaption></figure>

</div>

### **Configure KPIs For Other Modules - Steps** <a href="#how-to-configure-the-above-kpis-for-other-modules" id="how-to-configure-the-above-kpis-for-other-modules"></a>

Find the details below on how to configure the following KPIs in other modules -

**SLA KPI** - 2 Properties to be added in individual module national dashboard indexes as explained above -

* todaysApplicationsWithinSLA
* todaysMovedApplicationsForApplicationStatus

**Pendancy KPI -** Property already present for the Property Tax module, but would be added for other modules if not present as explained above.

* todaysClosedApplications

**Citizen Feedback Score and Citizen Delivery Index KPI** - The Citizen Feedback National Dashboard Index added above for Property Tax will handle data for other modules as well.

To present data for other modules [Citizen Feedback service](https://digit-discuss.atlassian.net/wiki/spaces/DD/pages/2322104328) linked [here](https://github.com/egovernments/DIGIT-Dev/pull/5201) should be integrated with your individual modules.

**Adapter Level Changes Required for the above KPIs - {Link to Adapter Doc}**

