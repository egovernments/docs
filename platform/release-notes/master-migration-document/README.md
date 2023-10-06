---
description: 2.9 release master migration document
---

# Master Migration Document

## **Overview**

This page contains the changes related to core and municipal services along with the MDMS, DevOps and configuration setups required to accommodate multi-tenancy. Browse through the details below to learn more about the Central Instance.&#x20;

Refer to[ SAAS Guidelines for Central Instance](https://app.gitbook.com/o/-MEQmzNGXk5ajuZujG7E/s/F18990sRPMwVnnjjJxWc/\~/changes/18/platform/release-notes/master-migration-document/saas-guideliness-cental-instance) to find additional information.

## Migration Steps

### **Service-request Module - Citizen Feedback Module**

The service-request module is required for the surveys to work.\
Follow the steps given below:

1. Add the [Service-request module](../../configure-digit/configuring-digit-services/citizen-engagement-configuration/service-request.md)
2. Add the new persister file: [service-request-persister](https://github.com/egovernments/configs/blob/UAT/egov-persister/service-request-persister.yml)
3. Add the [Helm chart](https://github.com/egovernments/DIGIT-DevOps/tree/master/deploy-as-code/helm/charts/core-services/service-request)&#x20;
4. Configure the build&#x20;

{% code lineNumbers="true" %}
```yaml
- name: "builds/digit-dev/core-services/service-request"
    build:
      - work-dir: "core-services/service-request"
        image-name: "service-request"
        dockerfile: "build/maven/Dockerfile"
      - work-dir: "core-services/service-request/src/main/resources/db"
        image-name: "service-request-db"
```
{% endcode %}

5. Make the role action-mapping changes in the MDMS

[Access Control Actions Test](https://github.com/egovernments/egov-mdms-data/blob/UAT/data/pg/ACCESSCONTROL-ACTIONS-TEST/actions-test.json#L14597)

[Access Control Role Actions](https://github.com/egovernments/egov-mdms-data/blob/UAT/data/pg/ACCESSCONTROL-ROLEACTIONS/roleactions.json#L25805)

6. Click on the Job-builder once the above steps are complete.
7. Restart the following services: egov-accesscontrol, egov-mdms-service, egov-persister
8.  Deploy the service-request module build

    For further details on how to use Citizen-feedback APIs refer to the [Citizen Feedback service](../../configure-digit/configuring-digit-services/citizen-engagement-configuration/citizen-feedback-service.md).
9. Create the Citizen Feedback Service definitions (as mentioned in the above Citizen Feedback Service document) for modules and flows as per requirement before using it on the UI.

{% hint style="info" %}
**Note:** Service definition creation is a backend task that requires sending an API request using tools like Postman. This task is typically performed once during the initial setup process.
{% endhint %}

### **New KPIs**

1. Refer to [KPIs: Pendancy, Citizen Feedback and Pt-SLA changes](../../configure-digit/configuring-digit-services/national-dashboard-service-configuration/kpis-pendancy-citizen-feedback-and-sla-changes.md) and make changes as per the document.
2. Restart dashboard analytics with Cluster-configs.

### **UI Migration Changes**

* **Central Instance:**

Find the details for prepping the UI build for a new instance.

[UI build preparation for a new instance](../../configure-digit/configuring-digit-services/central-instance-configuration/ui-build-preparation-for-new-instance.md)

* **Citizen Consent Form:**

This feature allows citizen users to give their consent at the time of logging in.

Add this MDMS [file](https://github.com/egovernments/egov-mdms-data/blob/QA/data/pb/common-masters/CitizenConsentForm.json)&#x20;

**Documentation:**\
a. Refer to [Citizen Consent Form](../../configure-digit/configuring-digit-services/citizen-engagement-configuration/citizen-consent-form-ui.md)\
b. Restart MDMS and deploy the latest front-end builds.

* **Citizen Feedback:**

A functionality that allows users to provide the user facility to submit feedback/ratings at the end of the service.

Add the MDMS file available here: [https://github.com/egovernments/egov-mdms-data/blob/QA/data/pb/common-masters/RatingAndFeedback.json](https://github.com/egovernments/egov-mdms-data/blob/QA/data/pb/common-masters/RatingAndFeedback.json)

{% code lineNumbers="true" %}
```json
{
  "tenantId": "pb",
  "moduleName": "common-masters",
  "RatingAndFeedback": [
    {
      "type": "isCitizenRatingEnabled",
      "value": true
    },
    {
      "type": "headerByRating",
      "value": [
        {
          "minvalue": 1,
          "maxvalue": 3,
          "code": "CS_WHAT_WENT_WRONG"
        },
        {
          "minvalue": 4,
          "maxvalue": 5,
          "code": "CS_WHAT_WENT_GOOD"
        }
      ]
    },
    {
      "type": "enabledScreensList",
      "value": [
        {
          "module": "PT",
          "bussinessService": "PT_CREATE",
          "screenfrom": "pt/property/new-application/acknowledgement",
          "cardHeader": "PT_RATE_HELP_TEXT_CREATE",
          "cardText": "PT_RATE_CARD_TEXT_CREATE"
        },
        {
          "module": "PT",
          "bussinessService": "PT_MUTATION",
          "screenfrom": "pt/property/property-mutation/acknowledgement",
          "cardHeader": "PT_RATE_HELP_TEXT_MUTATE",
          "cardText": "PT_RATE_CARD_TEXT_MUTATE"
        },
        {
          "module": "PT",
          "bussinessService": "PT_UPDATE",
          "screenfrom": "pt/property/edit-application/acknowledgement",
          "cardHeader": "PT_RATE_HELP_TEXT_UPDATE",
          "cardText": "PT_RATE_CARD_TEXT_UPDATE"
        },
        {
          "module": "PT",
          "bussinessService": "PT",
          "screenfrom": "digit-ui/citizen/payment/success",
          "cardHeader": "PT_RATE_HELP_TEXT_PAY",
          "cardText": "PT_RATE_CARD_TEXT_PAY"
        }
      ]
    }
  ]
}
```
{% endcode %}

In the provided configuration, the parameter `headerByRating` is utilized to specify the value for the star condition, along with the corresponding message to be displayed on the UI screen. The `enabledScreensList` parameter is used to indicate the specific flows where the Citizen feedback screen will be presented, allowing citizens to provide reviews.

The rating component is utilized for displaying star ratings on the citizen feedback screen. You can locate this component within the micro-ui-internals folder on the following GitHub link: [Rating.js](https://github.com/egovernments/DIGIT-Dev/blob/develop/frontend/micro-ui/web/micro-ui-internals/packages/react-components/src/atoms/Rating.js).

**Documentation**

a. Refer to [Citizen Feedback Documentation](../../configure-digit/configuring-digit-services/citizen-engagement-configuration/citizen-feedback-ui.md) for more details.

b. Restart MDMS and deploy the latest front-end builds.

&#x20;

&#x20;
