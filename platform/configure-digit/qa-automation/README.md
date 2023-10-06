---
description: DIGIT Test Automation Framework details
---

# QA Automation

## Overview

DIGIT Test Automation framework majorly deals with various API services validation. It enables to test and validate back end services across all active environments and as well as tenants.

## Scope

* Framework is robust enough to function with minimal changes
* Framework handles multi tenant with only properties update
* Framework can switch environment with no manual update in automation code
* Framework handles Kafka related services
* Framework supports browser integration for making citizen payment via payment gateway

## List of Services Completed

* **Core Services**
  * egov-accesscontrol, egov-enc-service, egov-filestore, egov-idgen, egov-indexer, egov-localization, egov-location, egov-mdms-service, egov-notification-mail, egov-notification-sms, egov-otp, egov-persister, egov-pg-service, egov-searcher, egov-url-shortening, egov-user, egov-workflow-v2, pdf-service, report, telemetry, user-otp, zuul
* **Business Services**
  * billing-service, collection-services, dashboard-analytics, dashboard-ingest, egf-instrument, egf-master, egov-apportion-service, egov-hrms
* **Municipal Services**
  * bpa-calculator, bpa-services, firenoc-calculator, firenoc-services, land-services, property-services, pt-calculator-v2, rainmaker-pgr, sw-calculator, sw-services, tl-calculator, tl-services, ws-calculator, ws-services
* **E2E - Integration of services**

E2E pt services, E2E ws services, E2E pgr services, E2E tl services, mCollect

## Approach

Automation is accomplished by building a custom framework using Karate Framework. Karate Framework is a BDD framework which is written on top of cucumber. Unlike cucumber which requires us to write step definitions for each and every scenarios, Karate supports writing scenarios directly in the feature files.

* Automation framework fetches data for respective modules wherever predefined values are required while creating a payload
* And uses generic functions to generate random mobile number, name, etc to pass values for respective fields in payload
* Framework allows to test kafka related services by using third party tool as a proxy to access kafka clusters via REST API called kafka Rest Proxy

|                  |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                              |
| ---------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **Title**        | **Description**                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                              |
| Karate Framework | [<img src="https://github.com/fluidicon.png" alt="" data-size="line">intuit/karate](https://github.com/intuit/karate)                                                                                                                                                                                                                                                                                                                                                                                                        |
| Gherkin Language | <ul><li>Gherkin is the format for cucumber specifications</li><li>Gherkin is line-oriented language just like YAML and Python</li><li>Gherkin Scripts connects the human concept of cause and effect to the software concept of input/process and output</li><li>Feature, Background, Scenario, Given, When, Then, And But are importantly used in Gherkin</li><li>In Gherkin, each scenario should execute separately</li><li>The biggest advantage of Gherkin is simple enough for non-programmers to understand</li></ul> |
| Cucumber         | [<img src="https://cucumber.io/cucumber/assets/img/favicon.png" alt="" data-size="line">BDD Testing & Collaboration Tools for Teams \| Cucumber](https://cucumber.io/)                                                                                                                                                                                                                                                                                                                                                       |
| MDMS             | [<img src="https://github.com/fluidicon.png" alt="" data-size="line">egovernments/egov-mdms-data](https://github.com/egovernments/egov-mdms-data)                                                                                                                                                                                                                                                                                                                                                                            |
| Kafka Rest Proxy | [<img src="https://github.com/fluidicon.png" alt="" data-size="line">confluentinc/kafka-rest](https://github.com/confluentinc/kafka-rest)                                                                                                                                                                                                                                                                                                                                                                                    |

### Tools Used

* [Java](https://www.java.com/en/)
* [JavaScript](https://developer.mozilla.org/en-US/docs/Web/JavaScript)
* [Karate](https://github.com/intuit/karate)
* [Cucumber](https://cucumber.io/docs/cucumber/api/)
* [JUnit](https://junit.org/junit4/)
* [Kafka Rest Proxy](https://github.com/confluentinc/kafka-rest)
* [Maven](https://maven.apache.org)

### Environments currently working on

* [https://qa.digit.org/](https://qa.digit.org/)
* [https://uat.digit.org/](https://uat.digit.org/)

### Observations

* Currently, there are failures in the automation scripts due to existing bugs
* Since there are some limitations with Kafka Rest Proxy, Kafka related test cases will not run. Awaiting the required fixes in its upcoming release

## Reference Docs

#### Doc Links <a href="#doc-links" id="doc-links"></a>

|                                                       |                                                                                                                                                                                                                                                    |
| ----------------------------------------------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **Title**                                             | **Link**                                                                                                                                                                                                                                           |
| Manual Test Cases                                     | [<img src="https://ssl.gstatic.com/docs/spreadsheets/favicon3.ico" alt="" data-size="line">Egov Automation: Test Cases](https://docs.google.com/spreadsheets/d/16BdbxgE4z38atk6MZBCRcw4\_D4fL0AHEvblqGPSYJ\_s/edit?usp=sharing)                    |
| Automation Source Code                                | [<img src="https://github.com/fluidicon.png" alt="" data-size="line">egovernments/test-automation](https://github.com/egovernments/test-automation)                                                                                                |
| Automation Readme                                     | [<img src="https://github.githubassets.com/favicon.ico" alt="" data-size="line">https://github.com/egovernments/test-automation/blob/master/README.md - Connect to preview](https://github.com/egovernments/test-automation/blob/master/README.md) |
| Kafka Approach Document                               | [Kafka Consumer Producer Approach](https://digit-discuss.atlassian.net/wiki/spaces/DD/pages/1540587710/Kafka+Consumer+Producer+Approach)                                                                                                           |
| Sample Config File (for passing to execution command) | [<img src="https://ssl.gstatic.com/images/branding/product/1x/drive_2020q4_32dp.png" alt="" data-size="line">config.yaml](https://drive.google.com/file/d/19XDqJErhGrNegrmI2AxL9dsDqubxaWdo/view?usp=sharing)                                      |

> [![Creative Commons License](https://i.creativecommons.org/l/by/4.0/80x15.png)\_\_](http://creativecommons.org/licenses/by/4.0/)_All content on this page by_ [_eGov Foundation_ ](https://egov.org.in/)_is licensed under a_ [_Creative Commons Attribution 4.0 International License_](http://creativecommons.org/licenses/by/4.0/)_._
