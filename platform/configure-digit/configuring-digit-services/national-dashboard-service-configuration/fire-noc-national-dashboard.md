---
description: Technical Doc
---

# Fire NOC - National Dashboard

## **Overview**

DSS has two sides to it. One is the process in which the data is pooled to ElasticSearch and the other is the way it is fetched, aggregated, computed, transformed and sent across.

As this revolves around a variety of data sets, there is a need for making this configurable. This ensures that the process can be configured easily in case a new scenario is introduced.&#x20;

This document walks us through the steps on how to define the configurations for DSS state analytics for the Fire NOC module.

## Technical Details

**Analytics:** Microservice responsible for building, fetching, aggregating and computing the data on ElasticSearch to a consumable data response. This is later used for visualizations and graphical representations.&#x20;

**Analytics Configurations:** Analytics contains multiple configurations. Add the changes related to fire NOC in this dashboard analytics.\
Configuration file path: [<img src="https://github.com/fluidicon.png" alt="" data-size="line">configs/egov-dss-dashboards/dashboard-analytics at qa · egovernments/configs](https://github.com/egovernments/configs/tree/qa/egov-dss-dashboards/dashboard-analytics)\
Below is a list of configurations that need to be changed to run the fire NOC data analytics successfully.

1. &#x20;Chart API Configuration
2. &#x20;Master Dashboard Configuration
3. &#x20;Role Dashboard Mappings Configuration

**Chart API Configuration:** Each visualization has its properties. Each visualization comes from different data sources (Sometimes it is a combination of different data sources). To configure each visualization and its properties, we have a Chart API Configuration Document.

The Visualization Code, which happens to be the key, has its properties configured as a part of the configuration and are easily changeable.

Sample ChartApiConfiguration.json data for the Fire NOC -

```
"nssNOCTodaysCollection": {
    "chartName": "NSS_NOC_TODAYS_COLLECTION",
    "queries": [
      {
        "module": "FIRENOC",
        "dateRefField": "",
        "requestQueryMap": "{\"ward\" : \"ward.keyword\",\"ulb\" : \"ulb.keyword\"}",
        "indexName": "firenoc-national-dashboard",
        "aggrQuery": "{\"aggs\":{\"AGGR\":{\"filter\":{\"bool\":{\"must\":[{\"range\":{\"date\":{\"gt\":\"now-1d\/d\",\"lte\":\"now\"}}}]}},\"aggs\":{\"Todays Collection\":{\"sum\":{\"field\":\"todaysCollectionForPaymentMode\"}}}}}}"
      }
    ],
    "chartType": "metric",
    "valueType": "amount",
    "action": "",
    "drillChart": "none",
    "aggregationPaths": [
      "Todays Collection"
    ],
    "insight": {
      
    },
    "_comment": "NSS FIRE NOC todays collections "
  },
  "nssNOCTotalCollection": {
    "chartName": "NSS_NOC_TOTAL_COLLECTION",
    "queries": [
      {
        "module": "FIRENOC",
        "dateRefField": "date",
        "requestQueryMap": "{\"ward\" : \"ward.keyword\", \"ulb\" : \"ulb.keyword\"}",
        "indexName": "firenoc-national-dashboard",
        "aggrQuery": "{\"aggs\":{\"AGGR\":{\"filter\":{\"bool\":{}},\"aggs\":{\"Total Collection\":{\"sum\":{\"field\":\"todaysCollectionForPaymentMode\"}}}}}}"
      }
    ],
    "chartType": "metric",
    "valueType": "amount",
    "action": "",
    "drillChart": "none",
    "aggregationPaths": [
      "Total Collection"
    ],
    "insight": {
      "chartResponseMap" : "nocTotalCollection",
      "action" : "differenceOfNumbers",
      "upwardIndicator" : "positive",
      "downwardIndicator" : "negative",
      "textMessage" : "$indicator$value% than last $insightInterval",
      "colorCode" : "#228B22",
      "insightInterval" : "year"
    },
    "_comment": "NSS FIRE NOC Total collections "
  },
  
  "nssNOCTotalApplications": {
    "chartName": "NSS_NOC_TOTAL_APPLICATIONS",
    "queries": [
      {
        "module": "FIRENOC",
        "dateRefField": "date",
        "requestQueryMap": "{\"ward\" : \"ward.keyword\",\"ulb\" : \"ulb.keyword\"}",
        "indexName": "firenoc-national-dashboard",
        "aggrQuery": "{\"aggs\":{\"AGGR\":{\"filter\":{\"bool\":{}},\"aggs\":{\"Total applications\":{\"sum\":{\"field\":\"todaysApplicationsForApplicationType\"}}}}}}"
      }
    ],
    "chartType": "metric",
    "valueType": "number",
    "action": "",
    "drillChart": "none",
    "aggregationPaths": [
      "Total applications"
    ],
    "insight": {
      "chartResponseMap" : "nocTotalApplications",
      "action" : "differenceOfNumbers",
      "upwardIndicator" : "positive",
      "downwardIndicator" : "negative",
      "textMessage" : "$indicator$value% than last $insightInterval",
      "colorCode" : "#228B22",
      "insightInterval" : "year"
    },
    "_comment": "NSS FIRE NOC Total applications "
  },
  
  "nssNOCActualIssued": {
    "chartName": "NSS_NOC_ACTUAL_ISSUED",
    "queries": [
      {
        "module": "FIRENOC",
        "dateRefField": "date",
        "requestQueryMap": "{\"ward\" : \"ward.keyword\",\"ulb\" : \"ulb.keyword\"}",
        "indexName": "firenoc-national-dashboard",
        "aggrQuery": "{\"aggs\":{\"AGGR\":{\"filter\":{\"bool\":{\"must\":[{\"term\":{\"applicationType.keyword\":\"NEW\"}}]}},\"aggs\":{\"Actual Noc's Issued\":{\"sum\":{\"field\":\"todaysApplicationsForApplicationType\"}}}}}}"
      }
    ],
    "chartType": "metric",
    "valueType": "number",
    "action": "",
    "drillChart": "none",
    "aggregationPaths": [
      "Actual Noc's Issued"
    ],
    "insight": {
      "chartResponseMap" : "nocActualIssued",
      "action" : "differenceOfNumbers",
      "upwardIndicator" : "positive",
      "downwardIndicator" : "negative",
      "textMessage" : "$indicator$value% than last $insightInterval",
      "colorCode" : "#228B22",
      "insightInterval" : "year"
    },
    "_comment": "NSS FIRE NOC Actual Issued "
  },
  
  "nssNOCCumulativeCollection": {
    "chartName": "NSS_NOC_TOTAL_CUMULATIVE_COLLECTION",
    "queries": [
      {
        "module": "FIRENOC",
        "dateRefField": "date",
        "requestQueryMap": "{\"ward\" : \"ward.keyword\",\"ulb\" : \"ulb.keyword\"}",
        "indexName": "firenoc-national-dashboard",
        "aggrQuery": "{\"aggs\":{\"AGGR\":{\"filter\":{\"bool\":{}},\"aggs\":{\"Collections\":{\"date_histogram\":{\"field\":\"date\",\"interval\":\"intervalvalue\"},\"aggs\":{\"Sum\":{\"sum\":{\"field\":\"todaysCollectionForPaymentMode\"}}}}}}}}"
      }
    ],
    "chartType": "line",
    "valueType": "amount",
    "action": "",
    "drillChart": "none",
    "documentType": "_doc",
    "aggregationPaths": [
      "Collections"
    ],
    "isCumulative": true,
    "interval": "month",
    "insight": {
    },
    "_comment": "NSS FIRE NOC Total cumulative collections "
  },
  
  "nssNOCAverageDaysToIssueProvisional": {
    "chartName": "NSS_NOC_AVERAGE_DAYS_TO_ISSUE_PROVISIONAL",
    "queries": [
      {
        "module": "FIRENOC",
        "dateRefField": "date",
        "requestQueryMap": "{\"ward\" : \"ward.keyword\",\"ulb\" : \"ulb.keyword\"}",
        "indexName": "firenoc-national-dashboard",
        "aggrQuery": "{\"aggs\":{\"AGGR\":{\"filter\":{\"bool\":{}},\"aggs\":{\"Average days to issue Provisional NOC\":{\"sum\":{\"field\":\"avgDaysToIssueProvisionalNOCForDepartment\"}}}}}}"
      }
    ],
    "chartType": "metric",
    "valueType": "number",
    "action": "",
    "drillChart": "none",
    "aggregationPaths": [
      "Average days to issue Provisional NOC"
    ],
     "insight": {
      "chartResponseMap" : "nocAvgDayToIssueProvisional",
      "action" : "differenceOfNumbers",
      "upwardIndicator" : "positive",
      "downwardIndicator" : "negative",
      "textMessage" : "$indicator$value% than last $insightInterval",
      "colorCode" : "#228B22",
      "insightInterval" : "year"
    },
    "_comment": "Average days to issue Provisional NOC"
  },
  "nssNOCAverageDaysToIssueActual": {
    "chartName": "NSS_NOC_AVERAGE_DAYS_TO_ISSUE_ACTUAL",
    "queries": [
      {
        "module": "FIRENOC",
        "dateRefField": "date",
        "requestQueryMap": "{\"ward\" : \"ward.keyword\",\"ulb\" : \"ulb.keyword\"}",
        "indexName": "firenoc-national-dashboard",
        "aggrQuery": "{\"aggs\":{\"AGGR\":{\"filter\":{\"bool\":{}},\"aggs\":{\"Average days to issue Actual NOC\":{\"sum\":{\"field\":\"avgDaysToIssueActualNOCForDepartment\"}}}}}}"
      }
    ],
    "chartType": "metric",
    "valueType": "number",
    "action": "",
    "drillChart": "none",
    "aggregationPaths": [
      "Average days to issue Actual NOC"
    ],
    "insight": {
      "chartResponseMap" : "nocAvgDayToIssueActual",
      "action" : "differenceOfNumbers",
      "upwardIndicator" : "positive",
      "downwardIndicator" : "negative",
      "textMessage" : "$indicator$value% than last $insightInterval",
      "colorCode" : "#228B22",
      "insightInterval" : "year"
    },
    "_comment": "Average days to issue Actual NOC"
  },
  "nssNOCSLAComplianceProvisional": {
    "chartName": "NSS_NOC_SLA_COMPLIANCE_PROVISIONAL",
    "queries": [
      {
        "module": "FIRENOC",
        "dateRefField": "date",
        "requestQueryMap": "{\"ward\" : \"ward.keyword\",\"ulb\" : \"ulb.keyword\"}",
        "indexName": "firenoc-national-dashboard",
        "aggrQuery": "{\"aggs\":{\"AGGR\":{\"filter\":{\"bool\":{}},\"aggs\":{\"SLA Compliance (Provisional NOC)\":{\"terms\":{\"field\":\"date\",\"size\":\"1\",\"order\":{\"_key\":\"desc\"}},\"aggs\":{\"Sum\":{\"sum\":{\"field\":\"slaComplianceProvisionalForDepartment\"}}}}}}}}"
      }
    ],
    "chartType": "metric",
    "valueType": "percentage",
    "action": "",
    "drillChart": "none",
    "aggregationPaths": [
      "SLA Compliance (Provisional NOC)"
    ],
    "insight": {
      "chartResponseMap" : "slaCompliance",
      "action" : "differenceOfNumbers",
      "upwardIndicator" : "positive",
      "downwardIndicator" : "negative",
      "textMessage" : "$indicator$value% than last $insightInterval",
      "colorCode" : "#228B22",
      "insightInterval" : "year",
      "isRoundOff": true
    },
    "_comment": "SLA Compliance (Provisional NOC)"
  },
  "nssNOCSLAComplianceActual": {
    "chartName": "NSS_NOC_SLA_COMPLIANCE_ACTUAL",
    "queries": [
      {
        "module": "FIRENOC",
        "dateRefField": "date",
        "requestQueryMap": "{\"ward\" : \"ward.keyword\",\"ulb\" : \"ulb.keyword\"}",
        "indexName": "firenoc-national-dashboard",
        "aggrQuery": "{\"aggs\":{\"AGGR\":{\"filter\":{\"bool\":{}},\"aggs\":{\"SLA Compliance (Actual NOC)\":{\"terms\":{\"field\":\"date\",\"size\":\"1\",\"order\":{\"_key\":\"desc\"}},\"aggs\":{\"Sum\":{\"sum\":{\"field\":\"slaComplianceActualForDepartment\"}}}}}}}}"
      }
    ],
    "chartType": "metric",
    "valueType": "percentage",
    "action": "",
    "drillChart": "none",
    "aggregationPaths": [
      "SLA Compliance (Actual NOC)"
    ],
    "insight": {
      "chartResponseMap" : "slaCompliance",
      "action" : "differenceOfNumbers",
      "upwardIndicator" : "positive",
      "downwardIndicator" : "negative",
      "textMessage" : "$indicator$value% than last $insightInterval",
      "colorCode" : "#228B22",
      "insightInterval" : "year",
      "isRoundOff": true
    },
    "_comment": "SLA Compliance (Actual NOC)"
  },
  "nssNOCProvisionalIssued": {
    "chartName": "NSS_NOC_PROVISIONAL_ISSUED",
    "queries": [
      {
        "module": "FIRENOC",
        "dateRefField": "date",
        "requestQueryMap": "{\"ward\" : \"ward.keyword\",\"ulb\" : \"ulb.keyword\"}",
        "indexName": "firenoc-national-dashboard",
        "aggrQuery": "{\"aggs\":{\"AGGR\":{\"filter\":{\"bool\":{\"must\":[{\"term\":{\"applicationType.keyword\":\"PROVISIONAL\"}}]}},\"aggs\":{\"Provisional Noc's Issued\":{\"sum\":{\"field\":\"todaysApplicationsForApplicationType\"}}}}}}"
      }
    ],
    "chartType": "metric",
    "valueType": "number",
    "action": "",
    "drillChart": "none",
    "aggregationPaths": [
      "Provisional Noc's Issued"
    ],
    "insight": {
      "chartResponseMap" : "nocProvisionalIssued",
      "action" : "differenceOfNumbers",
      "upwardIndicator" : "positive",
      "downwardIndicator" : "negative",
      "textMessage" : "$indicator$value% than last $insightInterval",
      "colorCode" : "#228B22",
      "insightInterval" : "year"
    },
    "_comment": "NSS FIRE NOC Provisional Issued "
  },
  
  "nssNOCApplicationVsProvisionalVsActual": {
    "chartName": "NSS_APPLICATION_VS_PROVISIONAL_VS_ACTUAL",
    "queries": [
      {
        "module": "FIRENOC",
        "dateRefField": "date",
        "requestQueryMap": "{\"ward\" : \"ward.keyword\",\"ulb\" : \"ulb.keyword\"}",
        "indexName": "firenoc-national-dashboard",
        "aggrQuery": "{\"aggs\":{\"AGGR\":{\"filter\":{\"bool\":{}},\"aggs\":{\"Total Applications\":{\"date_histogram\":{\"field\":\"date\",\"interval\":\"intervalvalue\"},\"aggs\":{\"Applications\":{\"sum\":{\"field\":\"todaysApplicationsForApplicationType\"}}}},\"Provisional NOCs Issued\":{\"date_histogram\":{\"field\":\"date\",\"interval\":\"intervalvalue\"},\"aggs\":{\"Provisional\":{\"filter\":{\"bool\":{\"must\":[{\"term\":{\"applicationType.keyword\":\"PROVISIONAL\"}}]}},\"aggs\":{\"Provisional Noc's Issued\":{\"sum\":{\"field\":\"todaysApplicationsForApplicationType\"}}}}}},\"Actual NOCs Issued\":{\"date_histogram\":{\"field\":\"date\",\"interval\":\"intervalvalue\"},\"aggs\":{\"Actual\":{\"filter\":{\"bool\":{\"must\":[{\"term\":{\"applicationType.keyword\":\"NEW\"}}]}},\"aggs\":{\"Actual Noc's Issued\":{\"sum\":{\"field\":\"todaysApplicationsForApplicationType\"}}}}}}}}}}"
      }
    ],
    "chartType": "line",
    "valueType": "number",
    "action": "",
    "drillChart": "none",
    "documentType": "_doc",
    "aggregationPaths": [
      "Total Applications",
      "Provisional NOCs Issued",
      "Actual NOCs Issued"
    ],
    "isCumulative": true,
    "interval": "month",
    "insight": {
    },
    "_comment": "NSS FIRE NOC application vs provisional vs actual"
  },
  
  "nssNocCollectionByPaymentMode": {
    "chartName": "NSS_NOC_COLLECTION_BY_PAYMENT_MODE",
    "queries": [
      {
        "module": "FIRENOC",
        "dateRefField": "date",
        "requestQueryMap": "{\"ward\" : \"ward.keyword\",\"ulb\" : \"ulb.keyword\"}",
        "indexName": "firenoc-national-dashboard",
        "aggrQuery": "{\"aggs\":{\"AGGR\":{\"filter\":{\"bool\":{}},\"aggs\":{\"NOC Collection by PaymentMode\":{\"terms\":{\"field\":\"paymentMode.keyword\"},\"aggs\":{\"Total Collection\":{\"sum\":{\"field\":\"todaysCollectionForPaymentMode\"}}}}}}}}"
      }
    ],
    "chartType": "pie",
    "valueType": "amount",
    "action": "",
    "documentType": "_doc",
    "drillChart": "none",
    "aggregationPaths": [
      "NOC Collection by PaymentMode"
    ],
    "insight": {
    },
    "_comment": "NSS FIRE NOC Collection by payment mode"
  },
  "nssTotalNocIssuedByType": {
    "chartName": "NSS_TOTAL_NOC_ISSUED_TYPE",
    "queries": [
      {
        "module": "FIRENOC",
        "dateRefField": "date",
        "requestQueryMap": "{\"ward\" : \"ward.keyword\",\"ulb\" : \"ulb.keyword\"}",
        "indexName": "firenoc-national-dashboard",
        "aggrQuery": "{\"aggs\":{\"AGGR\":{\"filter\":{\"bool\":{}},\"aggs\":{\"fire NOC Issued\":{\"terms\":{\"field\":\"type.keyword\"},\"aggs\":{\"nocs issued by type\":{\"sum\":{\"field\":\"nocIssuedTodayForType\"}}}}}}}}"
      }
    ],
    "chartType": "pie",
    "valueType": "amount",
    "action": "",
    "documentType": "_doc",
    "drillChart": "none",
    "aggregationPaths": [
      "fire NOC Issued"
    ],
    "insight": {
    },
    "_comment": "NSS FIRE NOC issued by type"
  },
  
  "nssNOCTopPerformingStatesActual": {
    "chartName": "NSS_NOC_TOP_3_PERFORMING_STATES_ACTUAL",
    "queries": [
      {
        "module": "FIRENOC",
        "dateRefField": "date",
        "requestQueryMap": "{\"ward\" : \"ward.keyword\",\"ulb\" : \"ulb.keyword\"}",
        "indexName": "firenoc-national-dashboard",
        "aggrQuery": "{\"aggs\":{\"AGGR\":{\"filter\":{\"bool\":{}},\"aggs\":{\"Total Noc's issued\":{\"terms\":{\"field\":\"state.keyword\",\"size\":\"200\",\"order\":{\"Total applications\":\"desc\"}},\"aggs\":{\"Total applications\":{\"sum\":{\"field\":\"todaysApplicationsForApplicationType\"}}}}}}}}"
      },
      {
        "module": "FIRENOC",
        "dateRefField": "date",
        "requestQueryMap": "{\"ward\" : \"ward.keyword\",\"ulb\" : \"ulb.keyword\"}",
        "indexName": "firenoc-national-dashboard",
        "aggrQuery": "{\"aggs\":{\"AGGR\":{\"filter\":{\"bool\":{}},\"aggs\":{\"Actual Nocs issued\":{\"filter\":{\"bool\":{\"must\":[{\"term\":{\"applicationType.keyword\":\"NEW\"}}]}},\"aggs\":{\"Noc's issued\":{\"terms\":{\"field\":\"state.keyword\",\"size\":\"200\",\"order\":{\"Sum\":\"desc\"}},\"aggs\":{\"Sum\":{\"sum\":{\"field\":\"todaysApplicationsForApplicationType\"}}}}}}}}}}"
      }
    ],
    "isMdmsEnabled": false,
    "isPostResponseHandler": true,
    "postAggregationTheory" : "repsonseToDifferenceOfDates",
    "chartType": "perform",
    "valueType": "percentage",
    "drillChart": "none",
    "documentType": "_doc",
    "action": "percentage",
    "plotLabel": "Actual",
    "order": "desc",
    "limit": 3,
    "aggregationPaths": [
      "Actual Nocs issued",
      "Total Noc's issued"
    ],
    "insight": {
    },
    "_comment": "NSS FIRE NOC top performing state actual"
  },
  
   "nssNOCTopPerformingStatesProvisional": {
    "chartName": "NSS_NOC_TOP_3_PERFORMING_STATES_PROVISIONAL",
    "queries": [
      {
        "module": "FIRENOC",
        "dateRefField": "date",
        "requestQueryMap": "{\"ward\" : \"ward.keyword\",\"ulb\" : \"ulb.keyword\"}",
        "indexName": "firenoc-national-dashboard",
        "aggrQuery": "{\"aggs\":{\"AGGR\":{\"filter\":{\"bool\":{}},\"aggs\":{\"Total Noc's issued\":{\"terms\":{\"field\":\"state.keyword\",\"size\":\"200\",\"order\":{\"Total applications\":\"desc\"}},\"aggs\":{\"Total applications\":{\"sum\":{\"field\":\"todaysApplicationsForApplicationType\"}}}}}}}}"
      },
      {
        "module": "FIRENOC",
        "dateRefField": "date",
        "requestQueryMap": "{\"ward\" : \"ward.keyword\",\"ulb\" : \"ulb.keyword\"}",
        "indexName": "firenoc-national-dashboard",
        "aggrQuery": "{\"aggs\":{\"AGGR\":{\"filter\":{\"bool\":{}},\"aggs\":{\"Provisional Nocs issued\":{\"filter\":{\"bool\":{\"must\":[{\"term\":{\"applicationType.keyword\":\"PROVISIONAL\"}}]}},\"aggs\":{\"Noc's issued\":{\"terms\":{\"field\":\"state.keyword\",\"size\":\"200\",\"order\":{\"Sum\":\"desc\"}},\"aggs\":{\"Sum\":{\"sum\":{\"field\":\"todaysApplicationsForApplicationType\"}}}}}}}}}}"
      }
    ],
    "isMdmsEnabled": false,
    "isPostResponseHandler": true,
    "chartType": "perform",
    "valueType": "percentage",
    "drillChart": "none",
    "documentType": "_doc",
    "action": "percentage",
    "plotLabel": "Provisional",
    "order": "desc",
    "limit": 3,
    "aggregationPaths": [
      "Provisional Nocs issued",
      "Total Noc's issued"      
    ],
    "insight": {
    },
    "_comment": "NSS FIRE NOC top performing state provisional"
  },
  
  "nssNOCBottomPerformingStatesActual": {
    "chartName": "NSS_NOC_BOTTOM_3_PERFORMING_STATES_ACTUAL",
    "queries": [
      {
        "module": "FIRENOC",
        "dateRefField": "date",
        "requestQueryMap": "{\"ward\" : \"ward.keyword\",\"ulb\" : \"ulb.keyword\"}",
        "indexName": "firenoc-national-dashboard",
        "aggrQuery": "{\"aggs\":{\"Total Noc's issued\":{\"terms\":{\"field\":\"state.keyword\",\"size\":\"200\",\"order\":{\"Total applications\":\"desc\"}},\"aggs\":{\"Total applications\":{\"sum\":{\"field\":\"todaysApplicationsForApplicationType\"}}}}}}"
      },
      {
        "module": "FIRENOC",
        "dateRefField": "date",
        "requestQueryMap": "{\"ward\" : \"ward.keyword\",\"ulb\" : \"ulb.keyword\"}",
        "indexName": "firenoc-national-dashboard",
        "aggrQuery": "{\"aggs\":{\"Actual Nocs issued\":{\"filter\":{\"bool\":{\"must\":[{\"term\":{\"applicationType.keyword\":\"NEW\"}}]}},\"aggs\":{\"Noc's issued\":{\"terms\":{\"field\":\"state.keyword\",\"size\":\"200\",\"order\":{\"Sum\":\"desc\"}},\"aggs\":{\"Sum\":{\"sum\":{\"field\":\"todaysApplicationsForApplicationType\"}}}}}}}}"
      }
    ],
    "isMdmsEnabled": false,
    "isPostResponseHandler": true,
    "chartType": "perform",
    "valueType": "percentage",
    "drillChart": "none",
    "documentType": "_doc",
    "action": "percentage",
    "plotLabel": "Actual",
    "order": "asc",
    "limit": 3,
    "aggregationPaths": [
      "Actual Nocs issued",
      "Total Noc's issued"
    ],
    "insight": {
    },
    "_comment": "NSS FIRE NOC bottom performing state actual"
  },
  
   "nssNOCBottomPerformingStatesProvisional": {
    "chartName": "NSS_NOC_BOTTOM_3_PERFORMING_STATES_PROVISIONAL",
    "queries": [
      {
        "module": "FIRENOC",
        "dateRefField": "date",
        "requestQueryMap": "{\"ward\" : \"ward.keyword\",\"ulb\" : \"ulb.keyword\"}",
        "indexName": "firenoc-national-dashboard",
        "aggrQuery": "{\"aggs\":{\"AGGR\":{\"filter\":{\"bool\":{}},\"aggs\":{\"Total Noc's issued\":{\"terms\":{\"field\":\"state.keyword\",\"size\":\"200\",\"order\":{\"Total applications\":\"desc\"}},\"aggs\":{\"Total applications\":{\"sum\":{\"field\":\"todaysApplicationsForApplicationType\"}}}}}}}}"
      },
      {
        "module": "FIRENOC",
        "dateRefField": "date",
        "requestQueryMap": "{\"ward\" : \"ward.keyword\",\"ulb\" : \"ulb.keyword\"}",
        "indexName": "firenoc-national-dashboard",
        "aggrQuery": "{\"aggs\":{\"AGGR\":{\"filter\":{\"bool\":{}},\"aggs\":{\"Provisional Nocs issued\":{\"filter\":{\"bool\":{\"must\":[{\"term\":{\"applicationType.keyword\":\"PROVISIONAL\"}}]}},\"aggs\":{\"Noc's issued\":{\"terms\":{\"field\":\"state.keyword\",\"size\":\"200\",\"order\":{\"Sum\":\"desc\"}},\"aggs\":{\"Sum\":{\"sum\":{\"field\":\"todaysApplicationsForApplicationType\"}}}}}}}}}}"
      }
    ],
    "isMdmsEnabled": false,
    "isPostResponseHandler": true,
    "chartType": "perform",
    "valueType": "percentage",
    "drillChart": "none",
    "documentType": "_doc",
    "action": "percentage",
    "plotLabel": "Provisional",
    "order": "asc",
    "limit": 3,
    "aggregationPaths": [
      "Provisional Nocs issued",
      "Total Noc's issued" 
    ],
    "insight": {
    },
    "_comment": "NSS FIRE NOC bottom performing state provisional"
  },
  
  "nssActualNocIssuedByUsageType": {
    "chartName": "NSS_ACTUAL_NOC_ISSUED_USAGETYPE",
    "queries": [
      {
        "module": "FIRENOC",
        "dateRefField": "date",
        "requestQueryMap": "{\"ward\" : \"ward.keyword\",\"ulb\" : \"ulb.keyword\"}",
        "indexName": "firenoc-national-dashboard",
        "aggrQuery": "{\"aggs\":{\"AGGR\":{\"filter\":{\"bool\":{}},\"aggs\":{\"fire NOC Issued\":{\"terms\":{\"field\":\"usageType.keyword\"},\"aggs\":{\"nocs issued by type\":{\"sum\":{\"field\":\"actualNOCIssuedForUsageType\"}}}}}}}}"
      }
    ],
    "chartType": "pie",
    "valueType": "amount",
    "action": "",
    "documentType": "_doc",
    "drillChart": "none",
    "aggregationPaths": [
      "fire NOC Issued"
    ],
    "insight": {
    },
    "_comment": "NSS Actual FIRE NOC issued by usagetype"
  },
  
  "nssNOCServiceReportByState": {
    "chartName": "NSS_NOC_SERVICE_REPORT_STATE",
    "queries": [
      {
        "module": "FIRENOC",
        "requestQueryMap": "{\"ward\" : \"ward.keyword\",\"state\":\"state.keyword\"}",
        "dateRefField": "date",
        "indexName": "firenoc-national-dashboard",
        "aggrQuery": "{\"aggs\":{\"FireNOC\":{\"filter\":{\"bool\":{\"must_not\":[{\"term\":{\"ulb.keyword\":\"pb.testing\"}}]}},\"aggs\":{\"State\":{\"terms\":{\"field\":\"state.keyword\",\"size\":1000},\"aggs\":{\"Total_Collection\":{\"sum\":{\"field\":\"todaysCollectionForPaymentMode\"}},\"Total_Applications\":{\"value_count\":{\"field\":\"todaysApplicationsForApplicationType\"}},\"Provisional_Fire_Nocs_issued\":{\"filter\":{\"bool\":{\"must\":[{\"term\":{\"applicationType.keyword\":\"PROVISIONAL\"}}]}},\"aggs\":{\"Provisional_Noc's_Issued\":{\"sum\":{\"field\":\"todaysApplicationsForApplicationType\"}}}},\"Actual_Fire_Nocs_issued\":{\"filter\":{\"bool\":{\"must\":[{\"term\":{\"applicationType.keyword\":\"NEW\"}}]}},\"aggs\":{\"Actual_Noc's_Issued\":{\"sum\":{\"field\":\"todaysApplicationsForApplicationType\"}}}},\"Average_days_to_issue_Provisional_NOC\":{\"sum\":{\"field\":\"avgDaysToIssueProvisionalNOCForDepartment\"}},\"Average_days_to_issue_Actual_NOC\":{\"sum\":{\"field\":\"avgDaysToIssueActualNOCForDepartment\"}},\"SLA_Compliance(Actual_NOC)\":{\"terms\":{\"field\":\"date\",\"size\":\"1\",\"order\":{\"_key\":\"desc\"}},\"aggs\":{\"Average\":{\"avg\":{\"field\":\"slaComplianceActualForDepartment\"}}}},\"SLA_Compliance(Provisional_NOC)\":{\"terms\":{\"field\":\"date\",\"size\":\"1\",\"order\":{\"_key\":\"desc\"}},\"aggs\":{\"Average\":{\"avg\":{\"field\":\"slaComplianceProvisionalForDepartment\"}}}}}}}}}}"
      }
    ],
    "isMdmsEnabled": false,
    "filterKeys": [
      {"key": "state", "column": "State"}
    ],
    "chartType": "xtable",
    "valueType": "number",
    "action": "",
    "plotLabel": "State",
    "isPostResponseHandler": true,
    "postAggregationTheory" : "repsonseToDifferenceOfDates",
    "documentType": "_doc",
    "drillChart": "nssNOCServiceReportDrillDownUlb",
    "aggregationPaths": [
      "Total_Collection",
      "Total_Applications",
      "Provisional_Fire_Nocs_issued",
      "Actual_Fire_Nocs_issued",
      "Average_days_to_issue_Provisional_NOC",
      "SLA_Compliance(Provisional_NOC)",
      "Average_days_to_issue_Actual_NOC",
      "SLA_Compliance(Actual_NOC)"
    ],
    "pathDataTypeMapping": [
      {
        "Total_Collection": "amount"
      },
      {
        "Total_Applications": "number"
      },
      {
        "Provisional_Fire_Nocs_issued": "number"
      },
      {
        "Actual_Fire_Nocs_issued": "number"
      },
      {
        "Average_days_to_issue_Provisional_NOC": "number"
      },
      {
        "SLA_Compliance(Provisional_NOC)": "percentage"
      },
      {
        "Average_days_to_issue_Actual_NOC": "number"
      },
      {
        "SLA_Compliance(Actual_NOC)": "percentage"
      }
    ],
    "insight": {
    },
    "_comment": " "
  },
  
  "nssNOCServiceReportDrillDownUlb": {
    "chartName": "NSS_NOC_SERVICE_REPORT_ULB",
    "queries": [
      {
        "module": "FIRENOC",
        "requestQueryMap": "{\"ward\" : \"ward.keyword\", \"tenantId\":\"ulb.keyword\", \"state\":\"state.keyword\"}",
        "dateRefField": "date",
        "indexName": "firenoc-national-dashboard",
        "aggrQuery": "{\"aggs\":{\"FireNOC\":{\"filter\":{\"bool\":{\"must_not\":[{\"term\":{\"ulb.keyword\":\"pb.testing\"}}]}},\"aggs\":{\"ULBs\":{\"terms\":{\"field\":\"ulb.keyword\",\"size\":1000},\"aggs\":{\"Total_Collection\":{\"sum\":{\"field\":\"todaysCollectionForPaymentMode\"}},\"Total_Applications\":{\"value_count\":{\"field\":\"todaysApplicationsForApplicationType\"}},\"Provisional_Fire_Nocs_issued\":{\"filter\":{\"bool\":{\"must\":[{\"term\":{\"applicationType.keyword\":\"PROVISIONAL\"}}]}},\"aggs\":{\"Provisional_Noc's_Issued\":{\"sum\":{\"field\":\"todaysApplicationsForApplicationType\"}}}},\"Actual_Fire_Nocs_issued\":{\"filter\":{\"bool\":{\"must\":[{\"term\":{\"applicationType.keyword\":\"NEW\"}}]}},\"aggs\":{\"Actual_Noc's_Issued\":{\"sum\":{\"field\":\"todaysApplicationsForApplicationType\"}}}},\"Average_days_to_issue_Provisional_NOC\":{\"sum\":{\"field\":\"avgDaysToIssueProvisionalNOCForDepartment\"}},\"Average_days_to_issue_Actual_NOC\":{\"sum\":{\"field\":\"avgDaysToIssueActualNOCForDepartment\"}},\"SLA_Compliance(Actual_NOC)\":{\"terms\":{\"field\":\"date\",\"size\":\"1\",\"order\":{\"_key\":\"desc\"}},\"aggs\":{\"Average\":{\"avg\":{\"field\":\"slaComplianceActualForDepartment\"}}}},\"SLA_Compliance(Provisional_NOC)\":{\"terms\":{\"field\":\"date\",\"size\":\"1\",\"order\":{\"_key\":\"desc\"}},\"aggs\":{\"Average\":{\"avg\":{\"field\":\"slaComplianceProvisionalForDepartment\"}}}}}}}}}}"
      }
    ],
    "isMdmsEnabled": false,
    "filterKeys": [
      {"key": "tenantId", "column": "ULBs"}
    ],
    "chartType": "xtable",
    "valueType": "number",
    "action": "",
    "plotLabel": "ULBs",
    "isPostResponseHandler": true,
    "postAggregationTheory" : "repsonseToDifferenceOfDates",
    "documentType": "_doc",
    "drillChart": "nssNOCServiceReportDrillDownWard",
    "aggregationPaths": [
      "Total_Collection",
      "Total_Applications",
      "Provisional_Fire_Nocs_issued",
      "Actual_Fire_Nocs_issued",
      "Average_days_to_issue_Provisional_NOC",
      "SLA_Compliance(Provisional_NOC)",
      "Average_days_to_issue_Actual_NOC",
      "SLA_Compliance(Actual_NOC)"
    ],
    "pathDataTypeMapping": [
      {
        "Total_Collection": "amount"
      },
      {
        "Total_Applications": "number"
      },
      {
        "Provisional_Fire_Nocs_issued": "number"
      },
      {
        "Actual_Fire_Nocs_issued": "number"
      },
      {
        "Average_days_to_issue_Provisional_NOC": "number"
      },
      {
        "SLA_Compliance(Provisional_NOC)": "percentage"
      },
      {
        "Average_days_to_issue_Actual_NOC": "number"
      },
      {
        "SLA_Compliance(Actual_NOC)": "percentage"
      }
    ],
    "insight": {
    },
    "_comment": " "
  },
   "nssNOCServiceReportDrillDownWard": {
    "chartName": "NSS_NOC_SERVICE_REPORT_WARD",
    "kind": "drillDown",
    "queries": [
      {
        "module": "FIRENOC",
        "requestQueryMap": "{\"ward\":\"ward.keyword\", \"state\":\"state.keyword\", \"tenantId\":\"ulb.keyword\"}",
        "dateRefField": "date",
        "indexName": "firenoc-national-dashboard",
        "aggrQuery": "{\"aggs\":{\"FireNOC\":{\"filter\":{\"bool\":{\"must_not\":[{\"term\":{\"ulb.keyword\":\"pb.testing\"}}]}},\"aggs\":{\"Ward\":{\"terms\":{\"field\":\"ward.keyword\",\"size\":1000},\"aggs\":{\"Total_Collection\":{\"sum\":{\"field\":\"todaysCollectionForPaymentMode\"}},\"Total_Applications\":{\"value_count\":{\"field\":\"todaysApplicationsForApplicationType\"}},\"Provisional_Fire_Nocs_issued\":{\"filter\":{\"bool\":{\"must\":[{\"term\":{\"applicationType.keyword\":\"PROVISIONAL\"}}]}},\"aggs\":{\"Provisional_Noc's_Issued\":{\"sum\":{\"field\":\"todaysApplicationsForApplicationType\"}}}},\"Actual_Fire_Nocs_issued\":{\"filter\":{\"bool\":{\"must\":[{\"term\":{\"applicationType.keyword\":\"NEW\"}}]}},\"aggs\":{\"Actual_Noc's_Issued\":{\"sum\":{\"field\":\"todaysApplicationsForApplicationType\"}}}},\"Average_days_to_issue_Provisional_NOC\":{\"sum\":{\"field\":\"avgDaysToIssueProvisionalNOCForDepartment\"}},\"Average_days_to_issue_Actual_NOC\":{\"sum\":{\"field\":\"avgDaysToIssueActualNOCForDepartment\"}},\"SLA_Compliance(Actual_NOC)\":{\"terms\":{\"field\":\"date\",\"size\":\"1\",\"order\":{\"_key\":\"desc\"}},\"aggs\":{\"Average\":{\"avg\":{\"field\":\"slaComplianceActualForDepartment\"}}}},\"SLA_Compliance(Provisional_NOC)\":{\"terms\":{\"field\":\"date\",\"size\":\"1\",\"order\":{\"_key\":\"desc\"}},\"aggs\":{\"Average\":{\"avg\":{\"field\":\"slaComplianceProvisionalForDepartment\"}}}}}}}}}}"
      }
    ],
    "isMdmsEnabled": false,
    "chartType": "table",
    "valueType": "number",
    "action": "",
    "plotLabel": "Ward",
    "isPostResponseHandler": true,
    "postAggregationTheory" : "repsonseToDifferenceOfDates",
    "documentType": "_doc",
    "drillChart": "none",
    "aggregationPaths": [
      "Total_Collection",
      "Total_Applications",
      "Provisional_Fire_Nocs_issued",
      "Actual_Fire_Nocs_issued",
      "Average_days_to_issue_Provisional_NOC",
      "SLA_Compliance(Provisional_NOC)",
      "Average_days_to_issue_Actual_NOC",
      "SLA_Compliance(Actual_NOC)"
    ],
    "pathDataTypeMapping": [
      {
        "Total_Collection": "amount"
      },
      {
        "Total_Applications": "number"
      },
      {
        "Provisional_Fire_Nocs_issued": "number"
      },
      {
        "Actual_Fire_Nocs_issued": "number"
      },
      {
        "Average_days_to_issue_Provisional_NOC": "number"
      },
      {
        "SLA_Compliance(Provisional_NOC)": "percentage"
      },
      {
        "Average_days_to_issue_Actual_NOC": "number"
      },
      {
        "SLA_Compliance(Actual_NOC)": "percentage"
      }
    ],
    "insight": {
    },
    "_comment": ""
  },
  
  "nssNOCServiceReportByDepartment": {
    "chartName": "NSS_NOC_SERVICE_REPORT_DEPARTMENT",
    "queries": [
      {
        "module": "FIRENOC",
        "requestQueryMap": "{\"ward\" : \"ward.keyword\",\"ulb\" : \"ulb.keyword\"}",
        "dateRefField": "date",
        "indexName": "firenoc-national-dashboard",
        "aggrQuery": "{\"aggs\":{\"FireNOC\":{\"filter\":{\"bool\":{\"must_not\":[{\"term\":{\"ulb.keyword\":\"pb.testing\"}}]}},\"aggs\":{\"Department\":{\"terms\":{\"field\":\"department.keyword\",\"size\":1000},\"aggs\":{\"Total_Collection\":{\"sum\":{\"field\":\"todaysCollectionForDepartment\"}},\"Total_Applications\":{\"value_count\":{\"field\":\"todaysApplicationsForDepartment\"}},\"Provisional_Fire_Nocs_issued\":{\"sum\":{\"field\":\"provisionalNOCIssuedForDepartment\"}},\"Actual_Fire_Nocs_issued\":{\"sum\":{\"field\":\"actualNOCIssuedForDepartment\"}},\"Average_days_to_issue_Provisional_NOC\":{\"sum\":{\"field\":\"avgDaysToIssueProvisionalNOCForDepartment\"}},\"Average_days_to_issue_Actual_NOC\":{\"sum\":{\"field\":\"avgDaysToIssueActualNOCForDepartment\"}},\"SLA_Compliance(Actual_NOC)\":{\"terms\":{\"field\":\"date\",\"size\":\"1\",\"order\":{\"_key\":\"desc\"}},\"aggs\":{\"Average\":{\"avg\":{\"field\":\"slaComplianceActualForDepartment\"}}}},\"SLA_Compliance(Provisional_NOC)\":{\"terms\":{\"field\":\"date\",\"size\":\"1\",\"order\":{\"_key\":\"desc\"}},\"aggs\":{\"Average\":{\"avg\":{\"field\":\"slaComplianceProvisionalForDepartment\"}}}}}}}}}}"
      }
    ],
    "isMdmsEnabled": false,
    "chartType": "table",
    "valueType": "number",
    "action": "",
    "plotLabel": "Department",
    "isPostResponseHandler": true,
    "postAggregationTheory" : "repsonseToDifferenceOfDates",
    "documentType": "_doc",
    "drillChart": "none",
    "aggregationPaths": [
      "Total_Collection",
      "Total_Applications",
      "Provisional_Fire_Nocs_issued",
      "Actual_Fire_Nocs_issued",
      "Average_days_to_issue_Provisional_NOC",
      "SLA_Compliance(Provisional_NOC)",
      "Average_days_to_issue_Actual_NOC",
      "SLA_Compliance(Actual_NOC)"
    ],
    "pathDataTypeMapping": [
      {
        "Total_Collection": "amount"
      },
      {
        "Total_Applications": "number"
      },
      {
        "Provisional_Fire_Nocs_issued": "number"
      },
      {
        "Actual_Fire_Nocs_issued": "number"
      },
      {
        "Average_days_to_issue_Provisional_NOC": "number"
      },
      {
        "SLA_Compliance(Provisional_NOC)": "percentage"
      },
      {
        "Average_days_to_issue_Actual_NOC": "number"
      },
      {
        "SLA_Compliance(Actual_NOC)": "percentage"
      }
    ],
    "insight": {
    },
    "_comment": ""
  },
```

[Click here to check the complete configuration](https://github.com/egovernments/configs/blob/qa/egov-dss-dashboards/dashboard-analytics/ChartApiConfig.json)

**Master Dashboard Configuration:** Master Dashboard Configuration is the main configuration which defines as which are the Dashboards which are to be painted on the screen.&#x20;

It includes all the Visualizations, their groups, the charts which come within them and even their dimensions as what should be their height and width.

```
 {
      "name": "NSS_FIRE_NOC_DASHBOARD",
      "id": "national-firenoc",
      "isActive": "",
      "style": "linear",
      "visualizations": [
        {
          "row": 1,
          "name": "NSS_REVENUE",
          "vizArray": [
            {
              "id": 342,
              "name": "NSS_OVERVIEW",
              "dimensions": {
                "height": 350,
                "width": 2
              },
              "vizType": "metric-collection",
              "noUnit": true,
              "isCollapsible": false,
              "charts": [
                {
                  "id": "nssNOCTodaysCollection",
                  "name": "NSS_NOC_TODAYS_COLLECTION",
                  "code": "",
                  "chartType": "metric",
                  "filter": {
                    "title": "TODAY"
                  },
                  "headers": []
                },
                {
                  "id": "nssNOCTotalCollection",
                  "name": "NSS_NOC_TOTAL_COLLECTION",
                  "code": "",
                  "chartType": "metric",
                  "filter": "",
                  "headers": []
                },
                {
                  "id": "nssNOCTotalApplications",
                  "name": "NSS_NOC_TOTAL_APPLICATIONS",
                  "code": "",
                  "chartType": "metric",
                  "filter": "",
                  "headers": []
                },
                {
                  "id": "nssNOCProvisionalIssued",
                  "name": "NSS_NOC_PROVISIONAL_ISSUED",
                  "code": "",
                  "chartType": "metric",
                  "filter": "",
                  "headers": []
                },
                {
                  "id": "nssNOCActualIssued",
                  "name": "NSS_NOC_ACTUAL_ISSUED",
                  "code": "",
                  "chartType": "metric",
                  "filter": "",
                  "headers": []
                },
                {
                  "id": "nssNOCAverageDaysToIssueProvisional",
                  "name": "NSS_NOC_AVERAGE_DAYS_TO_ISSUE_PROVISIONAL",
                  "code": "",
                  "chartType": "metric",
                  "filter": "",
                  "headers": []
                },
                {
                  "id": "nssNOCSLAComplianceProvisional",
                  "name": "NSS_NOC_SLA_COMPLIANCE_PROVISIONAL",
                  "code": "",
                  "chartType": "metric",
                  "filter": "",
                  "headers": []
                },
                {
                  "id": "nssNOCAverageDaysToIssueActual",
                  "name": "NSS_NOC_AVERAGE_DAYS_TO_ISSUE_ACTUAL",
                  "code": "",
                  "chartType": "metric",
                  "filter": "",
                  "headers": []
                },
                {
                  "id": "nssNOCSLAComplianceActual",
                  "name": "NSS_NOC_SLA_COMPLIANCE_ACTUAL",
                  "code": "",
                  "chartType": "metric",
                  "filter": "",
                  "headers": []
                }
              ]
            },
            {
              "id": 342,
              "name": "NSS_NOC_TOTAL_CUMULATIVE_COLLECTION",
              "dimensions": {
                "height": 350,
                "width": 7
              },
              "vizType": "chart",
              "label": "",
              "noUnit": true,
              "isCollapsible": false,
              "charts": [
                {
                  "id": "nssNOCCumulativeCollection",
                  "name": "Monthly",
                  "code": "",
                  "chartType": "line",
                  "filter": "",
                  "headers": []
                }
              ]
            }
          ]
        },
        {
          "row": 2,
          "name": "NSS_REVENUE",
          "vizArray": [
          	{
              "id": 343,
              "name": "NSS_APPLICATION_VS_PROVISIONAL_VS_ACTUAL",
              "dimensions": {
                "height": 190,
                "width": 10
              },
              "vizType": "chart",
              "isCollapsible": false,
              "label": "",
              "charts": [
                {
                  "id": "nssNOCApplicationVsProvisionalVsActual",
                  "name": "Monthly",
                  "code": "",
                  "chartType": "line",
                  "filter": "",
                  "headers": []
                }
              ]
            },
            {
              "id": 210,
              "name": "NSS_NOC_COLLECTION_BY_PAYMENT_MODE",
              "dimensions": {
                "height": 250,
                "width": 4
              },
              "vizType": "chart",
              "label": "",
              "noUnit": false,
              "isCollapsible": false,
              "charts": [
                {
                  "id": "nssNocCollectionByPaymentMode",
                  "name": "NSS_NOC_COLLECTION_BY_PAYMENT_MODE",
                  "code": "",
                  "chartType": "donut",
                  "filter": "",
                  "headers": []
                }
              ]
            },
            {
              "id": 211,
              "name": "NSS_TOTAL_NOC_ISSUED_TYPE",
              "dimensions": {
                "height": 250,
                "width": 4
              },
              "vizType": "chart",
              "noUnit": false,
              "isCollapsible": false,
              "charts": [
                {
                  "id": "nssTotalNocIssuedByType",
                  "name": "NSS_TOTAL_NOC_ISSUED_TYPE",
                  "code": "",
                  "chartType": "donut",
                  "filter": "",
                  "headers": []
                }
              ]
            }
          ]
        },
        {
          "row": 3,
          "name": "NSS_REVENUE",
          "vizArray": [
            {
              "id": 212,
              "name": "NSS_ACTUAL_NOC_ISSUED_USAGETYPE",
              "dimensions": {
                "height": 250,
                "width": 4
              },
              "vizType": "chart",
              "noUnit": false,
              "isCollapsible": false,
              "charts": [
                {
                  "id": "nssActualNocIssuedByUsageType",
                  "name": "NSS_ACTUAL_NOC_ISSUED_USAGETYPE",
                  "code": "",
                  "chartType": "donut",
                  "filter": "",
                  "headers": []
                }
              ]
            },
            {
              "id": 221,
              "name": "NSS_NOC_TOP_3_PERFORMING_STATES",
              "dimensions": {
                "height": 250,
                "width": 4
              },
              "vizType": "performing-metric",
              "isCollapsible": false,
              "label": "",
              "charts": [
                {
                  "id": "nssNOCTopPerformingStatesActual",
                  "name": "NSS_NOC_TOP_3_PERFORMING_STATES_ACTUAL",
                  "code": "",
                  "chartType": "bar",
                  "filter": "",
                  "headers": [],
                  "tabName": "Actual"
                },
                {
                  "id": "nssNOCTopPerformingStatesProvisional",
                  "name": "NSS_NOC_TOP_3_PERFORMING_STATES_PROVISIONAL",
                  "code": "",
                  "chartType": "bar",
                  "filter": "",
                  "headers": [],
                  "tabName": "Provisional"
                }
              ]
            },
            {
              "id": 222,
              "name": "NSS_NOC_BOTTOM_3_PERFORMING_STATES",
              "dimensions": {
                "height": 250,
                "width": 4
              },
              "vizType": "performing-metric",
              "isCollapsible": false,
              "charts": [
                {
                  "id": "nssNOCBottomPerformingStatesActual",
                  "name": "NSS_NOC_BOTTOM_3_PERFORMING_STATES_ACTUAL",
                  "code": "",
                  "chartType": "bar",
                  "filter": "",
                  "headers": [],
                  "tabName": "Actual"
                },
                {
                  "id": "nssNOCBottomPerformingStatesProvisional",
                  "name": "NSS_NOC_BOTTOM_3_PERFORMING_STATES_PROVISIONAL",
                  "code": "",
                  "chartType": "bar",
                  "filter": "",
                  "headers": [],
                  "tabName": "Provisional"
                }
              ]
            }
          ]
        },
        {
          "row": 4,
          "name": "NSS_REVENUE",
          "vizArray": [
            {
              "id": 231,
              "name": "Service Report",
              "dimensions": {
                "height": 350,
                "width": 12
              },
              "vizType": "chart",
              "noUnit": false,
              "isCollapsible": false,
              "charts": [
                {
                  "id": "nssNOCServiceReportByState",
                  "name": "NSS_NOC_SERVICE_REPORT_STATE",
                  "code": "",
                  "chartType": "table",
                  "filter": "",
                  "headers": [],
                  "tabName": "State"
                },
                {
                  "id": "nssNOCServiceReportByDepartment",
                  "name": "NSS_NOC_SERVICE_REPORT_DEPARTMENT",
                  "code": "",
                  "chartType": "table",
                  "filter": "",
                  "headers": [],
                  "tabName": "Department"
                }
              ]
            }
          ]
        } 
      ]
    }
```

[Click here for the complete configuration](https://github.com/egovernments/configs/blob/qa/egov-dss-dashboards/dashboard-analytics/MasterDashboardConfig.json)

**Role Dashboard Mappings Configuration:** Master Dashboard Configuration which was explained earlier holds the list of dashboards that are available.

Given the instance where role action mapping is not maintained in the Application Service, this configuration acts as a role dashboard mapping configuration. In this, each role is mapped against the dashboard that they are authorized to see.

This was used earlier when the role action mapping of eGov was not integrated. Later, when the role action mapping started controlling the dashboards to be seen on the client side, this configuration was just used to enable the dashboards for viewing.&#x20;

```
{
  "_comment": "Holds mapping for each role with and its associated dashboards",
  "roles" : [
    {
      "_comment":"This role is super role which can access all the available dashboards: [other/new roles are suppose to be added]",
      "roleId": 6,
      "roleName" : "Admin",
      "isSuper" : "",
      "orgId": "",
      "dashboards": [
        {
          "name": "National Fire Noc",
          "id": "national-firenoc"
        }
      ]
    }

  ]
}
```

[Click here to check the configuration](https://github.com/egovernments/configs/blob/qa/egov-dss-dashboards/dashboard-analytics/RoleDashboardMappingsConf.json)

&#x20;**MDMS Configuration to be added:** _common-masters/uiCommonConstants.json_

```
"national-firenoc":{
                  "routePath":"/dashboard/national-firenoc",
                  "isOrigin":true
               }
               }
```

[Click here to check the complete configuration](https://github.com/egovernments/egov-mdms-data/blob/QA/data/pb/common-masters/uiCommonConstants.json)

roleaction.json

```
{
      "rolecode": "STADMIN",
      "actionid": {{PlaceHolder1}},
      "actioncode": "",
      "tenantId": "pb"
    },
    
    {
      "rolecode": "STADMIN",
      "actionid": {{PlaceHolder2}},
      "actioncode": "",
      "tenantId": "pb"
    },
     {
      "rolecode": "EMPLOYEE",
      "actionid": {{PlaceHolder2}},
      "actioncode": "",
      "tenantId": "pb"
    },  
     {
      "rolecode": "UC_EMP",
      "actionid": {{PlaceHolder2}},
      "actioncode": "",
      "tenantId": "pb"
    },
```

[Click here to check the complete configuration](https://github.com/egovernments/egov-mdms-data/blob/QA/data/pb/ACCESSCONTROL-ROLEACTIONS/roleactions.json)

Action test.json:

```
{
      "id": {{PlaceHolder1}},
      "name": "NSS Dashboard Config obps",
      "url": "/dashboard-analytics/dashboard/getDashboardConfig/national-firenoc",
      "parentModule": "",
      "displayName": "NSS",
      "orderNumber": 0,
      "enabled": false,
      "serviceCode": "NSS",
      "code": "null",
      "path": ""
},
{
      "id": {{PlaceHolder2}},
      "name": "National Dashboard Fire Noc",
      "url": "url",
      "displayName": "National Fire Noc",
      "orderNumber": 4,
      "parentModule": "ndss-dashboard",
      "enabled": true,
      "serviceCode": "NDSS",
      "code": "null",
      "path": "NatDashboard.FireNoc",
      "navigationURL": "integration/dss/national-firenoc",
      "leftIcon": "places:business-center",
      "rightIcon": ""
}
```

[Click here to check the complete configuration](https://github.com/egovernments/egov-mdms-data/blob/QA/data/pb/ACCESSCONTROL-ACTIONS-TEST/actions-test.json)

FireNoc-National DSS _c_ontains multiple graphs that represent the Fire NOC data. Each graph has its own configuration that describes the chart and its type.

National DSS contains the following charts in Fire NOC:

**Fire Noc Page**

* Overview
* Total Cumulative Collection
* Total applications vs Provisional NOCs issued vs Actual NOCs issued
* Collection by Payment Mode
* Total NOCs issued by type
* Actual Fire NOCs by usage type
* Top 3 Performing States
* Bottom 3 Performing States
* Service Report

**Overview:** The overview graph contains multiple data information as below in the selected time period.

* **Today’s Collection:** This represents the sum of revenue collected from the issuance of a Provisional and Actual Fire NOC which is Application fee + NOC Issuance fee
* &#x20;**Total Collection:** Sum of revenue collected from Fire NOC for the applied date filter
* **Total Applications:** Total number of applications submitted for a new Fire NOC
* **Provisional NOC Issued:** The Provisional NOC is to be obtained to ensure that the proposed constructions meet the fire safety compliant norms
* **Actual NOCs Issued:** The Actual NOC is to be obtained to ensure that the proposed constructions meet the fire safety compliant norms
* **Avg. days to issue Provisional Fire NOC:** Average number of days taken to issue a Provisional NOC
* **Avg. days to issue Actual Fire NOC:** Average number of days taken to issue an actual NOC
* **SLA Compliance (Actual Fire NOC):** % of Actual NOCs issued within SLA
* **SLA Compliance (Provisional Fire NOC):** % of Provisional NOCs issued within SLA

![](<../../../../.gitbook/assets/image (163).png>)

**Total Cumulative Collection:** This graph contains the Fire NOC collection amount information on a monthly base as a cumulative line graph for each Fire NOC collection separately. This will change as per the denomination amount filter selection.

**line** - this graph/chart is data representation on date histograms or date groupings.

![](<../../../../.gitbook/assets/image (365).png>)

**Total applications vs Provisional NOCs issued vs Actual NOCs issued:** This graph contains the Fire NOC showing total applications submitted vs provisional NOCs issued vs actual NOCs issued for a given month collection separately. This changes as per the denomination amount filter selection.

**line** - this graph/chart is data representation on date histograms or date groupings.

<div align="left">

<img src="../../../../.gitbook/assets/image (22).png" alt="">

</div>

**Collection by Payment Mode:** This is a pie chart showing the bifurcation of total collections by payment mode (online, cash, card, cheque) which is the sum of revenue collected from Fire NOC for the applied date filter.

<div align="left">

<img src="../../../../.gitbook/assets/image (31).png" alt="">

</div>

**Total NOCs issued by type:** This is a pie chart showing bifurcation of Total NOCs issued into Provisional and Actual Fire NOCs. The sum of Provisional and Actual Fire NOCs issued.

<div align="left">

<img src="../../../../.gitbook/assets/image (84).png" alt="">

</div>

**Actual Fire NOCs by usage typeThe total:** This is a pie chart showing a bifurcation of Actual Fire NOCs by usage type. Total number of Fire NOCs issued by the concerned authority.

<div align="left">

<img src="../../../../.gitbook/assets/image (19).png" alt="">

</div>

**Top 3 Performing States:** This card shows the Top 3 Performing States/ULBs/Wards based on % NOCs issued. The number of Fire NOCs issued / Number of applications depends on whether a user selects 'Provisional' or 'Actual'.

Clicking on Actual shows the % of NOCs issued for Actual Fire NOCs.

<div align="left">

<img src="../../../../.gitbook/assets/image (74).png" alt="">

</div>

Clicking on Provisional shows the % of NOCs issued for Actual Fire NOCs.

<div align="left">

<img src="../../../../.gitbook/assets/image (154).png" alt="">

</div>

Clicking on the Show More option displays information about all states.

![](<../../../../.gitbook/assets/image (125).png>)

**Bottom 3 Performing States:** This card shows the Bottom 3 Performing States/ULBs/Wards based on % NOCs issued. The Number of Fire NOCs issued / Number of applications depends on whether a user selects 'Provisional' or 'Actual'.

Clicking on Actual shows the % of NOCs issued for Actual Fire NOCs.

<div align="left">

<img src="../../../../.gitbook/assets/image (43).png" alt="">

</div>

Clicking on Provisional shows the % of NOCs issued for Actual Fire NOCs.

<div align="left">

<img src="../../../../.gitbook/assets/image (133).png" alt="">

</div>

Clicking on Show More provides information on all the states.

![](<../../../../.gitbook/assets/image (78).png>)

**Service Report:** This tabular chart representation graph shows multiple Fire NOC information like Total Collection, Applications Submitted, Provisional Fire NOC issued, New Fire NOC Issued, Average days to issue Provisional NOC, SLA Compliance (Provisional NOC), Average days to issue New NOC, SLA Compliance (New NOC). And this table shows the data at the state level and also has the drill-down chart for each state to ULB and from ULB to the ward level data for the same.

xtable type allows to add multiple computed fields with the aggregated fields dynamically added.

To add multiple computed columns,  computedFields \[]  where actionName (IComputedField\<T> interface), fields \[] names as in exist in query key, newField as name to appear for computation must be defined.

![](<../../../../.gitbook/assets/image (152).png>)

![](<../../../../.gitbook/assets/image (86).png>)

Clicking on any region name provides drill-down charts representing the specific state data.

![](<../../../../.gitbook/assets/image (143).png>)

Clicking on the ULB navigates to wards under that specific ULB and each ward shows the specific data regarding that ward.

![](<../../../../.gitbook/assets/image (146).png>)

### **Newly Introduced Properties** <a href="#newly-introduced-property" id="newly-introduced-property"></a>

**isRoundOff**: This property is introduced to round off the decimal values. Ex: if the value is 25.43 by using isRoundOff property in the configuration we will get it as 25. if the value is 22.56 round of value will be 23.\
This can be used for insights configuration as well for overview graphs.

### Common Properties Available <a href="#common-properties-available" id="common-properties-available"></a>

**Key(eg: fsmTotalrequest):** This is the Visualization Code. This key will be referred to in further visualization configurations.

This is the key which will be used by the client application to indicate which visualization is needed for display.

**chartName:** The name of the Chart which has to be used as a label on the Dashboard. The name of the Chart will be a detailed name.

In this configuration, the Name of the Chart will be the code of Localization which will be used by the Client Side.

**queries:** Some visualizations are derived from a specific data source. While some others are derived from different data sources and are combined together to get a meaningful representation.

The queries of aggregation which are to be used to fetch out the right data in the right aggregated format are configured here.

**queries.module:** The module/domain level, on which the query should be applied on. Fire NOC is FIRE NOC.

**queries.indexName:** The name of the index upon which the query has to be executed is configured here.

**queries.aggrQuery:** The aggregation query in itself is added here. Based on the Module and the Index name specified, this query is attached to the filter part of the complete search request and then executed against that index

**queries.requestQueryMap:** Client Request would carry certain fields which are to be filtered. The parameters specified in the Client Request are different from the parameters in each of these indexed documents.

In order to map the parameters of the request to the parameters of the ElasticSearch Document, this mapping is maintained.

**queries.dateRefField:** Each of these modules has separate indexes. And all of them have their own date fields.&#x20;

When there is a date filter applied against these visualizations, each of them has to apply it against their own date reference fields.

In order to maintain what is the date field in which index, we have this configured in this configuration parameter.

**chartType:** As there are different types of visualizations, this field defines what is the type of chart /visualization that this data should be used to represent.&#x20;

**Chart types available are**:

**metric** - this represents the aggregated amount/value for records filter by the aggregate es query&#x20;

**pie** - this represents the aggregated data on grouping. This is can be used to represent any line graph, bar graph, pie chart or donuts

**line** - this graph/chart is data representation on date histograms or date groupings

**perform** - this chart represents groping data as performance wise.

**table** - represents a form of plots and value with headers as grouped on and list of its key, values pairs.&#x20;

**xtable -** represents a advanced feature of table, it has addition capabilities for dynamic adding header values.

**valueType:** In any case of data, the values which are sent to plot, might be a percentage, sometimes an amount and sometimes it is just a count.

In order to represent them and differentiate the numbers from amount from percentage, this field is used to indicate the type of value that this Visualization will be sending.

**action:** Some of the visualizations are not just aggregation on data source. There might be some cases where we have to do a post aggregation computation.

For Example, in the case of Top 3 Performing ULBs, the Target and Total Collection is obtained and then the percentage is calculated. In these kinds of cases, what is the action that has to be performed on that data obtained is defined in this parameter.&#x20;

**documentType:** The type of document upon which the query has to be executed is defined here.&#x20;

**drillChart:** If there is a drill down on the visualization, then the code of the Drill Down Visualization is added here. This will be used by Client Service to manage drill downs.

**aggregationPaths:** All the queries will be having Aggregation names in it. In order to fetch the value out of each Aggregation Responses, the name of the aggregation in the query will be an easy bet. These aggregation paths will have the names of Aggregation in it.

**insights:** It is to show the data with the comparison of last year with arrow symbols, it will show the data in how much % is increased or decreased.&#x20;

**\_comment:** In order to display information on the “i” symbol of each visualization, Visualization Information is maintained in this field.&#x20;

#### **Index Properties of National Fire NOC-DSS** <a href="#index-properties-of-state-firenoc-dss" id="index-properties-of-state-firenoc-dss"></a>

The index that contains data for National Fire NOC is - _firenoc-services_

The mapping for this index is given below

```
{
  "properties": {
    "tenantId": {
      "type": "text",
      "fields": {
        "keyword": {
          "type": "keyword",
          "ignore_above": 256
        }
      }
    },
	"date": {
      "type": "date",
      "format": "dd-MM-yyyy HH:mm:ss||dd-MM-yyyy||epoch_millis"
    },
	"module": {
      "type": "text",
      "fields": {
        "keyword": {
          "type": "keyword",
          "ignore_above": 256
        }
      }
    },
	"ulb": {
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
    "todaysApplicationsForApplicationType": {
      "type": "long"
    },
    "todaysApplicationsForDepartment": {
      "type": "long"
    },
    "todaysCollectionForDepartment": {
      "type": "long"
    },
    "provisionalNOCIssuedForDepartment": {
      "type": "long"
    },
    "actualNOCIssuedForDepartment": {
      "type": "long"
    },
    "avgDaysToIssueProvisionalNOCForDepartment": {
      "type": "long"
    },
    "slaComplianceActualForDepartment": {
      "type": "long"
    },
    "avgDaysToIssueActualNOCForDepartment": {
      "type": "long"
    },
    "actualNOCIssuedByDeptForDepartment": {
      "type": "long"
    },
    "nocIssuedTodayForType": {
      "type": "long"
    },
    "todaysCollectionForPaymentMode": {
      "type": "long"
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
    "applicationType": {
      "type": "text",
      "fields": {
        "keyword": {
          "type": "keyword",
          "ignore_above": 256
        }
      }
    },
    "department": {
      "type": "text",
      "fields": {
        "keyword": {
          "type": "keyword",
          "ignore_above": 256
        }
      }
    },
    "type": {
      "type": "text",
      "fields": {
        "keyword": {
          "type": "keyword",
          "ignore_above": 256
        }
      }
    },
    "paymentMode": {
      "type": "text",
      "fields": {
        "keyword": {
          "type": "keyword",
          "ignore_above": 256
        }
      }
    }
  }
}
```

The following is the table that describes the properties mentioned above:

| **Attributes**                       | **Definition**                                                                                                       | **Breakup**                               |
| ------------------------------------ | -------------------------------------------------------------------------------------------------------------------- | ----------------------------------------- |
| ulb                                  | The district or region for which the data is ingested                                                                | Nil                                       |
| state                                | The ULB name for which the data is ingested                                                                          | Nil                                       |
| ward                                 | The ward for which the data is ingested                                                                              | Nil                                       |
| todaysCollection                     | <p>Sum of revenue collected from issuance of a Fire NOC<br>Application fee + NOC Issuance fee + renewal fee</p>      | Breakup by paymentMode and department     |
| todaysApplications                   | Total number of applications received                                                                                | Breakup by applicationType and department |
| nocIssuedToday                       | Total number of NOC issued by the concerned authority                                                                | Breakup by type                           |
| provisionalNOCIssued                 | The Provisional NOC is to be obtained to ensure that the proposed constructions meet the fire safety compliant norms | Breakup by department                     |
| actualNOCIssued                      | Total # of Fire NOCs issued by concerned authority                                                                   | Breakup by usageType and department       |
| avgDaysToIssueProvisionalNOC         | Total # of days taken to issue a Provisional NOC / Provisional NOCs issued - latest date                             | Breakup by department                     |
| slaComplianceActual                  | # of Actual NOCs issued within SLA / Total applications - till the given date                                        | Breakup by department                     |
| slaComplianceProvisional             | # of Provisional NOCs issued within SLA / Total applications - till the given date                                   | Breakup by department                     |
| avgDaysToIssueActualNOC              | Total # of days taken to issue an actual NOC / Actual NOCs issued - latest date                                      | Breakup by department                     |
| todaysClosedApplications             | # of Applications closed on the given date                                                                           | Nill                                      |
| todaysCompletedApplicationsWithinSLA | # of Applications closed on the given date within SLA                                                                | Nill                                      |

**Postman collection for National FireNoc- Dss:**

[https://www.getpostman.com/collections/2f7a283a42c695b2a52f](https://www.getpostman.com/collections/2f7a283a42c695b2a52f)

