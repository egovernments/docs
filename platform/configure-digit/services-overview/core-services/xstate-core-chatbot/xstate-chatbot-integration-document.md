# XState-Chatbot Integration Document

## Overview

The [XState-Chatbot](https://github.com/egovernments/core-services/tree/xstate-chatbot/xstate-chatbot) is a revamped version of the [chatbot](https://github.com/egovernments/core-services/tree/master/chatbot), which provides functionality to the user to access PGR module services like file complaints, track complaints, notifications from whats app,\
It allows the user to view receipts and pay the bills for Property, Trade Licence, FireNOC, Water and Sewerage and BPA service module.

## Key Functionalities

* File PGR complaint
* Track PGR complaint
* Support images when filing complaints
* Notifications to citizens when an employee performs any action on the complaint
* Allow users to search and pay bills of different modules.
* Allow users to search and view receipts of different modules.
* Allow users to change the language of their choice to have a better experience.
* Put user interactions on an elastic search for Telemetry.

## Integration Details

### Integration Scope <a href="#integration-scope" id="integration-scope"></a>

The XState chatbot can be integrated with any other module to improve the ease of search and view bills/past payment receipts and to improve speed and convenience for bill payment. It can be integrated with the PGR module for easiness of creation and tracking of the complaint.

### Integration Benefits

* Increase in convenience and ease of making the bill payment.
* Increase in no. of users opting for online payment.
* Improvement in demand collection efficiency
* Creating an additional channel for payment.
* Remove dependency on mobile/web apps or counters.

### Integration Approach <a href="#integration-details" id="integration-details"></a>

#### Integration of New Whatsapp Provider <a href="#integration-of-new-whatsapp-provider" id="integration-of-new-whatsapp-provider"></a>

Whatsapp provider is a third-party service that works in the middle of a user's WhatsApp client and XState-Chatbot server. All messages coming/going to/from the user pass through the WhatsApp provider. Chatbot calls WhatsApp provider to send messages to the user. When a user responds with any WhatsApp message the WhatsApp provider calls Chatbot service’s configured endpoint with details ex:- the user sent message, sender’s number etc.

If any new WhatsApp provider is to be used with a chatbot, code must be written to convert the provider’s incoming messages to the format that the chatbot understands and also final output from the chatbot should be converted to the WhatsApp provider’s API request format.

Currently, the XState-Chatbot service is using ValueFirst as the WhatsApp Provider. This will require provider-specific environment variables to be configured. If the provider changes then, all these environment variables will also change. A few of those environment variables are stored as secrets, so these values need to be configured in _env_-secrets.yaml.

As this is a revamped version of the chatbot service, all of the secrets should already be present. There is no need to create new secrets.

#### Integration of PGR complaint feature in XState-Chatbot <a href="#integration-of-pgr-complaint-feature-in-xstate-chatbot" id="integration-of-pgr-complaint-feature-in-xstate-chatbot"></a>

The integration of PGR with a chatbot can be enabled and disabled by making changes in this [file](https://github.com/egovernments/core-services/blob/xstate-chatbot/xstate-chatbot/nodejs/src/machine/service/service-loader.js).\
By exporting the respective PGR service file, the PGR service feature can be sable and vice versa.

## Configuration Details

**Configuration of PGR version in chatbot**

To configure the PGR module to use in Xstate-chatbot - the below variable values need to change in the [environment file](https://github.com/egovernments/eGov-infraOps/blob/master/helm/environments/qa.yaml#L207) as per the requirement.

* pgrVersion
* pgrUpdateTopic

To configure PGR v2 in XState chatbot then pgrVersion should be ‘v2' and pgrUpdateTopic should be 'update-pgr-request’.

**Configuration of city and locality search with nlp-search engine**

To enable the fuzzy search for city and locality selection in PGR complaint flow\
The variable **nlp-geoSearch** has to be set true in the [environment file](https://github.com/egovernments/DIGIT-DevOps/blob/master/deploy-as-code/helm/environments/qa.yaml#L221).\
To use the nlp-search engine with xstate chatbot, make sure that a stable build is deployed and all the mdms data are present for that particular environment.\
To know more about the nlp-search engine service please refer to the Reference document section.

**Adding Information Image in PGR complaint creation and Open search information image**

To configure the filestoreid for an informational image follow the steps mentioned below

1. Download the images from the section _**Information Images for PGR and Open Search**_
2. Upload the image into filestore server. Use the upload file API from this postman collection([https://www.getpostman.com/collections/bdb059c5af698f0d81d6)](https://www.getpostman.com/collections/bdb059c5af698f0d81d6)
3. For PGR information image mention the filestore id [here](https://github.com/egovernments/DIGIT-DevOps/blob/master/deploy-as-code/helm/environments/qa.yaml#L219) in the environment file.
4. For open search, the information image mentions the filestore id [here](https://github.com/egovernments/DIGIT-DevOps/blob/master/deploy-as-code/helm/environments/qa.yaml#L220) in the environment file.

**For example:**

a) if supportedLocales: process.env.SUPPORTED\_LOCALES || 'en\_IN,hi\_IN'

then valuefirst-notification-resolved-templateid: "12345,6789"

b) if supportedLocales: process.env.SUPPORTED\_LOCALES || 'hi\_IN,en\_IN'

then valuefirst-notification-resolved-templateid: "6789,12345"

_(Note: Both lists should not be empty - they must contain at least one element)_

#### **Configuration of push notification template messages** with a button <a href="#hardbreak-configuration-of-push-notification-template-messages-with-button" id="hardbreak-configuration-of-push-notification-template-messages-with-button"></a>

Template messages with buttons are maintained in the same way as described in the previous section (**Configuration of push notification template messages**)

There are two types of button message

* Quick Reply
* Call To Action

The Value First document below provides more details.&#x20;

{% file src="../../../../../.gitbook/assets/userguide-valuefirst-whatsapp-v1.0.4-190421-1-.pdf" %}
Value First Whatsapp User Guide
{% endfile %}

#### Integration of Bill Payment and Receipt Search feature in Xstate-Chatbot <a href="#integration-of-bill-payment-and-receipt-search-feature-in-xstate-chatbot" id="integration-of-bill-payment-and-receipt-search-feature-in-xstate-chatbot"></a>

The integration of the Bill payment and receipt search feature with the chatbot is enabled and disabled by making changes in this [file](https://github.com/egovernments/core-services/blob/develop/xstate-chatbot/nodejs/src/machine/service/service-loader.js). The payment and receipt search feature can be enabled and vice versa by exporting the respective bill service and receipt service file.

**Configuration of module for Bill payment and Receipt search**

To configure the list of modules to appear as an option for payment and receipt, Add the module business service code in the list present in the [environment](https://github.com/egovernments/DIGIT-DevOps/blob/master/deploy-as-code/helm/environments/qa.yaml#L216) file.

**For example:**\
If the applicable modules are defined in the variable - `bill-supported-modules: "WS, PT, TL" -`the defined modules will appear in the bill payment and receipt search. In the given example,  the modules Water and Sewerage, Property Tax, and Trade license will appear for bill payment and receipt search.

Add the message bundle, validation and service code for locality searcher in [egov-bill](https://github.com/egovernments/core-services/blob/develop/xstate-chatbot/nodejs/src/machine/service/egov-bill.js) and [egov-receipt](https://github.com/egovernments/core-services/blob/develop/xstate-chatbot/nodejs/src/machine/service/egov-receipts.js) file.

| Environmental Variables           | Description                                                                                                                                                            |
| --------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `WHATSAPP_BUSINESS_NUMBER`        | The mobile number to be used on server                                                                                                                                 |
| `VALUEFIRST_USERNAME`             | Username for configured number for sending messages to user through whatsapp provider API calls                                                                        |
| `VALUEFIRST_PASSWORD`             | Password for configured number for sending messages to user through whatsapp provider API calls                                                                        |
| `GOOGLE_MAPS_API_KEY`             | Maps API key to access geocoding feature                                                                                                                               |
| `ROOT_TENANTID`                   | Contains state level tenantid value                                                                                                                                    |
| `SUPPORTED_LOCALES`               | This variable contains the list supported language in chatbot. If there is a need to add new language in chatbot, then its respective locale need to add in this list. |
| `PGR_VERSION`                     | Contains PGR version value to use (i.e v1 or v2)                                                                                                                       |
| `PGR_UPDATE_TOPIC`                | Depends on PGR version respective PGR update kafka topic name should mention here. Example: If `PGR_VERSION: 'v2'` then `PGR_UPDATE_TOPIC: 'update-pgr-request'`       |
| `BILL_SEARCH_LIMIT`               | Limit for showing maximum number of bills on search.                                                                                                                   |
| `RECEIPT_SEARCH_LIMIT`            | Limit for showing maximum number of receipts on search.                                                                                                                |
| `COMPLAINT_SEARCH_LIMIT`          | Limit for showing maximum number of complaints on search.                                                                                                              |
| `BILL_SUPPORTED_MODULES`          | Contains the list of modules to be use for bill payment and receipts search.                                                                                           |
| `INFORMATION_IMAGE_FILESTORE_ID`  | Contains the filestoreid of informational image, which shows how to share the user current location.                                                                   |
| `OPEN_SEARCH_IMAGE_FILESTORE_ID`  | Contains the filestoreid of open search informational image, which shows how to use open search pay feature for bill payment                                           |
| `USER_SERVICE_HARDCODED_PASSWORD` | This variable contain fixed value of login password and otp. This value has to configured in _env_-secrets.yaml.                                                       |
| `GEO_SEARCH`                      | Boolean flag to enable and disable city / locality nlp search                                                                                                          |

**Configuration of Telemetry File**

Add this [telemetry file](https://github.com/egovernments/configs/pull/629/files) in [config repo](https://github.com/egovernments/configs/tree/DEV/egov-indexer) and mention the filename in the respective [environment yaml file](https://github.com/egovernments/DIGIT-DevOps/blob/master/deploy-as-code/helm/environments/qa.yaml#L263).

#### **Searcher config file:** <a href="#hardbreak-searcher-config-file" id="hardbreak-searcher-config-file"></a>

[<img src="https://github.com/fluidicon.png" alt="" data-size="line">configs/localitySearcher.yml at qa · egovernments/configs](https://github.com/egovernments/configs/blob/qa/egov-searcher/localitySearcher.yml)

**Cron job mdms entry:**

[<img src="https://github.com/fluidicon.png" alt="" data-size="line">RAIN-2768 Added entry in cron job api config file · egovernments/egov-mdms-data@30881ab](https://github.com/egovernments/egov-mdms-data/commit/30881ab4f759c8b607417be2047b46865ec953ef)

#### **Localisation for PGR service** <a href="#hardbreak-localisation-for-pgr-service-hardbreak" id="hardbreak-localisation-for-pgr-service-hardbreak"></a>

Information Images for PGR and Open Search

![Location Share Image](<../../../../../.gitbook/assets/image (280).png>)

![Open Search Image](<../../../../../.gitbook/assets/image (300) (1).png>)

## Reference Docs

### Doc Links <a href="#doc-links" id="doc-links"></a>

| Title                        | Link                                                                       |
| ---------------------------- | -------------------------------------------------------------------------- |
| Chatbot Message Localisation | [Chatbot Message Localisation Doc](xstate-chatbot-message-localisation.md) |
| nlp-search engine            | [NLP Engine Service](../nlp-engine-service.md)                             |

### API List

| Title                    | Link                                                                                                                       |
| ------------------------ | -------------------------------------------------------------------------------------------------------------------------- |
| /xstate-chatbot/message  | [https://www.getpostman.com/collections/57615217a846330672c6](https://www.getpostman.com/collections/57615217a846330672c6) |
| /xstate-chatbot/reminder | [https://www.getpostman.com/collections/47c10d1bc82a7133c269](https://www.getpostman.com/collections/47c10d1bc82a7133c269) |
| /xstate-chatbot/status   | [https://www.getpostman.com/collections/47c10d1bc82a7133c269](https://www.getpostman.com/collections/47c10d1bc82a7133c269) |

