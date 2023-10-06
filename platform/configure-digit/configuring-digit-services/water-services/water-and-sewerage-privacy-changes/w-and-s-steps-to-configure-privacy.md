---
description: Detailed steps to configure privacy in W&S module
---

# W\&S - Steps To Configure Privacy

## Overview

To make sure that after enabling privacy, the system works as expected, we will require some configurations to be made in the environment. This document contains all the steps to ensure successful implementation and working of the Water & Sewerage module.

## Steps

The following are the changes required to move the water and sewerage application to other environments:

1. Add a new role for REINDEXING so as to push encrypted data in the index in [roleactions.json](https://github.com/egovernments/egov-mdms-data/pull/2835/files#diff-9aabafcbd38f82bbabd00da339ed4448e6f75321d19da128cad45b436c77d20a) and [roles.json](https://github.com/egovernments/egov-mdms-data/pull/2835/files#diff-e9cb576f6be8078be7fd3494c51d0f6756f042421100ff6fc7a7db863b24cd2e) files.\
   Reference for these file changes can be taken from the following commit: [<img src="https://github.com/fluidicon.png" alt="" data-size="line">UM-4763 :: 2.8 UAT Promotion MDMS Changes by prashant-eGov · Pull Request #2835 · egovernments/egov-mdms-data](https://github.com/egovernments/egov-mdms-data/pull/2835/files) (Please pick the changes for the required files- roleactions.json and roles.json only)
2. Add a copy of the existing water-service index with a different topic name(`update-ws-encryption` and `update-sw-encryption`) for the encryption process.\
   _Reference:_ [<img src="https://github.com/fluidicon.png" alt="" data-size="line">Enc-WnS indexer and persister changes by hinamakhija-eGov · Pull Request #2510 · egovernments/configs](https://github.com/egovernments/configs/pull/2510/commits/bf025f1489933dce71fe448d1181515fa418f09c)
3. Some changes need to be made for existing indexes in the water-service and sewerage-service indexer files. The changes with respect to these files can be referred to from the following commit:\
   [<img src="https://github.com/fluidicon.png" alt="" data-size="line">\[UM-4382\]- Updated indexer for water service by hinamakhija-eGov · Pull Request #2342 · egovernments/configs](https://github.com/egovernments/configs/pull/2342)\
   [<img src="https://github.com/fluidicon.png" alt="" data-size="line">\[UM-4382\]-Updated indexer for sewerage by hinamakhija-eGov · Pull Request #2345 · egovernments/configs](https://github.com/egovernments/configs/pull/2345)
4. Restart the indexer.
5. Add the following json mappings in the existing mappings (parallel to water-services and sewerage-services key) for water-services and sewerage-services in kibana so that the PII data is not visible during search(The data do remain in the index and also search with respect to this happens as is).

```
"_source": {
        "excludes": [
            "Data.ownerMobileNumbers",
            "Data.connectionHolders.ownerType",
            "Data.connectionHolders.gender",
            "Data.connectionHolders.mobileNumber",
            "Data.connectionHolders.correspondenceAddress",
            "Data.connectionHolders.fatherOrHusbandName",
            "Data.connectionHolders.relationship",
            "Data.plumberInfo.mobileNumber"
        ]
      }
```

Sample index at the bottom

1. Add _2 new persister files_ responsible for managing old data encryption. [ws-enc-audit-persister.yml](https://github.com/egovernments/configs/blob/UAT/egov-persister/ws-enc-audit-persister.yml) and [sw-enc-audit-persister.yml](https://github.com/egovernments/configs/blob/UAT/egov-persister/sw-enc-audit-persister.yml).
2. Update the path of these files in the DevOps repo in the specific environment file.
3. Restart the persister
4. Deploy new ws-service and sw-service builds.
5. Port-forward the ws-service and sw-service pods and hit the curl to start encryption.\
   The curls can be referred from here:

**Water-encryption curl:**

```
curl --location --request POST 'http://localhost:8040/ws-services/wc/_encryptOldData?tenantIds=pb,pb.jalandhar&limit=200' \
--header 'authority: dev.digit.org' \
--header 'accept: application/json, text/plain, */*' \
--header 'accept-language: en-GB,en-US;q=0.9,en;q=0.8' \
--header 'content-type: application/json;charset=UTF-8' \
--header 'origin: https://dev.digit.org' \
--header 'referer: https://dev.digit.org/digit-ui/employee/pt/search' \
--header 'sec-ch-ua: ".Not/A)Brand";v="99", "Google Chrome";v="103", "Chromium";v="103"' \
--header 'sec-ch-ua-mobile: ?0' \
--header 'sec-ch-ua-platform: "Linux"' \
--header 'sec-fetch-dest: empty' \
--header 'sec-fetch-mode: cors' \
--header 'sec-fetch-site: same-origin' \
--header 'user-agent: Mozilla/5.0 (X11; Linux x86_64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/103.0.0.0 Safari/537.36' \
--data-raw '{
    "RequestInfo": {
        "apiId": "Rainmaker",
        "authToken": "{{auth}}",
        "userInfo": {
            "id": 24226,
            "uuid": "11b0e02b-0145-4de2-bc42-c97b96264807",
            "userName": "amr001",
            "name": "leela",
            "mobileNumber": "9814424443",
            "emailId": "leela@llgmail.com",
            "locale": null,
            "type": "EMPLOYEE",
            "roles": [
                 {
                    "name": "WS Document Verifier",
                    "code": "WS_DOC_VERIFIER",
                    "tenantId": "pb.amritsar"
                }
            ],
            "active": true,
            "tenantId": "pb.amritsar",
            "permanentCity": "Amritsar"
        },
        "plainAccessRequest": {
        },
        "msgId": "1657027355542|en_IN"
    }
}'
```

**Sewerage-encryption curl:**

```
curl --location --request POST 'http://localhost:4040/sw-services/swc/_encryptOldData?tenantIds=pb.amritsar&limit=150' \
--header 'authority: dev.digit.org' \
--header 'accept: application/json, text/plain, */*' \
--header 'accept-language: en-GB,en-US;q=0.9,en;q=0.8' \
--header 'content-type: application/json;charset=UTF-8' \
--header 'origin: https://dev.digit.org' \
--header 'referer: https://dev.digit.org/digit-ui/employee/pt/search' \
--header 'sec-ch-ua: ".Not/A)Brand";v="99", "Google Chrome";v="103", "Chromium";v="103"' \
--header 'sec-ch-ua-mobile: ?0' \
--header 'sec-ch-ua-platform: "Linux"' \
--header 'sec-fetch-dest: empty' \
--header 'sec-fetch-mode: cors' \
--header 'sec-fetch-site: same-origin' \
--header 'user-agent: Mozilla/5.0 (X11; Linux x86_64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/103.0.0.0 Safari/537.36' \
--data-raw '{
    "RequestInfo": {
        "apiId": "Rainmaker",
        "authToken": "null",
        "userInfo": {
            "id": 24226,
            "uuid": "11b0e02b-0145-4de2-bc42-c97b96264807",
            "userName": "amr001",
            "name": "leela",
            "mobileNumber": "9814424443",
            "emailId": "leela@llgmail.com",
            "locale": null,
            "type": "EMPLOYEE",
            "roles": [
                {
                    "name": "SW Approver",
                    "code": "SW_APPROVER",
                    "tenantId": "pb.amritsar"
                }
            ],
            "active": true,
            "tenantId": "pb.amritsar",
            "permanentCity": "Amritsar"
        },
        "plainAccessRequest": {
        },
        "msgId": "1657027355542|en_IN"
    }
}'
```

In the params list in both the above curls, “tenantIds” param can either be provided with a single tenantId or a list of tenantIds for encrypting the data with respect to the provided tenantIds. However, to encrypt the data for all tenantIds in the system, tenantIds param itself should be removed.

To validate if the encryption is completed, you can check with the following dB queries:

* `select * from eg_ws_enc_audit order by createdtime desc;`
* `select count(*) from eg_ws_id_enc_audit;`

This query can validate whether all records are there or not. The count should match the total count of records in the eg\_ws\_connection table.

* `select * from eg_ws_id_enc_audit;`

This can help you check what all properties have been updated so far. This table contains the id, applicationnumber, connectionnumber and tenantid.

**Sample Index for point 5:**

```
PUT water-services
{
  
}
```

\
