---
description: UI build preparation details for central instance
---

# UI Build Preparation For New Instance

## **Overview**

This page offers comprehensive instructions on preparing the UI build for the central instance. Follow the steps outlined in the respective sections below to successfully configure this setup.

## Steps

**Code Path:** [egovernments/DIGIT-Dev](https://github.com/egovernments/DIGIT-Dev)

### Step 1. Generate G**lobal Configuration File**

A global configuration file should be generated for each instance.\
**Example:** UAT instance s3 bucket file Path: [https://s3.ap-south-1.amazonaws.com/egov-uat-assets/globalConfigs.js](https://s3.ap-south-1.amazonaws.com/egov-uat-assets/globalConfigs.js)

Add the below content to this file.

{% code lineNumbers="true" %}
```json
var globalConfigs = (function () {
      var stateTenantId = 'pg'
      var gmaps_api_key_old = 'AIzaSyAQOd09-vjmk1sXFb_ZQYDz2nlfhXq7Wf8'
      var gmaps_api_key = 'AIzaSyASqkAr3d494ihZaJeCOg4CJ3xnQ_83e2s'
      var finEnv = 'uat'
      var centralInstanceEnabled = false;
      var footerBWLogoURL = 'https://s3.ap-south-1.amazonaws.com/egov-uat-assets/digit-footer-bw.png'
      var footerLogoURL = 'https://s3.ap-south-1.amazonaws.com/egov-uat-assets/digit-footer.png'
      var digitHomeURL = 'https://www.digit.org/'
      var assetS3Bucket = 'pg-egov-assets';


      var getConfig = function (key) {
        if (key === 'STATE_LEVEL_TENANT_ID') {
          return stateTenantId;
        }
        else if (key === 'GMAPS_API_KEY') {
          return gmaps_api_key;
        }
        else if (key === 'FIN_ENV') {
          return finEnv;
        } else if (key === 'ENABLE_SINGLEINSTANCE') {
          return centralInstanceEnabled;
        } else if (key === 'DIGIT_FOOTER_BW') {
          return footerBWLogoURL;
        } else if (key === 'DIGIT_FOOTER') {
          return footerLogoURL;
        } else if (key === 'DIGIT_HOME_URL') {
          return digitHomeURL;
        } else if (key === 'S3BUCKET') {
          return assetS3Bucket;
        } else if (key === "JWT_TOKEN"){
          return "ZWdvdi11c2VyLWNsaWVudDo=";
        }
      };


      return {
        getConfig
      };
}());
```
{% endcode %}

In this file -

1. Change the **“stateTenantId”** value as per instance; in this instance, it should be **‘pg’**.
2. Change the **“finEnv”** value based on the specific instance; in this instance, it should be **‘uat’.**
3. Change the **“footerBWLogoURL”** value as per instance requirements; in this instance, it should be **‘'**[**https://s3.ap-south-1.amazonaws.com/egov-uat-assets/digit-footer-bw.png**](https://s3.ap-south-1.amazonaws.com/egov-uat-assets/digit-footer-bw.png)**'’** (this is s3 link for footer image).
4. Change the **“footerLogoURL”** value as per instance requirements; for this instance, it is **‘'**[**https://s3.ap-south-1.amazonaws.com/egov-uat-assets/digit-footer.png**](https://s3.ap-south-1.amazonaws.com/egov-uat-assets/digit-footer.png)**'’** (this is the s3 link for footer image).
5. Modify the "**digitHomeURL**" according to the instance requirements; in this instance, it should be set to "Coming Soon."
6. Change the "**assetS3Bucket**" value based on the specific instance; in this case, it should be set as "pg-egov-assets."
7. To modify the Google Maps key, you should make the necessary changes in the "**gmaps\_api\_key**" field.
8. If the "**centralInstanceEnabled**" parameter is configured as "false," the default behaviour of the logic will be active in the UI. Conversely, if the "**centralInstanceEnabled**" parameter is configured as "true," the central instance logic will come into effect.

The DevOps team generates this file as part of the new instance creation process. Finally, the file path is incorporated into the environment folder within the DevOps repository.\
\
**Example:** DIGIT UI repo path: [egovernments/DIGIT-DevOps](https://github.com/egovernments/DIGIT-DevOps)\
**UAT File Path:** [<img src="https://github.githubassets.com/favicon.ico" alt="" data-size="line">uat.yaml](https://github.com/egovernments/DIGIT-DevOps/blob/master/deploy-as-code/helm/environments/uat.yaml)\
\
These details are essential for the creation of a new instance build.

### Step 2. **Enable Modules**&#x20;

Activate the modules by utilizing the MDMS configuration, toggling the parameters to either "true" or "false."\
MDMS file path of UAT: [<img src="https://github.githubassets.com/favicon.ico" alt="" data-size="line">citymodule.json](https://github.com/egovernments/egov-mdms-data/blob/UAT/data/pg/tenant/citymodule.json)





