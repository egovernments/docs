# Water & Sewerage Reports

## Overview <a href="#overview" id="overview"></a>

This document provides the steps for configuring water & sewerage reports. There are 3 Water & Sewerage reports that can be generated:

1. **Receipt Register Report**
2. **Collection Register Report**
3. **Defaulter Report**

## Configuration Details <a href="#configuring-report" id="configuring-report"></a>

To configure the Water & Sewerage report, follow the steps below:

* [x] To add a new report first add a file path in the **reportFileLocationsv1**.\
  List the W\&S report location in the following link: [<img src="https://github.com/fluidicon.png" alt="" data-size="line">configs/reportFileLocationsv1.txt at f80f822314ef951890b41c92ca9eab3ee41413b0 · egovernments/configs](https://github.com/egovernments/configs/blob/f80f822314ef951890b41c92ca9eab3ee41413b0/reports/reportFileLocationsv1.txt#L21)
* [x] Once the file path is added in the file reportFileLocationsv1, go to the folder /configs/reports/config \[[<img src="https://github.com/fluidicon.png" alt="" data-size="line">configs/reports/config at qa · egovernments/configs](https://github.com/egovernments/configs/tree/qa/reports/config) ].\
  Create a new file and name the file that you have given in the file reportFileLocationsv1.\
  Name the W\&S report: **rainmaker-wns-reports.yml**
* [x] Write the report configuration -\
  Refer [<img src="https://github.com/fluidicon.png" alt="" data-size="line">configs/rainmaker-wns-reports.yml at qa · egovernments/configs](https://github.com/egovernments/configs/blob/qa/reports/config/rainmaker-wns-reports.yml) for current configs.\
  \[For further clarification on how to write the report configs, refer to [Report Service](https://core.digit.org/platform/core-services/report-service) ]\
  Commit the changes once complete.
* [x] Add the role and actions for the new report as given below:\
  \
  **In action-test.json:**

```
{
      "id": 2343,
      "name": "WnsDefaulterReport",
      "url": "url",
      "displayName": "WnS Defaulter Report",
      "orderNumber": 2,
      "parentModule": "rainmaker-wns",
      "enabled": true,
      "serviceCode": "WnS",
      "code": "null",
      "path": "WnS.Wns Reports.WnSDefaulterReport",
      "navigationURL": "report/rainmaker-wns/WnsDefaulterReport",
      "leftIcon": "action:assignment",
      "rightIcon": ""
    },
    {
      "id": 2344,
      "name": "WnsDefaulterReport",
      "url": "/report/rainmaker-wns/WnsDefaulterReport/metadata/_get",
      "displayName": "rainmaker-wns-WnsDefaulterReport",
      "orderNumber": 1,
      "parentModule": "",
      "enabled": true,
      "serviceCode": "report",
      "code": "null",
      "path": ""
    },
    {
      "id": 2345,
      "name": "WnsDefaulterReport",
      "url": "/report/rainmaker-wns/WnsDefaulterReport/_get",
      "displayName": "rainmaker-wns-WnsDefaulterReport",
      "orderNumber": 1,
      "parentModule": "",
      "enabled": true,
      "serviceCode": "report",
      "code": "null",
      "path": ""
    }
```

**In action-test.json:**

```
    {
      "rolecode": "WATER_REPORT_VIEWER",
      "actionid": 2343,
      "actioncode": "",
      "tenantId": "pb"
    },
    {
      "rolecode": "SEWERAGE_REPORT_VIEWER",
      "actionid": 2343,
      "actioncode": "",
      "tenantId": "pb"
    },
    {
      "rolecode": "WATER_REPORT_VIEWER",
      "actionid": 2344,
      "actioncode": "",
      "tenantId": "pb"
    },
    {
      "rolecode": "SEWERAGE_REPORT_VIEWER",
      "actionid": 2344,
      "actioncode": "",
      "tenantId": "pb"
    },
    {
      "rolecode": "WATER_REPORT_VIEWER",
      "actionid": 2345,
      "actioncode": "",
      "tenantId": "pb"
    },
    {
      "rolecode": "SEWERAGE_REPORT_VIEWER",
      "actionid": 2345,
      "actioncode": "",
      "tenantId": "pb"
    }
```

* [x] Restart the MDMS and report service.

{% hint style="info" %}
**Above is the sample for Defaulter Report, in a similar way other reports can also be configured.**
{% endhint %}

## **Reference Docs** <a href="#reference-docs" id="reference-docs"></a>

### **Doc Links**

| **Title**                                                                                                                   | **Link**                                                                                                                                                                                      |
| --------------------------------------------------------------------------------------------------------------------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
|  [reportFileLocationsv1](https://raw.githubusercontent.com/egovernments/configs/DEV/reports/reportFileLocationsv1.txt) file |  [https://raw.githubusercontent.com/egovernments/configs/DEV/reports/reportFileLocationsv1.txt](https://raw.githubusercontent.com/egovernments/configs/DEV/reports/reportFileLocationsv1.txt) |
|  report config folder                                                                                                       |  [configs/reports/config at DEV · egovernments/configs](https://github.com/egovernments/configs/tree/DEV/reports/config)                                                                      |
| Report service                                                                                                              | [Report Service](https://core.digit.org/platform/core-services/report-service)                                                                                                                |

&#x20;
