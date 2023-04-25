# National Dashboard Adaptor Service

## Overview <a href="#overview" id="overview"></a>

Provides a detailed walk-through of how to set up, configure and deploy Airflow DAGs on the state side to extract data from the Elastic Search server to push to the National Dashboard Adaptor.

## **Scope**

Design and develop an adaptor service which will extract data from the state DIGIT installations and push it onto the National Dashboard instance periodically.&#x20;

A list of tasks for this has been tracked for the Adaptor&#x20;

[Jira - Dashboard](https://digit-discuss.atlassian.net/jira/software/projects/NDA/boards/120)

* Adaptor to be deployed on state DIGIT installations&#x20;
* Periodically, the adaptor extracts data and aggregates it from the different DIGIT modules
* Posts the data to the National Dashboard for the state
* Bookkeeping is done for every adaptor data extract and pushes for audit and debugging&#x20;
* Out of scope: Extraction from non-DIGIT sources&#x20;

&#x20;A national dashboard adaptor extracts data from the state DSS at a scheduled time which can be configured and then would ingest in the National Dashboard. The adaptor ingests data at the state/ULB/Ward level for each module on a daily basis. The adapter sends the data in a batch size of 50 to the national dashboard.

<figure><img src="../../../../../.gitbook/assets/image (407).png" alt=""><figcaption></figcaption></figure>
