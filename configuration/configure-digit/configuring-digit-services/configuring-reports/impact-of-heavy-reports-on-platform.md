# Impact Of Heavy Reports On Platform

### Overview <a href="#overview" id="overview"></a>

Rainmaker has report framework to configure new reports. As part of the report configuration, we have to write a native SQL query to get the required data for the report. So if the query takes huge time to execute or query result has huge data, then it will impact on the whole application performance.

### Root Cause <a href="#root-cause" id="root-cause"></a>

The following cases where we can see the application performance issue because of heavy reports.

* Filtering with long date range data or applying fewer filters which in turns return huge data
* Join the multiple tables for getting required data and missing creating index on join columns
* Implementing conditional logic inside the queries itself
* Writing multiple sub-queries inside a single query for getting required data

### Impact <a href="#impact" id="impact"></a>

Because of heavy reports, the following things will impact the platform

* When we execute a complex query on the database, thread from connection pool will block to execute the query
* When threads from connection pool are blocked completely, the application will become very slow for incoming requests
* When max request timeout is crossed, API gateway will return timeout error, But still, connection thread on the database is active, Then all these types of idle threads will occupy database resources like memory, CPU which in turns increase the load on the database
* Some times when running huge queries, because of time taken by the query will lead to broken pipe issue which causes more memory leaks and out of heap memory type issues. Because of this, the service will frequently restart automatically.
* If a query returns huge data, the browser will become unresponsive and application will become unresponsive.

[![Creative Commons License](https://i.creativecommons.org/l/by/4.0/80x15.png)​](http://creativecommons.org/licenses/by/4.0/)All content on this page by [eGov Foundation](https://egov.org.in/) is licensed under a [Creative Commons Attribution 4.0 International License](http://creativecommons.org/licenses/by/4.0/).
