---
description: National dashboard KPIs
---

# New KPIs

## Overview

We have added 3 new KPIs as per requirements. The following are the KPIs:

1. **Average Property Tax Collected:** This represents the average tax collected by each property. This is calculated by the formula- (Total property tax collected  / Total number of properties paid). This KPI is added in the National Dashboard Property Tax screen on the overview card.
2. **Total Non-Tax Collection:**  This is the sum of all non-tax revenue collections such as ( Trade licenses, Building plan approval, miscellaneous receipts, etc..)This KPI can be found in the National Dashboard Overview Screen on the overview card.
3. **Total Non-Tax Revenue Contribution:**  This represents the percentage contribution of the total non-tax revenue over total revenue. This is calculated by the formula -   (Total non-tax collected/Total revenue collected) x 100. This KPI can also be found in the National Dashboard Overview Screen on the overview card.

The updated screens for these KPIs have been added to the [National Dashboard Overview](national-dashboard-ingest-service/) and [Property Tax ](property-tax-national-dashboard.md)docs.

## Assumptions

1. In each module, we cannot bifurcate the tax and nontax heads. Eg: PT tax including cess consider as one Tax head.
2. The average property tax paid is decided based on the number of payment transactions. If the same property is paid 2 times for different financial years, we consider these two transactions.
3. Tax and Non Tax includes arrears, penalty, exemption etc.
4. Mcollect: Here many tax heads are there. All are considered non-tax heads.
5. Re-indexing is required to the existing data for "Average property tax Paid" Kpi.
6. Each payment is assumed to be separate (PT), and partial payment is also considered a single payment
7. Data can only be considered from today or existing national DSS data should be reindexed
8. Mappings for the new property should be considered Long&#x20;
9. Long or decimal-amount fields.
10. Build and commit to division operation required for PT avg tax KPI.

## Steps

Follow the steps below to implement the new KPIs.\
\
**Step 1:**  Add the config changes in the **ChartApiConfig.json** file in the [configs](https://github.com/egovernments/configs/tree/UAT) repository.   Newly added configs can be referred to from [here](https://github.com/egovernments/configs/blob/17bec4912246fa073c212c3d440dbed7e47abb88/egov-dss-dashboards/dashboard-analytics/ChartApiConfig.json#L18200-L18445).

&#x20;**Step 2:**  Add the config placement in the **MasterDashboardConfig.json** file.   Placement configs can be referred from 2 places in the file:

1. For National Dashboard Overview KPIs in the Overview card refer [here](https://github.com/egovernments/configs/blob/17bec4912246fa073c212c3d440dbed7e47abb88/egov-dss-dashboards/dashboard-analytics/MasterDashboardConfig.json#L337-L352).
2. For property tax KPI refer [here](https://github.com/egovernments/configs/blob/17bec4912246fa073c212c3d440dbed7e47abb88/egov-dss-dashboards/dashboard-analytics/MasterDashboardConfig.json#L1046-L1053).

**Step 3:**  Add the newly added property: **noOfPropertiesPaidToday** to the PT  **module-fields-mapping** in the DevOps, in the respective environment file, refer [here](https://github.com/egovernments/DIGIT-DevOps/blob/a94e465d8f3bd5f29a0bf4c76f37611d2934f9f1/deploy-as-code/helm/environments/uat.yaml#L340).

Updated PT fields: "PT":{"transactions":"array::number","todaysTotalApplications":"number","todaysClosedApplications":"number","assessments":"number","assessedProperties":"array::number","propertiesRegistered":"array::number","todaysCollection":"array::number","propertyTax":"array::number","cess":"array::number","rebate":"array::number","penalty":"array::number","interest":"array::number"**,"noOfPropertiesPaidToday":"number"**}

&#x20;**Step 4:** Update the index mapping in Kibana as follows:

{% code lineNumbers="true" %}
```
PUT pt-national-dashboard/_mapping/nss
{
 "properties" : {
          "assessedPropertiesForUsageCategory" : {
            "type" : "long"
          },
          "assessments" : {
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
          }
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
                "type" : "keyword"
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

**Step 5:** Re-indexing pt-national-dashboard

**Step 6:**  Code-level changes are required in dashboard analytics as well to implement the **“division”**  logic. Add the change as listed [here](https://github.com/egovernments/DIGIT-Dev/blob/90d151a56659627211734bd8c6aa093886540f6b/business-services/dashboard-analytics/src/main/java/com/tarento/analytics/handler/MetricChartResponseHandler.java#L191-L202). Refer to [this](https://github.com/egovernments/DIGIT-Dev/blob/90d151a56659627211734bd8c6aa093886540f6b/business-services/dashboard-analytics/src/main/java/com/tarento/analytics/handler/IResponseHandler.java#L87) file for adding constants.    Following is the build: **dashboard-analytics:v1.1.8\_beta-9dabbb1f7c-107**

&#x20;**Step 7:** Upsert the localisations for the new KPIs as follows:

{% code lineNumbers="true" %}
```
curl --location -g --request POST '{{url}}/localization/messages/v1/_upsert' \
--header 'Content-Type: application/json' \
--data-raw '{
    "RequestInfo": {
        "apiId": "emp",
        "ver": "1.0",
        "ts": "10-03-2017 00:00:00",
        "action": "create",
        "did": "1",
        "key": "abcdkey",
        "msgId": "20170310130900",
        "requesterId": "rajesh",
        "authToken": "a8dd019c-25db-4796-838a-51c31d1a4120",
        "userInfo": {
            "id": 128
        }
    },
    "tenantId": "pg",
    "messages": [
        {
            "code": "NATIONAL_PT_DSS_AVG_TAX_COLLECTION",
            "message": "Average Property Tax Collected",
            "module": "rainmaker-dss",
            "locale": "en_IN"
        },
        {
            "code": "TIP_NATIONAL_PT_DSS_AVG_TAX_COLLECTION",
            "message": "Total property tax collected  / Total number of properties",
            "module": "rainmaker-dss",
            "locale": "en_IN"
        },
        {
            "code": "DSS_TOTAL_NON_TAX_COLLECTION",
            "message": "Total Non-Tax Collection",
            "module": "rainmaker-dss",
            "locale": "en_IN"
        },
        {
            "code": "TIP_DSS_TOTAL_NON_TAX_COLLECTION",
            "message": "Sum of all non tax revenue collections such as ( Trade licenses , Building plan approval , miscellaneous receipts , etc..)",
            "module": "rainmaker-dss",
            "locale": "en_IN"
        },
        {
            "code": "DSS_NON_TAX_REVENUE_CONTRIBUTION",
            "message": "Non-Tax Revenue Contribution",
            "module": "rainmaker-dss",
            "locale": "en_IN"
        },
        {
            "code": "TIP_DSS_NON_TAX_REVENUE_CONTRIBUTION",
            "message": "(Total non-tax collected/Total revenue collected) x 100",
            "module": "rainmaker-dss",
            "locale": "en_IN"
        }
    ]
}'
```
{% endcode %}

**Step 8:**  Once these changes are implemented, restart the _**dashboard-analytics**_ and _**national-dashboard-ingest**_ by checking the Cluster-configs.

{% hint style="info" %}
_**Note:**_ Now the data can be ingested using an adapter. Step 8 is optional and should be used only for testing purposes.&#x20;
{% endhint %}

&#x20;**Step 9 (Optional Step - Only for testing purposes)**: Now you can upsert the new data for testing using \_ingest API. The curl for the same is as follows:

{% code lineNumbers="true" %}
```
curl --location --request POST 'http://localhost:8081/national-dashboard/metric/_ingest' \
--header 'Content-Type: application/json' \
--data-raw '{
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
            "date": "12-11-2022",
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

