---
description: Technical documentation
---

# Birth and Death: Reports

## Overview <a href="#overview" id="overview"></a>

There are 5 B\&D Reports that exist _viz._ **Birth Count Report, Birth Records Count Report By District, Birth and Death Certificate Payment Records, Death Count Report, Death Records Count Report by District.**

## Configuration Details <a href="#configuring-report" id="configuring-report"></a>

To configure the B\&D Report, follow the steps below:

* [x] To add a new report first add the file path in the **reportFileLocationsv1**.\
  The B\&D report location can be listed in the following link: [<img src="https://github.com/fluidicon.png" alt="" data-size="line">configs/reportFileLocationsv1.txt at f80f822314ef951890b41c92ca9eab3ee41413b0 · egovernments/configs](https://github.com/egovernments/configs/blob/f80f822314ef951890b41c92ca9eab3ee41413b0/reports/reportFileLocationsv1.txt#L23)
* [x] Once the file path is added in the file reportFileLocationsv1, go to the folder /configs/reports/config \[[<img src="https://github.com/fluidicon.png" alt="" data-size="line">configs/reports/config at qa · egovernments/configs](https://github.com/egovernments/configs/tree/qa/reports/config) ] . **birthcount-report.yml**\
  Create a new file and name the file that you have given in the file reportFileLocationsv1.
* [x] Write the report configuration.\
  Refer [<img src="https://github.com/fluidicon.png" alt="" data-size="line">configs/birthcount-reports.yml at qa · egovernments/configs](https://github.com/egovernments/configs/blob/qa/reports/config/birthcount-reports.yml) for current configs.\
  \[For further clarification on how to write the report configs, refer to [Report Service](broken-reference) ]\
  Once it is done commit those changes.
* [x] Add the role and actions for the new report as follows:

**In action-test.json:**

```
{
      "id": 2277,
      "name": "BirthRecordsCountReport",
      "url": "/report/rainmaker-bnd/BirthRecordsCountReport/_get",
      "displayName": "BirthRecordsCountReport",
      "orderNumber": 1,
      "parentModule": "",
      "enabled": true,
      "serviceCode": "report",
      "code": "null",
      "path": ""
    },
    {
      "id": 2278,
      "name": "BirthRecordsCountReport",
      "url": "/report/rainmaker-bnd/BirthRecordsCountReport/metadata/_get",
      "displayName": "BirthRecordsCountReport",
      "orderNumber": 1,
      "parentModule": "",
      "enabled": true,
      "serviceCode": "report",
      "code": "null",
      "path": ""
    },
    {
      "id": 2279,
      "name": "BirthRecordsCountReport",
      "url": "url",
      "displayName": "Birth Records Count",
      "orderNumber": 9,
      "parentModule": "rainmaker-bnd",
      "enabled": true,
      "serviceCode": "bnd",
      "code": "null",
      "path": "cbbnd.BirthRecordsCountReport",
      "navigationURL": "report/rainmaker-bnd/BirthRecordsCountReport",
      "leftIcon": "action:assignment",
      "rightIcon": ""
    },
    {
      "id": 2280,
      "name": "DeathRecordsCountReport",
      "url": "/report/rainmaker-bnd/DeathRecordsCountReport/_get",
      "displayName": "DeathRecordsCountReport",
      "orderNumber": 2,
      "parentModule": "",
      "enabled": true,
      "serviceCode": "report",
      "code": "null",
      "path": ""
    },
    {
      "id": 2281,
      "name": "DeathRecordsCountReport",
      "url": "/report/rainmaker-bnd/DeathRecordsCountReport/metadata/_get",
      "displayName": "DeathRecordsCountReport",
      "orderNumber": 2,
      "parentModule": "",
      "enabled": true,
      "serviceCode": "report",
      "code": "null",
      "path": ""
    },
    {
      "id": 2282,
      "name": "DeathRecordsCountReport",
      "url": "url",
      "displayName": "Death Records Count",
      "orderNumber": 9,
      "parentModule": "rainmaker-bnd",
      "enabled": true,
      "serviceCode": "bnd",
      "code": "null",
      "path": "cbbnd.DeathRecordsCountReport",
      "navigationURL": "report/rainmaker-bnd/DeathRecordsCountReport",
      "leftIcon": "action:assignment",
      "rightIcon": ""
    },
    {
      "id": 2283,
      "name": "BirthRecordsCountReportCBLevel",
      "url": "/report/rainmaker-bnd/BirthRecordsCountReportCBLevel/_get",
      "displayName": "BirthRecordsCountReportCBLevel",
      "orderNumber": 1,
      "parentModule": "",
      "enabled": true,
      "serviceCode": "report",
      "code": "null",
      "path": ""
    },
    {
      "id": 2284,
      "name": "BirthRecordsCountReportCBLevel",
      "url": "/report/rainmaker-bnd/BirthRecordsCountReportCBLevel/metadata/_get",
      "displayName": "BirthRecordsCountReportCBLevel",
      "orderNumber": 1,
      "parentModule": "",
      "enabled": true,
      "serviceCode": "report",
      "code": "null",
      "path": ""
    },
    {
      "id": 2285,
      "name": "BirthRecordsCountReportCBLevel",
      "url": "url",
      "displayName": "Birth Records Count CBLevel",
      "orderNumber": 9,
      "parentModule": "rainmaker-bnd",
      "enabled": true,
      "serviceCode": "bnd",
      "code": "null",
      "path": "cbbnd.BirthRecordsCountReportCBLevel",
      "navigationURL": "report/rainmaker-bnd/BirthRecordsCountReportCBLevel",
      "leftIcon": "action:assignment",
      "rightIcon": ""
    },
    {
      "id": 2286,
      "name": "DeathRecordsCountReportCBLevel",
      "url": "/report/rainmaker-bnd/DeathRecordsCountReportCBLevel/_get",
      "displayName": "DeathRecordsCountReportCBLevel",
      "orderNumber": 2,
      "parentModule": "",
      "enabled": true,
      "serviceCode": "report",
      "code": "null",
      "path": ""
    },
    {
      "id": 2287,
      "name": "DeathRecordsCountReportCBLevel",
      "url": "/report/rainmaker-bnd/DeathRecordsCountReportCBLevel/metadata/_get",
      "displayName": "DeathRecordsCountReportCBLevel",
      "orderNumber": 2,
      "parentModule": "",
      "enabled": true,
      "serviceCode": "report",
      "code": "null",
      "path": ""
    },
    {
      "id": 2288,
      "name": "DeathRecordsCountReportCBLevel",
      "url": "url",
      "displayName": "Death Records Count CBLevel",
      "orderNumber": 9,
      "parentModule": "rainmaker-bnd",
      "enabled": true,
      "serviceCode": "bnd",
      "code": "null",
      "path": "cbbnd.DeathRecordsCountReportCBLevel",
      "navigationURL": "report/rainmaker-bnd/DeathRecordsCountReportCBLevel",
      "leftIcon": "action:assignment",
      "rightIcon": ""
    },
    {
      "id": 2289,
      "name": "BirthAndDeathCertificatePayment",
      "url": "/report/rainmaker-bnd/BirthAndDeathCertificatePayment/metadata/_get",
      "displayName": "Birth-Death Payment Report",
      "orderNumber": 3,
      "parentModule": "",
      "enabled": true,
      "serviceCode": "report",
      "code": "null",
      "path": ""
    },
    {
      "id": 2290,
      "name": "BirthAndDeathCertificatePayment",
      "url": "url",
      "displayName": "BnD Paid and Downloaded Records",
      "orderNumber": 9,
      "parentModule": "rainmaker-bnd",
      "enabled": true,
      "serviceCode": "bnd",
      "code": "null",
      "path": "cbbnd.BirthAndDeathCertificatePayment",
      "navigationURL": "report/rainmaker-bnd/BirthAndDeathCertificatePayment",
      "leftIcon": "action:assignment",
      "rightIcon": ""
    },
```

**In action-test.json:**

```
{
      "rolecode": "BIRTH_REPORT_VIEWER",
      "actionid": 2277,
      "actioncode": "",
      "tenantId": "pb"
    },
    {
      "rolecode": "BIRTH_REPORT_VIEWER",
      "actionid": 2278,
      "actioncode": "",
      "tenantId": "pb"
    },
    {
      "rolecode": "BIRTH_REPORT_VIEWER",
      "actionid": 2283,
      "actioncode": "",
      "tenantId": "pb"
    },
    {
      "rolecode": "BIRTH_REPORT_VIEWER",
      "actionid": 2285,
      "actioncode": "",
      "tenantId": "pb"
    },
    {
      "rolecode": "BIRTH_REPORT_VIEWER",
      "actionid": 2284,
      "actioncode": "",
      "tenantId": "pb"
    },
    {
      "rolecode": "BIRTH_REPORT_VIEWER",
      "actionid": 2289,
      "actioncode": "",
      "tenantId": "pb"
    },
    {
      "rolecode": "BIRTH_REPORT_VIEWER",
      "actionid": 2325,
      "actioncode": "",
      "tenantId": "pb"
    },
    {
      "rolecode": "DEATH_REPORT_VIEWER",
      "actionid": 2280,
      "actioncode": "",
      "tenantId": "pb"
    },
    {
      "rolecode": "DEATH_REPORT_VIEWER",
      "actionid": 2281,
      "actioncode": "",
      "tenantId": "pb"
    },
    {
      "rolecode": "DEATH_REPORT_VIEWER",
      "actionid": 2286,
      "actioncode": "",
      "tenantId": "pb"
    },
    {
      "rolecode": "DEATH_REPORT_VIEWER",
      "actionid": 2287,
      "actioncode": "",
      "tenantId": "pb"
    },
    {
      "rolecode": "DEATH_REPORT_VIEWER",
      "actionid": 2289,
      "actioncode": "",
      "tenantId": "pb"
    },
    {
      "rolecode": "DEATH_REPORT_VIEWER",
      "actionid": 2290,
      "actioncode": "",
      "tenantId": "pb"
    },
    {
      "rolecode": "DEATH_REPORT_VIEWER",
      "actionid": 2325,
      "actioncode": "",
      "tenantId": "pb"
    }
```

* [x] Restart the MDMS and report service.

**Above is the sample for Defaulter Report. In a similar way, other reports can also be configured.**

## **Reference Docs** <a href="#reference-docs" id="reference-docs"></a>

### **Doc Links**

| Title                                                                                                                       | Link                                                                                                                                                                                                                      |
| --------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
|  [reportFileLocationsv1](https://raw.githubusercontent.com/egovernments/configs/DEV/reports/reportFileLocationsv1.txt) file | [<img src="https://github.com/fluidicon.png" alt="" data-size="line">configs/reportFileLocationsv1.txt at UAT · egovernments/configs](https://github.com/egovernments/configs/blob/UAT/reports/reportFileLocationsv1.txt) |
|  report config folder                                                                                                       | [<img src="https://github.com/fluidicon.png" alt="" data-size="line">configs/reports/config at UAT · egovernments/configs](https://github.com/egovernments/configs/tree/UAT/reports/config)                               |
| Report service                                                                                                              | [Report Service](broken-reference)                                                                                                                                                                                        |

