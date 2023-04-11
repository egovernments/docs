---
description: 2.8 release master migration document
---

# Master Migration Document

## **Bill Amendment (Billing-service)**&#x20;

W\&S Bill Amendment workflow config migration&#x20;

* Follow the steps mentioned in the [W\&S Bill Amendment Workflow config migration document](../configure-digit/configuring-digit-services/water-services/workflow-config-replacement-data.md).
* Verify once if workflow name is hardcoded except edited parts of UI, Backend - check in indices and report - checked not present except config&#x20;
* Verify if wf config is there for tenant level or state level only
* An update has to be added as a patch to the first release of the amendment

## **Water & Sewerage**

* Latest persister file **-** [**Water**](https://github.com/egovernments/configs/blob/UAT/egov-persister/water-persist.yml)
* Latest persister file **-** [**Sewerage**](https://github.com/egovernments/configs/blob/UAT/egov-persister/sewerage-persist.yml)

{% hint style="info" %}
**Note :** `Replace the existing persister files with the latest files linked above.`
{% endhint %}

* **Water modify connection**
  * [**Workflow config**](https://github.com/egovernments/DIGIT-Dev/blob/master/municipal-services/ws-services/src/main/resources/workflowconfigs/PostmanScriptWorkflowModifyConnection.json)
* **Sewerage modify connection**
  * [**Workflow config**](https://github.com/egovernments/DIGIT-Dev/blob/master/municipal-services/sw-services/src/main/resources/workflowconfigs/PostmanScriptWorkflowModifyConnection.json)
* **Sewerage Disconnection**
  * [**Workflow config**](https://github.com/egovernments/DIGIT-Dev/blob/master/municipal-services/sw-services/src/main/resources/workflowconfigs/PostmanScriptWorkflowSewerageDisconnection.json)
* **Water Disconnection**
  * [**Workflow config**](https://github.com/egovernments/DIGIT-Dev/blob/master/municipal-services/ws-services/src/main/resources/workflowconfigs/PostmanScriptWorkflowWaterDisconnection.json)

## **Privacy Feature**&#x20;

**By default encryption & privacy is disabled for 2.8**

* To disable privacy for Property and W\&S make changes in the MDMS- DataSecurity -> SecurityPolicy.json file.
* For models- Property,PropertyDecrypDisabled, WnSConnection, WnSConnectionOwner, WnSConnectionDecrypDisabled, WnSConnectionOwnerDecrypDisabled, WnSConnectionPlumber, WnSConnectionPlumberDecrypDisabled; insert only one attribute in the attributeList as follows:

```
 {
         "name": "sample",
         "jsonPath": "sample",
         "patternId": null,
         "defaultVisibility": "PLAIN"
    }

```

* Insert the name and jsonPath which are not actually expected to be present in the RequestBody/ResponseBody
* **Files to be updated**
  1. [Security policy complete file](https://github.com/egovernments/egov-mdms-data/blob/UAT/data/pg/DataSecurity/SecurityPolicy.json)
  2. [Masking patterns](https://github.com/egovernments/egov-mdms-data/blob/UAT/data/pg/DataSecurity/MaskingPatterns.json) - needed only if enc is enabled and carried our for old data.
* **References for reading**
  1. [PT,W\&S decryption policy](https://github.com/egovernments/egov-mdms-data/blob/428e57bb105c9341ddb8763e39c73b2dc24f997c/data/pg/DataSecurity/SecurityPolicy.json#L332-L412)
  2. [Decryption Disabled config for PT,W\&S](https://github.com/egovernments/egov-mdms-data/blob/428e57bb105c9341ddb8763e39c73b2dc24f997c/data/pg/DataSecurity/SecurityPolicy.json#L575-L621)
  3. [W\&S Plumber enc/dec](https://github.com/egovernments/egov-mdms-data/blob/428e57bb105c9341ddb8763e39c73b2dc24f997c/data/pg/DataSecurity/SecurityPolicy.json#L776-L818)
  4. [Inbox decryption config](https://github.com/egovernments/egov-mdms-data/blob/428e57bb105c9341ddb8763e39c73b2dc24f997c/data/pg/DataSecurity/SecurityPolicy.json#L504-L525)
  5. [Reindexing enc/dec config](https://github.com/egovernments/egov-mdms-data/blob/428e57bb105c9341ddb8763e39c73b2dc24f997c/data/pg/DataSecurity/SecurityPolicy.json#L92-L102)
* Once the above changes are done deploy the following builds:
  1. **Ws-services**
  2. **Property-services**
  3. **Sw-services**
  4. **Inbox**
  5. Restart **egov-user service**
*   Impact of privacy framework&#x20;

    1. The privacy implementation masks the PII information based on the MDMS config ([Security Policy](https://github.com/egovernments/egov-mdms-data/blob/QA/data/pb/DataSecurity/SecurityPolicy.json))
    2. The masking/unmasking of data is entirely dependent on the roles of the users in the system, adding or removing these roles from the config will enable masking for each role.
    3. There is no module-level control here, so if a W\&S role is added to an employee of TL then data will be masked so cross-using of roles should be avoided.
    4. The agreement with Manish is that the privacy be disabled until redesign with the module filter - Done
    5. The policy should be defined for adding or removing fields from the encryption process.



    <figure><img src="../../.gitbook/assets/image (511).png" alt=""><figcaption></figcaption></figure>
* **W\&S privacy (Skip over if encryption is not carried out)**
  1. Deploy the latest builds provided for the 2.8 release {builds}
  2. Add privacy configs to MDMS ([**SecurityPolicy.json**](https://github.com/egovernments/egov-mdms-data/blob/QA/data/pb/DataSecurity/SecurityPolicy.json))
  3. Restart the MDMS service followed by the encryption service
  4. Add the temporary [index config](https://github.com/egovernments/configs/blob/DEV/egov-indexer/sewerage-service.yml#L425) update index with encrypted data
     * This file will fetch data from the Encryption of old data and upload it to the existing index so that the index will be encrypted or masked as per config.
  5. Trigger the encryption of old data through the provided [APIs](https://www.getpostman.com/collections/b3858ec2020462a6407d)&#x20;
  6. Validating the encryption of old data **{Doc Link}**
  7. Disable & enable decryption.privacy
     * &#x20;`water.decryption.abac.enabled=`**true**&#x20;
     * `sewerage.decryption.abac.enabled=`**true**
* **PT privacy (Skip over if encryption is not carried out)**
  1. Deploy the latest builds provided for the 2.8 release
  2. Add privacy configs to MDMS ([**SecurityPolicy.json**](https://github.com/egovernments/egov-mdms-data/blob/QA/data/pb/DataSecurity/SecurityPolicy.json))
  3. Restart the MDMS service followed by the encryption service
  4. Add the temporary [index config](https://github.com/egovernments/configs/blob/DEV/egov-indexer/property-services.yml#L956) update index with encrypted data
  5. Add the new [index config](https://github.com/egovernments/configs/blob/DEV/egov-indexer/property-services.yml#L5) for the fuzzy search index&#x20;
  6. Trigger the encryption of old data through the provided [APIs ](https://api.postman.com/collections/3048487-e947e718-9808-4f48-985a-b71f3c101926?access\_key=PMAT-01GQKMHJKZBSG19C7HC8H2XPES)
  7. Validating the encryption of old data **{Doc Link}**
  8. Disable & enable decryptionprivacy&#x20;
     * `property-decryption-abac-enabled:` **"true"**
* **Bill genie**
  1. No changes required
* **Bulk Bill PDF Generation and Performance Testing**
  1. Enhancement is part of the new build release.
* **W\&S Bulk Bill Generation and Performance Testing**
  1. **PR List**&#x20;
     * [**W\&S calculators**](https://github.com/egovernments/DIGIT-Dev/pull/2742/files)
     * [Bug Fixes on calculators](https://github.com/egovernments/DIGIT-Dev/pull/3115)
     * [**Billing service**](https://github.com/egovernments/DIGIT-Dev/pull/2967/files)
     * [![](https://digit-discuss.atlassian.net/rest/api/2/universal\_avatar/view/type/issuetype/avatar/10303?size=medium)UM-1035: Bulk Bill Performance:: Bills are not generating after hitting the job scheduler API.SIGNED OFF](https://digit-discuss.atlassian.net/browse/UM-1035)
     * [![](https://digit-discuss.atlassian.net/rest/api/2/universal\_avatar/view/type/issuetype/avatar/10318?size=medium)UM-591: W\&S: Bulk bill performance fixes merge it to product from 2.3 (Odisha branch) and testSIGNED OFF](https://digit-discuss.atlassian.net/browse/UM-591)
* **privacy integration - PT**
  1. **Covered as part of privacy above**
* **Notification based on channels - PGR**
  1. Localisation added as part of the release KIT
* **Notification based on channels - mCollect**
  1. Localisation added as part of the release KIT
* _**OBPS/ BPA (Notifications only)**_
  1. _Localisation added as part of the release KIT_
* **National Dashboard Adaptor Integration Testing**
  1. The [Docs](../configure-digit/configuring-digit-services/national-dashboard-service-configuration/national-dashboard-ingest-service/national-dashboard-adaptor-service.md) are specific to Punjab implementation, generic product document is in the pipeline.
* **NationalDashBoard 3 New KPI**
  1. [**CharApiConfig.json**](https://github.com/egovernments/configs/blob/17bec4912246fa073c212c3d440dbed7e47abb88/egov-dss-dashboards/dashboard-analytics/ChartApiConfig.json#L18200-L18445)
  2. **MasterDashboardConfig.json**
     * [**Overview Card config**](https://github.com/egovernments/configs/blob/17bec4912246fa073c212c3d440dbed7e47abb88/egov-dss-dashboards/dashboard-analytics/MasterDashboardConfig.json#L337-L352)
     * [**Property Tax config**](https://github.com/egovernments/configs/blob/17bec4912246fa073c212c3d440dbed7e47abb88/egov-dss-dashboards/dashboard-analytics/MasterDashboardConfig.json#L1046-L1053)
  3. [**DevOps change**](https://github.com/egovernments/DIGIT-DevOps/blob/a94e465d8f3bd5f29a0bf4c76f37611d2934f9f1/deploy-as-code/helm/environments/uat.yaml#L340)
* **Finance Module State DSS**
  1. [**Dss Chart API config**](https://github.com/egovernments/configs/blob/UAT/egov-dss-dashboards/dashboard-analytics/ChartApiConfig.json#L17899)
* **MDMS & Configs -**
  1. [_**Complete Localisation**_](https://github.com/egovernments/releasekit/pull/82/files)
  2. [_**Complete MDMS**_ ](https://github.com/egovernments/egov-mdms-data/pull/2936)
  3. [_**Complete configs**_](https://github.com/egovernments/configs/pull/2547)

**BackWard Compatibility Results** -

* [_**Folder Link**_](https://drive.google.com/drive/folders/131NQZOGOjNQMT8qLci53yi-UFfe5CPDk)

**UI Changes**

Please add all MDMS changes before deploying the UI code.

* **W\&S: W\&S UI/UX Revamp**
  * No changes are needed, it will work automatically if we deploy. There are two enhancements in the W\&S flow, i.e Edit by normal user and Edit by config user, it is based on the MDMS configuration ([Link](https://github.com/egovernments/egov-mdms-data/blob/UAT/data/pg/ws-services-masters/WSEditApplicationByConfigUser.json)). This is applicable in all 3 flows.
* **W\&S disconnection**
  * No changes needed, it will work automatically if we deploy.
* **Bill amendment W\&S UI/UX Revamp**I
  * No changes needed, it will work automatically if we deploy.
* **Bill Genie UI/UX revamp**
  * No changes needed, it will work automatically if we deploy.
* **OBPS Tabular Reports in old**
  * No changes needed, it will work automatically if we deploy. It is based on the configuration of the backend.
* **TL Tabular Reports**
  * No changes are needed, it will work automatically if we deploy. It is based on the configuration of the backend.
* **Standard Reports for WnS**
  * No changes are needed, it will work automatically if we deploy. It is based on the configuration of the backend.
* **Core UI Changes (Banner Images of Each module)**
  * No changes are needed, it will work automatically if we deploy. It is based on the configuration of the MDMS ([Link](https://github.com/egovernments/egov-mdms-data/blob/UAT/data/pg/tenant/citymodule.json))
  * We need to add the below images in the S3 bucket:PGR: [https://egov-uat-assets.s3.amazonaws.com/PGR.png](https://egov-uat-assets.s3.amazonaws.com/PGR.png)
  * PT: [https://egov-uat-assets.s3.amazonaws.com/PT.png](https://egov-uat-assets.s3.amazonaws.com/PT.png)
  * TL: [https://egov-uat-assets.s3.amazonaws.com/TL.png](https://egov-uat-assets.s3.amazonaws.com/TL.png)
  * OBPS: [https://egov-uat-assets.s3.amazonaws.com/OBPS.png](https://egov-uat-assets.s3.amazonaws.com/OBPS.png)
  * FSM: [https://egov-uat-assets.s3.amazonaws.com/FSM.png](https://egov-uat-assets.s3.amazonaws.com/FSM.png)
  * WS: [https://egov-uat-assets.s3.amazonaws.com/WS.png](https://egov-uat-assets.s3.amazonaws.com/WS.png)
  * Bills: [https://egov-uat-assets.s3.amazonaws.com/Bill.png](https://egov-uat-assets.s3.amazonaws.com/Bill.png)
* **Navigation re-direction from New UI to OLD UI**I. Mdms Changes are required for this ([Link](https://digit-discuss.atlassian.net/wiki/spaces/DD/pages/2299756623/Navigation+between+Old+and+New+UI.)).

**Old UI**

Only Fire Noc and Tabular reports are PO signed off in the current release for the OLD UI, the rest of the modules are covered as part of backward compatibility tests shared above.

