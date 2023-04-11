---
description: New release features, enhancements, and fixes
---

# Release Notes

## Release Summary <a href="#release-summary" id="release-summary"></a>

DIGIT 2.8 release includes 1 new module, several new products, functional and security features, regression testing, bug fixes of previously released modules and a few non-functional changes.

**New Module**

Citizen engagement - Survey service

**Functional Changes**&#x20;

* OBPS Tabular Reports in old UI/UX, Trade Licence Tabular Reports in old UI/UX
* Notification based on channels - PGR, OBPS & mCollect
* Help/FAQ section in Citizen UI - common framework - integration with all the modules
* Bill Genie UI/UX revamp
* Survey module
* Water & Sewerage UI/UX Revamp, Bill amendment workflow update & UI/UX revamp, W\&S disconnection
* Water & Sewerage Privacy Exemplar, Standard Reports for W\&S - Receipt Register, Collection Register, Defaulters Report - in old UI/UX
* Birth & Death Tabular Reports - in old UI/UX
* Enhancement on DSS, Finance Module State DSS, NSS Adaptor, Enhancements in National Dashboard- FAQ & About page.

**Non-functional Changes**&#x20;

* Navigation re-direction from New UI to OLD UI
* Bulk Bill PDF generation and performance testing
* W\&S Bulk Bill generation and performance testing

## New ‌Feature Additions <a href="#new-feature-additions" id="new-feature-additions"></a>

| Feature                                                                                       | Description                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                      |
| --------------------------------------------------------------------------------------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Water & Sewerage UI/UX Revamp                                                                 | <ul><li>Employee W&#x26;S UI/UX revamp</li><li>Citizen UI/UX revamp</li></ul>                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                    |
| Water & Sewerage disconnection                                                                | <p>Added W&#x26;S disconnection feature:</p><ul><li>Apply for disconnection (Permanent/Temporary)</li><li>Proceed with the workflow and Execute disconnection.</li><li>Events and Notifications for each step</li></ul><p>Added new screens for disconnection workflow.</p>                                                                                                                                                                                                                                                                                                                                                      |
| <p>Privacy Exemplar -</p><p>(The feature is disabled in the <a href="./">2.8 release</a>)</p> | Added Data Privacy for water & sewerage for masking/unmasking PII data.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                          |
| W\&S Bill Amendment Workflow update                                                           | Code change in billing service, workflow change and data update in workflow transition table.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                    |
| New KPIs for National Dashboard                                                               | <ul><li>Added 3 New KPIs - 2 on the <a href="../configure-digit/configuring-digit-services/national-dashboard-service-configuration/national-dashboard-overview.md">National Dashboard Overview</a> screen (Total Non-Tax Collection, Total Non-Tax Revenue Contribution), 1 in <a href="../configure-digit/configuring-digit-services/national-dashboard-service-configuration/property-tax-national-dashboard.md">Property Tax</a> (Average Property Tax Collected)</li><li>Added handover <a href="../configure-digit/configuring-digit-services/national-dashboard-service-configuration/new-kpis.md">document</a></li></ul> |
| Bill amendment UI/UX revamp                                                                   |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                  |

## Enhancements <a href="#enhancements" id="enhancements"></a>

| Updated Feature                                                                                                                                                                                   | Description                                                                                                                                                                                                                                                                                                                                              |
| ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| <p></p><p><br></p><p>Enhancements in National Dashboard- FAQ &#x26; About</p><p><br><br></p>                                                                                                      | Updated - About, Purpose page for National Dashboard                                                                                                                                                                                                                                                                                                     |
| B\&D Tabular Reports - in old UI/UX                                                                                                                                                               | <ul><li>Added - Birth Count Report, Death Count Report, Birth Count Report by District, Death Count Report by District, Birth and Death Certificate Payment Report.</li><li>Added <a href="../configure-digit/configuring-digit-services/birth-and-death-service-configuration/birth-and-death-reports.md">Reports Technical Documentation</a></li></ul> |
| Bill amendment UI/UX revamp                                                                                                                                                                       | <ul><li>Search Amendment </li><li>Create a new Amendment for W&#x26;S </li><li>Inbox screen for bill-amendment</li></ul>                                                                                                                                                                                                                                 |
| Notification based on channels - PGR, OBP and mCollect                                                                                                                                            | Enhanced PGR, OBPS and mCollect notifications to incorporate different notifications based on Channels.                                                                                                                                                                                                                                                  |
| Bulk Bill PDF Generation and Performance Testing                                                                                                                                                  | Updated \_jobscheduler API for enhancing performance for bulk records.                                                                                                                                                                                                                                                                                   |
| TL Tabular Reports in old UI/UX                                                                                                                                                                   | Enhanced TL Report: TLDailyCollectionReport, TLApplicationStatusReport, _TradeLicenseRegistryReport_                                                                                                                                                                                                                                                     |
| Navigation re-direction from new UI to old UI                                                                                                                                                     | Login screen navigation to new UI irrespective of and login screen(old/new)                                                                                                                                                                                                                                                                              |
| [Standard Reports](../configure-digit/configuring-digit-services/water-services/water-and-sewerage-reports.md) for W\&S - Receipt Register, Collection Register, Defaulters Report - in old UI/UX | Added W\&S reports: Receipt Register, Collection Register, Defaulters Report.                                                                                                                                                                                                                                                                            |
| Bill Genie UI/UX revamp                                                                                                                                                                           | <p>Added:</p><ul><li>Search bills</li><li>Group bills</li><li>Download bills</li></ul>                                                                                                                                                                                                                                                                   |
| National Dashboard Adaptor Integration Testing                                                                                                                                                    | Airflow setup for all modules integrated all modules with an adapter.                                                                                                                                                                                                                                                                                    |
| OBPS Tabular reports in old UI/UX                                                                                                                                                                 | Enhanced OBPS Report: OBPS Daily Collection Report                                                                                                                                                                                                                                                                                                       |
| Survey                                                                                                                                                                                            | Create surveys, update surveys, view survey results, fill in survey forms.                                                                                                                                                                                                                                                                               |

### Success Metrics

[https://docs.google.com/document/d/1b4plZ0TFMJC53MDt72\_sx-Wif2bdR4I5dnD9DTN40Ss/edit](https://docs.google.com/document/d/1b4plZ0TFMJC53MDt72\_sx-Wif2bdR4I5dnD9DTN40Ss/edit)

### Adoption Metrics

Adoption of new features will be tracked on the basis of the following metrics:

| **Metric**                      | **Description**                                                                         | **Estimate**                      |
| ------------------------------- | --------------------------------------------------------------------------------------- | --------------------------------- |
| Time to Value                   | Time taken from Gate 2 to all features of DIGIT 2.8 to be released as part of UPYOG 2.0 | 1.5 months                        |
| No. of states using the feature | No. of states implementing the feature/module within next 6 months                      | Refer Account Wise Feature Demand |
| No. of ULBs using the feature   | No. of ULBs implementing the feature/module within next 6 months                        | Refer Account Wise Feature Demand |
| Frequency of Use(Survey)        | No. of Surveys completed in next 6 months                                               | Target: 3                         |

## ‌Document Resources and Links <a href="#document-resources-and-links" id="document-resources-and-links"></a>

### UI Technical Documents

1. [Employee: Water and Sewerage Application Details](../configure-digit/configuring-digit-services/water-services/water-and-sewerage-service-ui-docs/employee-application-details.md)
2. [Employee: Water and Sewerage Connection Details](../configure-digit/configuring-digit-services/water-services/water-and-sewerage-service-ui-docs/employee-connection-details.md)
3. [Employee: Water & Sewerage Modify Create Flow](../configure-digit/configuring-digit-services/water-services/water-and-sewerage-service-ui-docs/employee-modify-create-flow.md)
4. [Employee: Water and Sewerage Modify Application Details](../configure-digit/configuring-digit-services/water-services/water-and-sewerage-service-ui-docs/employee-modify-application-details.md)
5. [Employee: Disconnection Water & Sewerage Create Flow](../configure-digit/configuring-digit-services/water-services/water-and-sewerage-service-ui-docs/employee-disconnection-create-flow.md)
6. [Employee: Water and Sewerage Disconnection Application Details](../configure-digit/configuring-digit-services/water-services/water-and-sewerage-service-ui-docs/employee-disconnection-application-details.md)
7. [Employee: Ad-hoc Rebate/Penalty and View Breakup in application details.](../configure-digit/configuring-digit-services/water-services/water-and-sewerage-service-ui-docs/employee-ad-hoc-rebate-penalty-and-view-breakup.md)
8. [Citizen: Water & Sewerage Create](../configure-digit/configuring-digit-services/water-services/water-and-sewerage-service-ui-docs/citizen-create-application.md)
9. [Citizen: Water & Sewerage - My Applications](../configure-digit/configuring-digit-services/water-services/water-and-sewerage-service-ui-docs/citizen-my-applications.md)
10. [Citizen: Water & Sewerage - My Connections](../configure-digit/configuring-digit-services/water-services/water-and-sewerage-service-ui-docs/citizen-my-connections.md)
11. [Citizen: Water and Sewerage Disconnection Application Create](../configure-digit/configuring-digit-services/water-services/water-and-sewerage-service-ui-docs/citizen-disconnection-application-create.md)
12. [Citizen: Water and Sewerage Disconnection Application Details](../configure-digit/configuring-digit-services/water-services/water-and-sewerage-service-ui-docs/citizen-disconnection-application-create.md)
13. [Privacy - UI](../configure-digit/configuring-digit-services/water-services/water-and-sewerage-service-ui-docs/privacy-ui.md)
14. [Employee: Bill Amendment - Create Flow](../configure-digit/configuring-digit-services/bill-amendment-service-configuration/ui-configuration/employee-bill-amendment-create-flow.md)
15. [Employee: Bill Amendment - Search, Edit & Resubmit, Approve, Reject & Send-Back Flows](../configure-digit/configuring-digit-services/bill-amendment-service-configuration/ui-configuration/employee-bill-amendment-create-flow.md)
16. [UI- Tech Documentation on Bill Genie and Group bill screens](../configure-digit/configuring-digit-services/bill-genie-service-configuration/ui-configuration/group-bills-screen.md)
17. [Bill Genie:: Employee: Search Bills](../configure-digit/configuring-digit-services/bill-genie-service-configuration/ui-configuration/employee-search-bills.md)
18. [Bill Genie:: Employee: Group Bills](../configure-digit/configuring-digit-services/bill-genie-service-configuration/ui-configuration/employee-group-bills.md)
19. [Bill Genie:: Employee: Download Bill](../configure-digit/configuring-digit-services/bill-genie-service-configuration/ui-configuration/employee-download-bill.md)
20. [Help/FAQ section Citizen UI](../configure-digit/configuring-digit-services/survey-service-configuration/help-faq-section-citizen-ui.md)
21. [National Dashboard - About & FAQs](../configure-digit/configuring-digit-services/national-dashboard-service-configuration/national-dashboard-ui-technical-doc/national-dashboard-about-and-faqs.md)
22. [Navigation between Old and New UI](../configure-digit/configuring-digit-services/common-ui-docs/navigation-between-old-and-new-ui.md)

Updated docs

1. [Trade License - Apply Flow](../configure-digit/configuring-digit-services/tl-service-configuration/tl-ui-configuration/tl-apply-flow-ui-details.md)
2. [New Trade License Application](../configure-digit/configuring-digit-services/tl-service-configuration/tl-ui-configuration/new-trade-license-ui-flow.md)

### Backend Service Documents

1. [Birth and Death Service](../configure-digit/configuring-digit-services/birth-and-death-service-configuration/birth-and-death-service-setup.md)
2. [State DSS - Birth and Death Technical Documentation](../configure-digit/configuring-digit-services/birth-and-death-service-configuration/state-dss-birth-and-death.md)
3. [Water & Sewerage-State DSS- Technical Documentation](../configure-digit/configuring-digit-services/water-services/state-dss-water-and-sewerage.md)
4. [National Dashboard-W\&S Technical Documentation](../configure-digit/configuring-digit-services/national-dashboard-service-configuration/)
5. [Water and Sewerage Service Technical Documents](../configure-digit/configuring-digit-services/water-services/)
6. [Guidelines for supporting User Privacy in a module](https://core.digit.org/platform/core-services/encryption-service/guidelines-for-supporting-user-privacy-in-a-module)
7. [Encryption Client Library](https://core.digit.org/platform/core-services/encryption-service/encryption-client-library)
8. [Water Service - Disconnection](../configure-digit/configuring-digit-services/water-services/water-service-disconnection.md)
9. [Sewerage Service - Disconnection](../configure-digit/configuring-digit-services/water-services/sewerage-service/sewerage-service-disconnection.md)
10. [Sewerage Disconnection Calculator Service](../configure-digit/configuring-digit-services/water-services/sewerage-service/sewerage-disconnection-calculator-service.md)
11. [Water Disconnection Calculator Service](../configure-digit/configuring-digit-services/water-services/water-disconnection-calculator-service.md)
12. [W\&S: Privacy Changes Backend Technical Documentation](../configure-digit/configuring-digit-services/water-services/water-and-sewerage-privacy-changes/)
13. [National Dashboard Adaptor Service](../configure-digit/configuring-digit-services/national-dashboard-service-configuration/national-dashboard-ingest-service/national-dashboard-adaptor-service.md)
14. [Workflow config-Replacement data-Migration Document for Bill Amendment W\&S](../configure-digit/configuring-digit-services/water-services/workflow-config-replacement-data.md)
15. [Survey Service](../configure-digit/configuring-digit-services/survey-service-configuration/)

&#x20;

