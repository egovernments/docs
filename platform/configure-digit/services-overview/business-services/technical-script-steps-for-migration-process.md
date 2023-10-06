---
description: Technical documentation detailing migration steps
---

# Steps For Migration Process

## Overview

This specifies the migration steps which are specific to the payment index.

## Steps

**Step 1:** Adding a target index - Add index name dss-payment\_v2 as below:

In kibana, dev tools, apply the below command

|                                                                                                     |
| --------------------------------------------------------------------------------------------------- |
| <p>PUT dss-payment_v2</p><p>{} // add mapping file content here. mapping.json as attached below</p> |

{% hint style="info" %}
**Note:** This name should be as the value present in ingest es.index.namemapping.json24 May 2021, 11:15 AM
{% endhint %}

**Step 2:** Optional changes required in Ingest application properties

Ingest pipeline application properties contain **es.direct.push** supposed to be set **true** for testing.

<table><thead><tr><th width="119">S.No.</th><th>Property Name</th><th>Value</th><th>Description</th></tr></thead><tbody><tr><td>1.</td><td>es.direct.push</td><td>true</td><td>the transformed data will be pushed to ES index directly.</td></tr><tr><td>2.</td><td>es.direct.push</td><td>false</td><td>the transformed data will be lying at egov-dss-ingest-enriched topic</td></tr></tbody></table>

**Step 3:** Run migration Api, which migrates the data from the source index to the target index.

<table><thead><tr><th width="123.33333333333331">S.No.</th><th width="159">Name</th><th>Description</th></tr></thead><tbody><tr><td></td><td><p>Method</p><p>End Point</p><p>Body</p></td><td><p>POST</p><p>{host}/dashboard-ingest/ingest/migrate/paymentsindex-v1/v2</p><p>{"RequestInfo":{"authToken":"2ba70924-1bba-4a9b-b55d-2e9471bf3081"}}</p></td></tr><tr><td>2.</td><td>CURL</td><td>curl -X POST<br><a href="https://dev.digit.org/dashboard-ingest/ingest/migrate/paymentsindex-v1/v2">https://dev.digit.org/dashboard-ingest/ingest/migrate/paymentsindex-v1/v2</a><br>-H 'cache-control: no-cache'<br>-H 'content-type: application/json'<br>-H 'postman-token: d83fc136-116d-265f-3b83-ea41e3d5bb57'<br>-d '{"RequestInfo":{"authToken":"2ba70924-1bba-4a9b-b55d-2e9471bf3081"}}'</td></tr></tbody></table>

{% hint style="info" %}
**Note:** After migration, ensure dss-payment\_v2 data has been populated and is available.
{% endhint %}

In kibana, dev tools verify using below command

```
GET dss-payment_v2/_search
```

