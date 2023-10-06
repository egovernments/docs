---
description: Service build details for 2.9 Release
---

# Service Build Updates

## S**ervice Builds 2.9**&#x20;

| Category                                                                                                  | Services                            | Docker Artefact ID                                       | Remarks     |
| --------------------------------------------------------------------------------------------------------- | ----------------------------------- | -------------------------------------------------------- | ----------- |
| **Frontend (old UI)** [**v2.9**](https://github.com/egovernments/DIGIT-OSS/tree/v2.9/frontend/mono-ui)    | Citizen                             | citizen:v1.10.0-beta-90968a5987-33                       |             |
|                                                                                                           | Employee                            | employee:v1.10.0-beta-90968a5987-45                      |             |
|                                                                                                           | DSS Dashboard                       | dss-dashboard:v1.10.0-beta-0ad561e837-4                  |  unchanged  |
| **Digit-UI** [**v2.9**](https://github.com/egovernments/DIGIT-OSS/tree/v2.9/frontend/micro-ui)            | DIGIT UI                            | digit-ui:v1.7.0-beta.2-6e3654830c-511                    |             |
| **Core Services** [**v2.9**](https://github.com/egovernments/Digit-Core/releases/tag/urban\_v2.9)         | Service-request                     | service-request:v1.0.0\_beta-cddd1fb55c-12               |   unchanged |
|                                                                                                           | Signed Audit                        | audit-service:v1.0.0-24873ba-3                           |  unchanged  |
|                                                                                                           | Encryption                          | egov-enc-service:v1.1.4-1f3649156d-5                     |             |
|                                                                                                           | xState Chatbot                      | xstate-chatbot:v1.1.1-44558a0602-1                       |             |
|                                                                                                           | Searcher                            | egov-searcher:v1.1.6-bc771ff4d4-6                        |             |
|                                                                                                           | Payment Gateway                     | egov-pg-service:v1.2.3-ffbb7a6-2                         |             |
|                                                                                                           | Filestore                           | egov-filestore:v1.2.4-9934605-2                          |             |
|                                                                                                           | Zuul - API Gateway                  | zuul:v1.3.1-76bf31f-2                                    |             |
|                                                                                                           | Mail Notification                   | egov-notification-mail:v1.2.0-9fde481c92-1               |             |
|                                                                                                           | SMS Notification                    | egov-notification-sms:v1.2.0-9fde481c92-2                |             |
|                                                                                                           | Localization                        | egov-localization:v1.1.3-44558a0602-2                    |             |
|                                                                                                           | Persist                             | egov-persister:v1.1.6-1f3649156d-3                       |             |
|                                                                                                           | ID Gen                              | egov-idgen:v1.2.3-44558a0602-2                           |             |
|                                                                                                           | User                                | egov-user:v1.2.8-9fde481c92-2                            |             |
|                                                                                                           | User Chatbot                        | egov-user-chatbot:v1.2.8-9fde481c92-2                    |             |
|                                                                                                           | MDMS                                | egov-mdms-service:v1.3.3-1f3649156d-4                    |             |
|                                                                                                           | URL Shortening                      | egov-url-shortening:v1.1.2-010cd85ad6-3                  |             |
|                                                                                                           | Indexer                             | egov-indexer:v1.1.8-36a0a061fd-34                        |             |
|                                                                                                           | Report                              | report:v1.3.6-3ad63f2273-4                               |             |
|                                                                                                           | Workflow                            | egov-workflow-v2:v1.3.1-1f3649156d-5                     |             |
|                                                                                                           | PDF Generator                       | pdf-service-db:v1.2.2-5d71b59949-18                      |             |
|                                                                                                           | Chatbot                             | chatbot:v1.1.6-44558a0602-1                              |             |
|                                                                                                           | Access Control                      | egov-accesscontrol:v1.1.3-852f5ea3a0-3                   |             |
|                                                                                                           | Location                            | egov-location:v1.1.5-fbea79700d-1                        |             |
|                                                                                                           | OTP                                 | egov-otp:v1.2.3-9fde481c92-1                             |             |
|                                                                                                           | User OTP                            | user-otp:v1.2.1-1f3649156d-2                             |             |
|                                                                                                           | NLP Engine                          | nlp-engine:v1.0.0-fbea6fba-21                            | unchanged   |
|                                                                                                           | Egov Document-Uploader              | egov-document-uploader:v1.0.1-a1ef7d4187-1               |             |
|                                                                                                           | National Dashboard Ingest           | national-dashboard-ingest:v1.0.1-44558a0-4               |             |
|                                                                                                           | National Dashboard Kafka Pipeline   | national-dashboard-kafka-pipeline:v1.0.1-44558a0-4       |             |
|                                                                                                           | Egov Survey Service                 | egov-survey-services:v0.0.1-a9d54c2543-25                | unchanged   |
|                                                                                                           | Internal Gateway                    | internal-gateway:v0.0.1-44558a0-3                        |             |
| **Business Services** [**v2.9**](https://github.com/egovernments/Digit-Core/releases/tag/urban\_v2.9)     | Apportion                           | egov-apportion-service:v1.1.5-44558a0602-1               |             |
|                                                                                                           | Collection                          | collection-services:v1.1.6-855dc9a-2                     |             |
|                                                                                                           | Billing                             | billing-service-db:v1.3.5-a4d411ecd0-16                  |             |
|                                                                                                           | HRMS                                | egov-hrms:v1.2.7-bc771ff4d4-4                            |             |
|                                                                                                           | Dashboard Analytics                 | dashboard-analytics:v1.1.9-aea1817792-10                 |             |
|                                                                                                           | Dashboard Ingest                    | national-dashboard-ingest:v1.0.1-44558a0-4               |             |
|                                                                                                           | EGF Instrument                      | egf-instrument:v1.1.4-d93a120c25-2                       | unchanged   |
|                                                                                                           | EGF Master                          | egf-master:v1.1.3-d93a120c25-2                           | unchanged   |
|                                                                                                           | Finance Collection Voucher Consumer | finance-collections-voucher-consumer:v1.1.6-d93a120c25-4 |             |
| **Municipal Services** [**v2.9**](https://github.com/egovernments/DIGIT-OSS/tree/v2.9/municipal-services) | Trade License                       | tl-services:v1.1.9-a7462eff5a-7                          |             |
|                                                                                                           | Trade License Calculator            | tl-calculator:v1.1.6-3ad63f2273-4                        |             |
|                                                                                                           | Fire NOC                            | firenoc-services-db:v1.3.3-4550d93cde-34                 |             |
|                                                                                                           | Fire NOC Calculator                 | firenoc-calculator:v1.2.3-3ad63f2273-13                  |             |
|                                                                                                           | Property Services                   | property-services:v1.2.2-a7462eff5a-57                   |             |
|                                                                                                           | Property Tax Calculator             | pt-calculator-v2:v1.1.6-3ad63f2273-10                    |             |
|                                                                                                           | Property Tax                        | property-services:v1.2.2-8566918dfc-66                   |             |
|                                                                                                           | Water Charges                       | ws-services:v1.7.5-a7462eff5a-20                         |             |
|                                                                                                           | Water Charges Calculator            | ws-calculator:v1.4.4-3ad63f2273-13                       |             |
|                                                                                                           | Sewerage Charges                    | sw-services:v1.7.5-a7462eff5a-14                         |             |
|                                                                                                           | Sewerage Charges Calculator         | sw-calculator:v1.4.4-a7462eff5a-18                       |             |
|                                                                                                           | BPA Calculator                      | bpa-calculator:v1.1.2-3ad63f2273-7                       |             |
|                                                                                                           | BPA Services                        | bpa-services:v1.1.7-a7462eff5a-18                        |             |
|                                                                                                           | User Event                          | egov-user-event:v1.2.0\_beta-97005a72ec-3                |             |
|                                                                                                           | PGR                                 | rainmaker-pgr:v1.1.4\_beta-e3769f2e9f-1                  |             |
|                                                                                                           | PGR Service                         | pgr-services:v1.1.8-3ad63f2273-7                         |             |
|                                                                                                           | Land Services                       | land-services:v1.0.5-3ad63f2273-6                        |             |
|                                                                                                           | NOC Services                        | noc-services:v1.0.6-3ad63f2273-11                        |             |
|                                                                                                           | FSM                                 | fsm:v1.2.0-98a12c2748-224                                | unchanged   |
|                                                                                                           | FSM Calculator                      | fsm-calculator:v1.1.0-32caf0d992-41                      | unchanged   |
|                                                                                                           | Vehicle                             | vehicle:v1.2.0-180a328097-97                             | unchanged   |
|                                                                                                           | Vendor                              | vendor:v1.2.0-a28b192446-64                              | unchanged   |
|                                                                                                           | eChallan Services                   | echallan-services:v1.1.1-a7462eff5a-14                   |             |
|                                                                                                           | eChallan Calculator                 | echallan-calculator:v1.0.3-3ad63f2273-5                  |             |
|                                                                                                           | Inbox                               | inbox:v1.3.1-1f3649156d-10                               |             |
|                                                                                                           | Turn-IO                             | turn-io-adapter:v1.0.1-3d7f744977-4                      |             |
|                                                                                                           | Birth and Death Services            | birth-death-services-db:v1.0.2-d43fa051aa-41             |             |
| **Utilities Services** [**v2.9**](https://github.com/egovernments/DIGIT-OSS/tree/v2.9/utilities)          | Custom Consumer                     | egov-custom-consumer:v1.1.1-d93a120c25-2                 |             |
|                                                                                                           | PDF                                 | egov-pdf:v1.2.1-cb236eaf66-8                             |             |
| **eDCR** [**v2.9**](https://github.com/egovernments/DIGIT-OSS/tree/v2.9-beta/edcr)                        | eDCR                                | egov-edcr:v2.1.2-bdebd6c5c1-26                           |             |
|  **Finance** [**v2.9**](https://github.com/egovernments/DIGIT-OSS/tree/v2.9/finance)                      | Finance                             | egov-finance:v3.0.2-3c708604d0-1                         |             |
| **Configs Stateb** [**v2.9**](https://github.com/egovernments/configs/releases/tag/urban\_v2.9)           |                                     |                                                          |             |
| **Configs Central** [**v2.9**](https://github.com/egovernments/configs/releases/tag/urban\_v2.9)          |                                     |                                                          |             |
| **MDMS StateB** [**v2.9**](https://github.com/egovernments/MDMS-TenantB/releases/tag/v2.9)                |                                     |                                                          |  unchanged  |
| **MDMS Central** [**v2.9**](https://github.com/egovernments/egov-mdms-data/releases/tag/v2.9)             |                                     |                                                          | unchanged   |
| **DevOps StateB** [**v.2.9**](https://github.com/egovernments/stateB-DevOps/releases/tag/v2.9)            |                                     |                                                          |             |
| **DevOps Central** [**v.2.9**](https://github.com/egovernments/DIGIT-DevOps/releases/tag/v2.9)            |                                     |                                                          |             |
| **Localization** [**v2.9**](https://github.com/egovernments/releasekit/releases/tag/v2.9)                 |                                     |                                                          | unchanged   |
| **QA Automation** [**v2.9**](https://github.com/egovernments/test-automation/releases/tag/v2.8)           |                                     |                                                          | unchanged   |

&#x20;
