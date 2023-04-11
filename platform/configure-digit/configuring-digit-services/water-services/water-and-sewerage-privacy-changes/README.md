---
description: Backend technical documentation
---

# Water & Sewerage Privacy Changes

## Overview <a href="#overview" id="overview"></a>

This document highlights the changes that need to be done in a Water and Sewerage module to support the privacy feature.

## Pre-requisites <a href="#pre-requisites" id="pre-requisites"></a>

* Prior knowledge of Java/J2EE
* Prior knowledge of Spring Boot
* MDMS service
* Encryption service

## MDMS Changes <a href="#mdms-changes" id="mdms-changes"></a>

#### Update the SecurityPolicy.json file <a href="#update-the-securitypolicy.json-file." id="update-the-securitypolicy.json-file."></a>

The Security Policy MDMS file must have the model configuration for fields to be encrypted/decrypted.\
The following models have been used for W\&S in the SecurityPolicy.json file:

```
{
      "model": "WnSConnection",
      "uniqueIdentifier": {
        "name": "uuid",
        "jsonPath": "/connectionHolders/0/uuid"
      },
      "attributes": [
        {
          "name": "ownerType",
          "jsonPath": "connectionHolders/*/ownerType",
          "patternId": "005",
          "defaultVisibility": "PLAIN"
        },
        {
          "name": "relationship",
          "jsonPath": "connectionHolders/*/relationship",
          "patternId": "005",
          "defaultVisibility": "PLAIN"
        }
      ],
      "roleBasedDecryptionPolicy": [
        {
          "roles": ["WS_CEMP","WS_DOC_VERIFIER","WS_FIELD_INSPECTOR","WS_APPROVER","WS_CLERK","SW_CEMP","SW_DOC_VERIFIER","SW_FIELD_INSPECTOR","SW_APPROVER","SW_CLERK"],
          "attributeAccessList": [          
            {
              "attribute": "ownerType",
              "firstLevelVisibility": "MASKED",
              "secondLevelVisibility": "PLAIN"
            },
            {
              "attribute": "relationship",
              "firstLevelVisibility": "MASKED",
              "secondLevelVisibility": "PLAIN"
            }
          ]
        },
        {
          "roles": ["REINDEXING_ROLE"],
          "attributeAccessList": [
            {
              "attribute": "ownerType",
              "firstLevelVisibility": "ENCRYPTED",
              "secondLevelVisibility": "PLAIN"
            },
            {
              "attribute": "relationship",
              "firstLevelVisibility": "ENCRYPTED",
              "secondLevelVisibility": "PLAIN"
            }
          ]
        }
      ]
    },
    {
      "model": "WnSConnectionOwner",
      "uniqueIdentifier": {
        "name": "uuid",
        "jsonPath": "/uuid"
      },
      "attributes": [
      
        {
          "name": "connectionHoldersMobileNumber",
          "jsonPath": "mobileNumber",
          "patternId": "001",
          "defaultVisibility": "PLAIN"
        },
        {
          "name": "fatherOrHusbandName",
          "jsonPath": "fatherOrHusbandName",
          "patternId": "002",
          "defaultVisibility": "PLAIN"
        },
        {
          "name": "gender",
          "jsonPath": "gender",
          "patternId": "005",
          "defaultVisibility": "PLAIN"
        },
        {
          "name": "correspondenceAddress",
          "jsonPath": "correspondenceAddress",
          "patternId": "005",
          "defaultVisibility": "PLAIN"
        },
        {
          "name": "ownerType",
          "jsonPath": "connectionHolders/*/ownerType",
          "patternId": "005",
          "defaultVisibility": "PLAIN"
        },
        {
          "name": "plumberInfoMobileNumber",
          "jsonPath": "plumberInfo/*/mobileNumber",
          "patternId": "001",
          "defaultVisibility": "PLAIN"
        },
        {
          "name": "assigneeMobileNumber",
          "jsonPath": "assignes/*/mobileNumber",
          "patternId": "001",
          "defaultVisibility": "PLAIN"
        },
        {
          "name": "relationship",
          "jsonPath": "connectionHolders/*/relationship",
          "patternId": "005",
          "defaultVisibility": "PLAIN"
        }
      ],
      "roleBasedDecryptionPolicy": [
        {
          "roles": ["WS_CEMP","WS_DOC_VERIFIER","WS_FIELD_INSPECTOR","WS_APPROVER","WS_CLERK","SW_CEMP","SW_DOC_VERIFIER","SW_FIELD_INSPECTOR","SW_APPROVER","SW_CLERK"],
          "attributeAccessList": [
            {
              "attribute": "connectionHoldersMobileNumber",
              "firstLevelVisibility": "MASKED",
              "secondLevelVisibility": "PLAIN"
            },
            {
              "attribute": "gender",
              "firstLevelVisibility": "MASKED",
              "secondLevelVisibility": "PLAIN"
            },
            {
              "attribute": "fatherOrHusbandName",
              "firstLevelVisibility": "MASKED",
              "secondLevelVisibility": "PLAIN"
            },
            {
              "attribute": "ownerType",
              "firstLevelVisibility": "MASKED",
              "secondLevelVisibility": "PLAIN"
            },
            {
              "attribute": "correspondenceAddress",
              "firstLevelVisibility": "MASKED",
              "secondLevelVisibility": "PLAIN"
            },
            {
              "attribute": "relationship",
              "firstLevelVisibility": "MASKED",
              "secondLevelVisibility": "PLAIN"
            },
            {
              "attribute": "plumberInfoMobileNumber",
              "firstLevelVisibility": "MASKED",
              "secondLevelVisibility": "PLAIN"
            },
            {
              "attribute": "assigneeMobileNumber",
              "firstLevelVisibility": "MASKED",
              "secondLevelVisibility": "PLAIN"
            }
          ]
        },
        {
          "roles": ["REINDEXING_ROLE"],
          "attributeAccessList": [
            {
              "attribute": "connectionHoldersMobileNumber",
              "firstLevelVisibility": "ENCRYPTED",
              "secondLevelVisibility": "PLAIN"
            },
            {
              "attribute": "gender",
              "firstLevelVisibility": "ENCRYPTED",
              "secondLevelVisibility": "PLAIN"
            },
            {
              "attribute": "fatherOrHusbandName",
              "firstLevelVisibility": "ENCRYPTED",
              "secondLevelVisibility": "PLAIN"
            },
            {
              "attribute": "ownerType",
              "firstLevelVisibility": "ENCRYPTED",
              "secondLevelVisibility": "PLAIN"
            },
            {
              "attribute": "correspondenceAddress",
              "firstLevelVisibility": "ENCRYPTED",
              "secondLevelVisibility": "PLAIN"
            },
            {
              "attribute": "relationship",
              "firstLevelVisibility": "ENCRYPTED",
              "secondLevelVisibility": "PLAIN"
            },
            {
              "attribute": "plumberInfoMobileNumber",
              "firstLevelVisibility": "ENCRYPTED",
              "secondLevelVisibility": "PLAIN"
            },
            {
              "attribute": "assigneeMobileNumber",
              "firstLevelVisibility": "ENCRYPTED",
              "secondLevelVisibility": "PLAIN"
            }
          ]
        }
      ]
    },
    {
      "model": "WnSConnectionDecrypDisabled",
      "uniqueIdentifier": {
        "name": "uuid",
        "jsonPath": "/connectionHolders/0/uuid"
      },
      "attributes": [
        {
          "name": "ownerType",
          "jsonPath": "connectionHolders/*/ownerType",
          "patternId": null,
          "defaultVisibility": "PLAIN"
        },
        {
          "name": "relationship",
          "jsonPath": "connectionHolders/*/relationship",
          "patternId": null,
          "defaultVisibility": "PLAIN"
        }
      ],
      "roleBasedDecryptionPolicy": []
    },
    {
      "model": "WnSConnectionOwnerDecrypDisabled",
      "uniqueIdentifier": {
        "name": "uuid",
        "jsonPath": "/uuid"
      },
      "attributes": [
        {
          "name": "connectionHoldersMobileNumber",
          "jsonPath": "mobileNumber",
          "patternId": null,
          "defaultVisibility": "PLAIN"
        },
        {
          "name": "fatherOrHusbandName",
          "jsonPath": "fatherOrHusbandName",
          "patternId": null,
          "defaultVisibility": "PLAIN"
        },
        {
          "name": "gender",
          "jsonPath": "gender",
          "patternId": null,
          "defaultVisibility": "PLAIN"
        },
        {
          "name": "correspondenceAddress",
          "jsonPath": "correspondenceAddress",
          "patternId": null,
          "defaultVisibility": "PLAIN"
        },
        {
          "name": "ownerType",
          "jsonPath": "connectionHolders/*/ownerType",
          "patternId": null,
          "defaultVisibility": "PLAIN"
        },
        {
          "name": "plumberInfoMobileNumber",
          "jsonPath": "plumberInfo/*/mobileNumber",
          "patternId": null,
          "defaultVisibility": "PLAIN"
        },
        {
          "name": "assigneeMobileNumber",
          "jsonPath": "assignes/*/mobileNumber",
          "patternId": null,
          "defaultVisibility": "PLAIN"
        },
        {
          "name": "relationship",
          "jsonPath": "connectionHolders/*/relationship",
          "patternId": "005",
          "defaultVisibility": "PLAIN"
        }
      ],
      "roleBasedDecryptionPolicy": []
    },
    {
      "model": "WnSConnectionPlumber",
      "uniqueIdentifier": {
        "name": "applicationNo",
        "jsonPath": "/applicationNo"
      },
      "attributes": [  
        {
          "name": "plumberInfoMobileNumber",
          "jsonPath": "plumberInfo/*/mobileNumber",
          "patternId": "001",
          "defaultVisibility": "PLAIN"
        }
      ],
      "roleBasedDecryptionPolicy": [
        {
          "roles": ["WS_CEMP","WS_DOC_VERIFIER","WS_FIELD_INSPECTOR","WS_APPROVER","WS_CLERK","SW_CEMP","SW_DOC_VERIFIER","SW_FIELD_INSPECTOR","SW_APPROVER","SW_CLERK"],
          "attributeAccessList": [
           {
              "attribute": "plumberInfoMobileNumber",
              "firstLevelVisibility": "MASKED",
              "secondLevelVisibility": "PLAIN"
            }
          ]
        },
        {
          "roles": ["REINDEXING_ROLE"],
          "attributeAccessList": [
            {
              "attribute": "plumberInfoMobileNumber",
              "firstLevelVisibility": "ENCRYPTED",
              "secondLevelVisibility": "PLAIN"
            }
          ]
        }
      ]
    },
    {
      "model": "WnSConnectionPlumberDecrypDisabled",
      "uniqueIdentifier": {
        "name": "applicationNo",
        "jsonPath": "/applicationNo"
      },
      "attributes": [
        {
          "name": "plumberInfoMobileNumber",
          "jsonPath": "plumberInfo/*/mobileNumber",
          "patternId": null,
          "defaultVisibility": "PLAIN"
        }
      ],
      "roleBasedDecryptionPolicy": []
    }
```

Also, add the following under `roleBasedDecryptionPolicy` of **User model**(already existing):

```
"roleBasedDecryptionPolicy": [
        {
          "roles": ["REINDEXING_ROLE"],
          "attributeAccessList": [
            {
              "attribute": "mobileNumber",
              "firstLevelVisibility": "ENCRYPTED",
              "secondLevelVisibility": "PLAIN"
            }
          ]
        },
        {
          "roles": ["WS_CEMP","WS_DOC_VERIFIER","WS_FIELD_INSPECTOR","WS_APPROVER","WS_CLERK","SW_CEMP","SW_DOC_VERIFIER","SW_FIELD_INSPECTOR","SW_APPROVER","SW_CLERK"
          ],
          "attributeAccessList": [
            {
              "attribute": "mobileNumber",
              "firstLevelVisibility": "MASKED",
              "secondLevelVisibility": "PLAIN"
            },
            {
              "attribute": "fatherOrHusbandName",
              "firstLevelVisibility": "MASKED",
              "secondLevelVisibility": "PLAIN"
            },
            {
              "attribute": "correspondenceAddress",
              "firstLevelVisibility": "MASKED",
              "secondLevelVisibility": "PLAIN"
            },
            {
              "attribute": "name",
              "firstLevelVisibility": "PLAIN",
              "secondLevelVisibility": "PLAIN"
            },
            {
              "attribute": "emailId",
              "firstLevelVisibility": "MASKED",
              "secondLevelVisibility": "PLAIN"
            },
            {
              "attribute": "permanentAddress",
              "firstLevelVisibility": "MASKED",
              "secondLevelVisibility": "PLAIN"
            },
            {
              "attribute": "guardian",
              "firstLevelVisibility": "MASKED",
              "secondLevelVisibility": "PLAIN"
            }
          ]
        }
     ]      
```

Refer to the [SecurityPolicy.json](https://github.com/egovernments/egov-mdms-data/blob/UAT/data/pg/DataSecurity/SecurityPolicy.json) file for full reference.

{% hint style="info" %}
For modules, there is no such hard rule or pattern for naming the model, but it should be related to that service.\
_**ex**_: 1.) For user service we have two security policy models [_**User**_](https://github.com/egovernments/egov-mdms-data/blob/DEV/data/pb/DataSecurity/SecurityPolicy.json#L6) which is used when a user tries to search other user data. The PII data will be available in masked, plain or encrypted form depending on the visibility set for an attribute in the MDMS.\
The other model is [_**UserSelf**_](https://github.com/egovernments/egov-mdms-data/blob/DEV/data/pb/DataSecurity/SecurityPolicy.json#L247) which is used when a user tries to search their own data.  The data is available as per the configuration set there.

For _report_ and _searcher_ config the model name should be similar to the value that we are setting in the field **decryptionPathId**.     ex:- [Employee Report](https://github.com/egovernments/configs/blob/DEV/reports/config/employee-report.yml#L3). [Employee Report Security Model](https://github.com/egovernments/egov-mdms-data/blob/DEV/data/pb/DataSecurity/SecurityPolicy.json#L329).\
\
2.) For W\&S we have 2 models -`WnSConnection` and `WnSConnectionOwner` which are meant for ConnectionHolderDetails.\
2 different models for connectionHolder data are required since some data for connectionHolder comes from the W\&S tables and the remaining is fetched from the User table. So to maintain consistency we had to have 2 different models.
{% endhint %}

{% hint style="info" %}
For an attribute where its firstLevelVisibility is set as "**Masked**" whenever the respective search API is called without the **plain Access Request,** the masked value is returned as the API response for that attribute.\
**for ex**:- if for mobile number attribute’s firstLevelVisibility is masked and its plain value is 9089243280 then in response, the value is displayed as **\*\*\*\*\*\*3280.** The masking pattern is defined in the [**MaskingPattern**](https://github.com/egovernments/egov-mdms-data/blob/DEV/data/pb/DataSecurity/MaskingPatterns.json) MDMS file and the pattern is picked up based on the **patternId.** Similarly, if the firstLevelVisibility is set as "**ENCRYPTED**" we will get the encrypted value of that plain data (which is present in DB) in response.
{% endhint %}

{% hint style="info" %}
_**NOTE:**_ For _adding of new attribute for encryption_, the following things need to be kept in mind:

We **do not have a direct approach** to it, but a workaround is as follows:

1. We need to make sure which property has to be encrypted and what is the path of the property in the Request/Response object of W\&S. If PII data is for connectionholder and is coming from WnS tables directly, then with the Proper name and path of the object we can add a new Property in existing model _WnSConnection._\
   The inclusion of any new attribute here would need encryption of the old data for this new property.\
   For that, in MDMS, we will have to replace the existing model attributes with only new attributes and hit the `_encryptOldData` API. Once old data encryption is done, we can put back all the required attributes (old and +new) in the model.\
   Also, before starting the encryption of old data, we will have to check the latest record of the table `eg_ws_enc_audit` / `eg_sw_enc_audit` / `eg_pt_enc_audit`(for PT) . If the latest record has offset and record count value other than 0 then insert a random record with offset and record count as 0 and `createdtime` and `encryptiontime` as a current timestamp in millis in utc.
2. Any data other than that of connectionHolder would need a new model to be created and changes at the code level as well.\
   For old data encryption of new property other than that of connectionHolder, we will have to have code changes as well.
{% endhint %}

{% hint style="info" %}
For further info about adding models refer [here](https://digit-discuss.atlassian.net/wiki/spaces/DD/pages/2144862213/Encryption+Client+Library#Security-Policy).
{% endhint %}

## Backend Service Changes <a href="#backend-service-changes" id="backend-service-changes"></a>

#### Update the pom.xml file <a href="#update-the-pom.xml-file." id="update-the-pom.xml-file."></a>

* Upgrade services-common library version.

```
<dependency>
    <groupId>org.egov.services</groupId>
    <artifactId>services-common</artifactId>
    <version>1.1.0-SNAPSHOT</version>
</dependency>
```

* Upgrade the tracer library version.

```
<dependency>
    <groupId>org.egov.services</groupId>
    <artifactId>tracer</artifactId>
    <version>2.0.0-SNAPSHOT</version>
</dependency>
```

* Add enc-client library

```
<dependency>
	<groupId>org.egov</groupId>
		<artifactId>enc-client</artifactId>
		<version>2.0.4-SNAPSHOT</version>
		<exclusions>
			<exclusion>
				<groupId>org.springframework.kafka</groupId>
				<artifactId>spring-kafka</artifactId>
			</exclusion>
			<exclusion>
				<groupId>org.apache.kafka</groupId>
				<artifactId>kafka-clients</artifactId>
			</exclusion>
		</exclusions>
</dependency>
```

## Application Properties Changes

In ws-services encryption and decryption endpoints should be declared as follows:

```
#--------enable/disable ABAC in encryption----------#
water.decryption.abac.enabled=true

encryption.batch.value=500
encryption.offset.value=0

#-------Persister topics for oldDataEncryption-------#
egov.waterservice.oldDataEncryptionStatus.topic=ws-enc-audit
egov.waterservice.update.oldData.topic=update-ws-encryption
```

In sw-services encryption and decryption endpoints should be declared as follows:

```
#--------enable/disable ABAC in encryption----------#
sewerage.decryption.abac.enabled=true

encryption.batch.value=500
encryption.offset.value=0

#-------Persister topics for oldDataEncryption-------#
egov.sewerageservice.oldDataEncryptionStatus.topic=sw-enc-audit
egov.sewerageservice.update.oldData.topic=update-sw-encryption
```

**EncryptionDecryptionUtil.java**

We need an interfacing file for handling the encryption and decryption of attributes and for interacting with the enc-client library directly.\
\
For reference follow the below code snippet:

```
package org.egov.waterconnection.util;

import com.fasterxml.jackson.databind.ObjectMapper;
import lombok.extern.slf4j.Slf4j;
import org.egov.common.contract.request.RequestInfo;
import org.egov.common.contract.request.User;
import org.egov.encryption.EncryptionService;
import org.egov.encryption.audit.AuditService;
import org.egov.tracer.model.CustomException;
import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.beans.factory.annotation.Value;
import org.springframework.stereotype.Component;
import org.springframework.web.client.HttpClientErrorException;
import org.springframework.web.client.HttpServerErrorException;
import org.springframework.web.client.ResourceAccessException;

import java.io.IOException;
import java.util.*;

import static org.egov.waterconnection.constants.WCConstants.*;

@Slf4j
@Component
public class EncryptionDecryptionUtil {

    private EncryptionService encryptionService;

    @Autowired
    private AuditService auditService;

    @Autowired
    private ObjectMapper objectMapper;

    @Value(("${state.level.tenant.id}"))
    private String stateLevelTenantId;

    @Value(("${water.decryption.abac.enabled}"))
    private boolean abacEnabled;

    public EncryptionDecryptionUtil(EncryptionService encryptionService) {
        this.encryptionService = encryptionService;
    }

    public <T> T encryptObject(Object objectToEncrypt, String key, Class<T> classType) {
        try {
            if (objectToEncrypt == null) {
                return null;
            }
            T encryptedObject = encryptionService.encryptJson(objectToEncrypt, key, stateLevelTenantId, classType);
            if (encryptedObject == null) {
                throw new CustomException("ENCRYPTION_NULL_ERROR", "Null object found on performing encryption");
            }
            return encryptedObject;
        } catch (Exception e) {
            log.error("Unknown Error occurred while encrypting", e);
            throw new CustomException("UNKNOWN_ERROR", "Unknown error occurred in encryption process");
        }
    }

    public <E, P> P decryptObject(Object objectToDecrypt, String key, Class<E> classType, RequestInfo requestInfo) {

        try {
            boolean objectToDecryptNotList = false;
            if (objectToDecrypt == null) {
                return null;
            } else if (requestInfo == null || requestInfo.getUserInfo() == null) {
                User userInfo = User.builder().uuid("no uuid").type("EMPLOYEE").build();
                requestInfo = RequestInfo.builder().userInfo(userInfo).build();
            }
            if (!(objectToDecrypt instanceof List)) {
                objectToDecryptNotList = true;
                objectToDecrypt = Collections.singletonList(objectToDecrypt);
            }

            Map<String, String> keyPurposeMap = getKeyToDecrypt(objectToDecrypt, key);
            String purpose = keyPurposeMap.get("purpose");

            if (key.equalsIgnoreCase(WNS_ENCRYPTION_MODEL) || key.equalsIgnoreCase(WNS_OWNER_ENCRYPTION_MODEL) || key.equalsIgnoreCase(WNS_PLUMBER_ENCRYPTION_MODEL))
                key = keyPurposeMap.get("key");

            P decryptedObject = (P) encryptionService.decryptJson(requestInfo, objectToDecrypt, key, purpose, classType);
            if (decryptedObject == null) {
                throw new CustomException("DECRYPTION_NULL_ERROR", "Null object found on performing decryption");
            }

            if (objectToDecryptNotList) {
                decryptedObject = (P) ((List<E>) decryptedObject).get(0);
            }
            return decryptedObject;
        } catch (IOException | HttpClientErrorException | HttpServerErrorException | ResourceAccessException e) {
            log.error("Error occurred while decrypting", e);
            throw new CustomException("DECRYPTION_SERVICE_ERROR", "Error occurred in decryption process");
        } catch (Exception e) {
            log.error("Unknown Error occurred while decrypting", e);
            throw new CustomException("UNKNOWN_ERROR", "Unknown error occurred in decryption process");
        }
    }

    public Map<String, String> getKeyToDecrypt(Object objectToDecrypt, String key) {
        Map<String, String> keyPurposeMap = new HashMap<>();

        if (!abacEnabled) {
            if (key.equals(WNS_ENCRYPTION_MODEL) || key == null) {
                keyPurposeMap.put("key", "WnSConnectionDecrypDisabled");
                keyPurposeMap.put("purpose", "WnSConnectionDecryptionDisabled");
            } else if (key.equals(WNS_OWNER_ENCRYPTION_MODEL)) {
                keyPurposeMap.put("key", "WnSConnectionOwnerDecrypDisabled");
                keyPurposeMap.put("purpose", "WnSConnectionDecryptionDisabled");
            } else if (key.equals(WNS_PLUMBER_ENCRYPTION_MODEL)) {
                keyPurposeMap.put("key", "WnSConnectionPlumberDecrypDisabled");
                keyPurposeMap.put("purpose", "WnSConnectionPlumberDecrypDisabled");
            }
        } else {
            if (key.equals(WNS_ENCRYPTION_MODEL) || key == null) {
                keyPurposeMap.put("key", WNS_ENCRYPTION_MODEL);
                keyPurposeMap.put("purpose", "WnSConnectionSearch");
            } else if (key.equals(WNS_OWNER_ENCRYPTION_MODEL)) {
                keyPurposeMap.put("key", WNS_OWNER_ENCRYPTION_MODEL);
                keyPurposeMap.put("purpose", "WnSConnectionSearch");
            } else if (key.equals(WNS_PLUMBER_ENCRYPTION_MODEL)) {
                keyPurposeMap.put("key", WNS_PLUMBER_ENCRYPTION_MODEL);
                keyPurposeMap.put("purpose", "WnSConnectionPlumberSearch");
            }
        }

        return keyPurposeMap;
    }
}

```

You may find the file [here](https://github.com/egovernments/DIGIT-Dev/blob/develop/municipal-services/ws-services/src/main/java/org/egov/waterconnection/util/EncryptionDecryptionUtil.java) in the repo.

**UnmaskingUtil.java**

UnmaskingUtil.java file helps in extracting the plain data of the Owner from the User service.\
This file also contains a method that swaps the PlumberInfo in a similar manner.

For reference follow the below code snippet:

```
package org.egov.waterconnection.util;

import java.util.*;
import java.util.function.Function;
import java.util.stream.Collectors;
import java.util.stream.StreamSupport;

import org.egov.common.contract.request.PlainAccessRequest;
import org.egov.common.contract.request.RequestInfo;
import org.egov.waterconnection.web.models.OwnerInfo;
import org.egov.waterconnection.service.UserService;
import org.egov.waterconnection.web.models.PlumberInfo;
import org.egov.waterconnection.web.models.WaterConnection;
import org.egov.waterconnection.web.models.users.UserDetailResponse;
import org.egov.waterconnection.web.models.users.UserSearchRequest;
import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.stereotype.Component;
import org.springframework.util.ObjectUtils;
import org.springframework.util.StringUtils;

@Component
public class UnmaskingUtil {

    private static List<String> plainRequestFieldsList;

    @Autowired
    private UserService userService;

    public void getOwnerDetailsUnmasked(WaterConnection waterConnection, RequestInfo requestInfo) {

        PlainAccessRequest apiPlainAccessRequest = requestInfo.getPlainAccessRequest();

        List<String> plainRequestFieldsList = getAllFieldsPlainAccessList();
        PlainAccessRequest plainAccessRequest = PlainAccessRequest.builder()
                .plainRequestFields(plainRequestFieldsList)
                .build();
        requestInfo.setPlainAccessRequest(plainAccessRequest);

        UserSearchRequest userSearchRequest = userService.getBaseUserSearchRequest(waterConnection.getTenantId(), requestInfo);

        Set<String> ownerIds = new HashSet<>();

        for (OwnerInfo ownerInfo : waterConnection.getConnectionHolders()) {

            String currentOwnerId = ownerInfo.getUuid();

            /*
             * once user module is updated to handle masked update
             * users will be unmasked on need, currently all.
             */
            ownerIds.clear();
            ownerIds.add(currentOwnerId);
            userSearchRequest.setUuid(ownerIds);
            plainAccessRequest.setRecordId(currentOwnerId);

            UserDetailResponse userDetailResponse = userService.getUser(userSearchRequest);

            if(!ObjectUtils.isEmpty(userDetailResponse.getUser())) {
                OwnerInfo unmaskedUser = userDetailResponse.getUser().get(0);
                updateMaskedOwnerInfoWithUnmaskedFields(ownerInfo, unmaskedUser);
            }
            requestInfo.setPlainAccessRequest(apiPlainAccessRequest);
        }

    }

    private void updateMaskedOwnerInfoWithUnmaskedFields(OwnerInfo ownerInfo, OwnerInfo unmaskedUser) {

        if (ownerInfo.getFatherOrHusbandName().contains("*")) {
            ownerInfo.setFatherOrHusbandName(unmaskedUser.getFatherOrHusbandName());
        }
        if (ownerInfo.getMobileNumber().contains("*")) {
            ownerInfo.setMobileNumber(unmaskedUser.getMobileNumber());
        }
        if (ownerInfo.getCorrespondenceAddress().contains("*")) {
            ownerInfo.setCorrespondenceAddress(unmaskedUser.getCorrespondenceAddress());
        }
        if (ownerInfo.getUserName().contains("*")) {
            ownerInfo.setUserName(unmaskedUser.getUserName());
        }
        if (ownerInfo.getName().contains("*")) {
            ownerInfo.setName(unmaskedUser.getName());
        }
        if (ownerInfo.getGender().contains("*")) {
            ownerInfo.setGender(unmaskedUser.getGender());
        }
    }

    public static List<String> getAllFieldsPlainAccessList() {

        if (plainRequestFieldsList == null) {

            plainRequestFieldsList = new ArrayList<>();
            plainRequestFieldsList.add("mobileNumber");
            plainRequestFieldsList.add("guardian");
            plainRequestFieldsList.add("fatherOrHusbandName");
            plainRequestFieldsList.add("correspondenceAddress");
            plainRequestFieldsList.add("userName");
            plainRequestFieldsList.add("name");
            plainRequestFieldsList.add("gender");
        }
        return plainRequestFieldsList;
    }

    /**
     * Method returns true then owner info is modified for update,
     * it should be unmasked for unchanged field updates
     *
     * @param ownerInfo
     * @return Boolean
     */
    private Boolean shouldOwnerBeUnmaksed(OwnerInfo ownerInfo) {

        return !(ownerInfo.getFatherOrHusbandName().contains("*") &&

                ownerInfo.getMobileNumber().contains("*") &&

                ownerInfo.getCorrespondenceAddress().contains("*") &&

                ownerInfo.getUserName().contains("*") &&

                ownerInfo.getName().contains("*") &&

                ownerInfo.getGender().contains("*"));

    }


    /**
     * Method returns unmasked PlumberInfo,
     * it should be unmasked for unchanged field updates
     *
     * @param plumberInfos
     * @param unmaskedPlumberInfos
     */
    public boolean getUnmaskedPlumberInfo(List<PlumberInfo> plumberInfos, List<PlumberInfo> unmaskedPlumberInfos) {
        Map<String, PlumberInfo> unmaskedPlumberInfoMap;
        boolean isPlumberSwapped = false;
        if (!ObjectUtils.isEmpty(unmaskedPlumberInfos)) {
            unmaskedPlumberInfoMap = unmaskedPlumberInfos.stream().collect(Collectors.toMap(PlumberInfo::getId, Function.identity()));
            if (!ObjectUtils.isEmpty(plumberInfos)) {
                for (PlumberInfo plumberInfo : plumberInfos) {
                    if (!StringUtils.isEmpty(plumberInfo.getMobileNumber()) && plumberInfo.getMobileNumber().contains("*")) {
                        if (!StringUtils.isEmpty(unmaskedPlumberInfoMap.get(plumberInfo.getId()))) {
                            plumberInfo.setMobileNumber(unmaskedPlumberInfoMap.get(plumberInfo.getId()).getMobileNumber());
                            isPlumberSwapped = true;
                        }
                    }
                }
            }
        }
        return isPlumberSwapped;
    }

}
```

You may find the file [here](https://github.com/egovernments/DIGIT-Dev/blob/develop/municipal-services/ws-services/src/main/java/org/egov/waterconnection/util/UnmaskingUtil.java) in the repo.

### **Important Methods To Add** <a href="#important-methods-to-be-added" id="important-methods-to-be-added"></a>

#### Method to encrypt the water/sewerage requestBody data: <a href="#method-to-encrypt-the-water-sewerage-requestbody-data" id="method-to-encrypt-the-water-sewerage-requestbody-data"></a>

The following method is added in `WaterServiceImpl`.java for encrypting the entire data

```
    /**
	 * Encrypts waterConnection details
	 *
	 * @param waterConnection contains  waterConnection object
	 *
	 */
	private WaterConnection encryptConnectionDetails(WaterConnection waterConnection) {
		/* encrypt here */
		waterConnection = encryptionDecryptionUtil.encryptObject(waterConnection, WNS_ENCRYPTION_MODEL, WaterConnection.class);
		waterConnection = encryptionDecryptionUtil.encryptObject(waterConnection, WNS_PLUMBER_ENCRYPTION_MODEL, WaterConnection.class);
		List<OwnerInfo> connectionHolders = waterConnection.getConnectionHolders();
		if (!CollectionUtils.isEmpty(connectionHolders)) {
			int k = 0;
			for (OwnerInfo holderInfo : connectionHolders) {
				waterConnection.getConnectionHolders().set(k, encryptionDecryptionUtil.encryptObject(holderInfo, WNS_OWNER_ENCRYPTION_MODEL, OwnerInfo.class));
				k++;
			}
		}
		return waterConnection;
	}
```

**Method to decrypt the water/sewerage data:**

The following method is added in `WaterServiceImpl`.java for decrypting the entire data

```
    /**
	 * Decrypts waterConnection details
	 *
	 * @param waterConnection contains  waterConnection object
	 */
	private WaterConnection decryptConnectionDetails(WaterConnection waterConnection, RequestInfo requestInfo) {
		/* decrypt here */
		waterConnection = encryptionDecryptionUtil.decryptObject(waterConnection, WNS_ENCRYPTION_MODEL, WaterConnection.class, requestInfo);
		waterConnection = encryptionDecryptionUtil.decryptObject(waterConnection, WNS_PLUMBER_ENCRYPTION_MODEL, WaterConnection.class, requestInfo);
		List<OwnerInfo> connectionHolders = waterConnection.getConnectionHolders();
		if (!CollectionUtils.isEmpty(connectionHolders))
			waterConnection.setConnectionHolders(encryptionDecryptionUtil.decryptObject(connectionHolders, WNS_OWNER_ENCRYPTION_MODEL, OwnerInfo.class, requestInfo));

		return waterConnection;
	}
```

**\_search API Changes**

During the search call the PII data needs to be masked in the response received.\
For this, the searchCriteria needs to be encrypted before fetching details and eventually the data retrieved needs to be decrypted and then returned to the user.

Following changes need to be made in `WaterServiceImpl`.java

```
public List<WaterConnection> search(SearchCriteria criteria, RequestInfo requestInfo) {
		List<WaterConnection> waterConnectionList;

		//Creating copies of apiPlainAcessRequests for decryption process
		//Any decryption process returns the  requestInfo with only the already used plain Access Request fields

		PlainAccessRequest apiPlainAccessRequest = null, apiPlainAccessRequestCopy = null;
		if (!ObjectUtils.isEmpty(requestInfo.getPlainAccessRequest())) {
			PlainAccessRequest plainAccessRequest = requestInfo.getPlainAccessRequest();
			if (!StringUtils.isEmpty(plainAccessRequest.getRecordId()) && !ObjectUtils.isEmpty(plainAccessRequest.getPlainRequestFields())) {
				apiPlainAccessRequest = new PlainAccessRequest(plainAccessRequest.getRecordId(), plainAccessRequest.getPlainRequestFields());
				apiPlainAccessRequestCopy = new PlainAccessRequest(plainAccessRequest.getRecordId(), plainAccessRequest.getPlainRequestFields());
			}
		}
		/* encrypt here */
		if (criteria.getIsInternalCall()) {
			criteria = encryptionDecryptionUtil.encryptObject(criteria, "WnSConnectionDecrypDisabled", SearchCriteria.class);
			criteria = encryptionDecryptionUtil.encryptObject(criteria, "WnSConnectionPlumberDecrypDisabled", SearchCriteria.class);
		} else {
			criteria = encryptionDecryptionUtil.encryptObject(criteria, WNS_ENCRYPTION_MODEL, SearchCriteria.class);
			criteria = encryptionDecryptionUtil.encryptObject(criteria, WNS_PLUMBER_ENCRYPTION_MODEL, SearchCriteria.class);
		}
		waterConnectionList = getWaterConnectionsList(criteria, requestInfo);
		if (!StringUtils.isEmpty(criteria.getSearchType()) &&
				criteria.getSearchType().equals(WCConstants.SEARCH_TYPE_CONNECTION)) {
			waterConnectionList = enrichmentService.filterConnections(waterConnectionList);
			/*if(criteria.getIsPropertyDetailsRequired()){
				waterConnectionList = enrichmentService.enrichPropertyDetails(waterConnectionList, criteria, requestInfo);
			}*/
		}
		if ((criteria.getIsPropertyDetailsRequired() != null) && criteria.getIsPropertyDetailsRequired()) {
			waterConnectionList = enrichmentService.enrichPropertyDetails(waterConnectionList, criteria, requestInfo);
		}
		waterConnectionValidator.validatePropertyForConnection(waterConnectionList);
		enrichmentService.enrichConnectionHolderDeatils(waterConnectionList, criteria, requestInfo);
		enrichmentService.enrichProcessInstance(waterConnectionList, criteria, requestInfo);
//		enrichmentService.enrichDocumentDetails(waterConnectionList, criteria, requestInfo);

		requestInfo.setPlainAccessRequest(apiPlainAccessRequest);
		/* decrypt here */
		if (criteria.getIsInternalCall()) {
			waterConnectionList = encryptionDecryptionUtil.decryptObject(waterConnectionList, "WnSConnectionPlumberDecrypDisabled", WaterConnection.class, requestInfo);
			requestInfo.setPlainAccessRequest(apiPlainAccessRequestCopy);
			return encryptionDecryptionUtil.decryptObject(waterConnectionList, "WnSConnectionDecrypDisabled", WaterConnection.class, requestInfo);
		}
		waterConnectionList = encryptionDecryptionUtil.decryptObject(waterConnectionList, WNS_PLUMBER_ENCRYPTION_MODEL, WaterConnection.class, requestInfo);
		requestInfo.setPlainAccessRequest(apiPlainAccessRequestCopy);
		return encryptionDecryptionUtil.decryptObject(waterConnectionList, WNS_ENCRYPTION_MODEL, WaterConnection.class, requestInfo);
	}
```

You may find the file [here](https://github.com/egovernments/DIGIT-Dev/blob/484e8be7c4eca4befc892b3c8484683f77628d58/municipal-services/ws-services/src/main/java/org/egov/waterconnection/service/WaterServiceImpl.java#L184) in the repo.

If you want to get all the PII data in the plain format then in the search request add the search param **“isInternalCall“** as **“true”**

If the user wants only specific fields to be unmasked then add the `plainAccessRequest` in the RequestBody in the following format:

```
{
    "RequestInfo": {
        "apiId": "Rainmaker",
        "authToken": "03df03a9-58c4-47a7-96eb-e745570ac6b7",
        "userInfo": {
            "id": 12105,
            "uuid": "6d29df57-c2bd-4fd5-ab6c-2815749ebff8",
            "userName": "QAWSSU",
            "name": "Lata Naik",
            "mobileNumber": "9090909091",
            "emailId": "lata@gmail.com",
            "locale": null,
            "type": "EMPLOYEE",
            "roles": [
                {
                    "name": "PT Doc Verifier",
                    "code": "PT_DOC_VERIFIER",
                    "tenantId": "pb.amritsar"
                },
                {
                    "name": "WS Document Verifier",
                    "code": "WS_DOC_VERIFIER",
                    "tenantId": "pb.amritsar"
                },
                {
                    "name": "SW Field Inspector",
                    "code": "SW_FIELD_INSPECTOR",
                    "tenantId": "pb.amritsar"
                },
                {
                    "name": "SW Document Verifier",
                    "code": "SW_DOC_VERIFIER",
                    "tenantId": "pb.amritsar"
                },
                {
                    "name": "PT Counter Employee",
                    "code": "PT_CEMP",
                    "tenantId": "pb.amritsar"
                },
                {
                    "name": "WS Approver",
                    "code": "WS_APPROVER",
                    "tenantId": "pb.amritsar"
                },
                {
                    "name": "PT Counter Approver",
                    "code": "PT_APPROVER",
                    "tenantId": "pb.amritsar"
                },
                {
                    "name": "PT Field Inspector",
                    "code": "PT_FIELD_INSPECTOR",
                    "tenantId": "pb.amritsar"
                },
                {
                    "name": "WS Counter Employee",
                    "code": "WS_CEMP",
                    "tenantId": "pb.amritsar"
                },
                {
                    "name": "SW Counter Employee",
                    "code": "SW_CEMP",
                    "tenantId": "pb.amritsar"
                },
                {
                    "name": "SW Clerk",
                    "code": "SW_CLERK",
                    "tenantId": "pb.amritsar"
                },
                {
                    "name": "WS Field Inspector",
                    "code": "WS_FIELD_INSPECTOR",
                    "tenantId": "pb.amritsar"
                },
                {
                    "name": "WS Clerk",
                    "code": "WS_CLERK",
                    "tenantId": "pb.amritsar"
                },
                {
                    "name": "SW Approver",
                    "code": "SW_APPROVER",
                    "tenantId": "pb.amritsar"
                }
            ],
            "active": true,
            "tenantId": "pb.amritsar",
            "permanentCity": null
        },
        "msgId": "1667459745751|en_IN",
        "plainAccessRequest": {
            "recordId": "e7989e70-b5cc-4361-8837-64f47bd297b5",
            "plainRequestFields": [
                "correspondenceAddress","guardian"
            ]
        }
    }
}
```

`plainAccessRequest` contains :\
1\. `recordId` which will take the uuid of the user as an input for which PII data has to be unmasked, and\
2\. `plainRequestFields` will take an array of attributes that need to be unmasked. These attributes should comply with the attributes used in the Mdms SecurityPolicy.json’s models created.

For unmasking PlumberInfoMobileNumber, recordId will take the applicationno as value.

**\_create and \_update API Changes**

In \_create and \_update API calls the data needs to be encrypted before the data for application/connection is pushed to respective topics.

A sample code line for encrypting data in these calls is as follows:

```
waterConnectionRequest.setWaterConnection(encryptConnectionDetails(waterConnectionRequest.getWaterConnection()));
```

A sample code line for decrypting data in these calls is as follows:

```
waterConnectionRequest.setWaterConnection(encryptionDecryptionUtil.decryptObject(waterConnectionRequest.getWaterConnection(), WNS_ENCRYPTION_MODEL, WaterConnection.class, waterConnectionRequest.getRequestInfo()));
```

The entire method for create call can be found here: [create method](https://github.com/egovernments/DIGIT-Dev/blob/484e8be7c4eca4befc892b3c8484683f77628d58/municipal-services/ws-services/src/main/java/org/egov/waterconnection/service/WaterServiceImpl.java#L100)

and update call can be found here: [update method](https://github.com/egovernments/DIGIT-Dev/blob/484e8be7c4eca4befc892b3c8484683f77628d58/municipal-services/ws-services/src/main/java/org/egov/waterconnection/service/WaterServiceImpl.java#L279)

### Encrypting Old Data In The DB

Before using the privacy feature in any environment, the encryption of existing data in the dB should be done.

An API for the same is written in the service and needs to be triggered by port-forwarding the respective service pod.

The data encryption API uses the existing plainSearch method and the encryption shall take place _**tenantId-wise.**_ If tenantId is not specified then all the tenants are picked from the MDMS repository and the encryption happens for all the tenants. However, if the tenantId is specified, then the encryption happens only for that tenantId.

The following method is added to execute the oldDataEncryption

**In WaterController.java**

```
    /**
	 * Encrypts existing Water records
	 *
	 * @param requestInfoWrapper RequestInfoWrapper
	 * @param criteria SearchCriteria
	 * @return list of updated encrypted data
	 */
	/* To be executed only once */
	@RequestMapping(value = "/_encryptOldData", method = RequestMethod.POST)
	public ResponseEntity<WaterConnectionResponse> encryptOldData(@Valid @RequestBody RequestInfoWrapper requestInfoWrapper,
			@Valid @ModelAttribute SearchCriteria criteria){
		WaterConnectionResponse waterConnectionResponse = waterEncryptionService.updateOldData(criteria, requestInfoWrapper.getRequestInfo());
		waterConnectionResponse.setResponseInfo(
				responseInfoFactory.createResponseInfoFromRequestInfo(requestInfoWrapper.getRequestInfo(), true));
		return new ResponseEntity<>(waterConnectionResponse, HttpStatus.OK);
	}
```

**n WaterEncryptionService.java**\
This service is solely for old data encryption and can be referred from here:\
[https://github.com/egovernments/DIGIT-Dev/blob/8ec8592b73470c6dcdb1508caa1e6b1cf8ebb2ca/municipal-services/ws-services/src/main/java/org/egov/waterconnection/service/WaterEncryptionService.java](https://github.com/egovernments/DIGIT-Dev/blob/8ec8592b73470c6dcdb1508caa1e6b1cf8ebb2ca/municipal-services/ws-services/src/main/java/org/egov/waterconnection/service/WaterEncryptionService.java)\
\
A _**new persister file**_ needs to be added for keeping track of progress of oldDataEncryption.\
Refer this [ws-enc-audit-persister.yml](https://github.com/egovernments/configs/blob/UAT/egov-persister/ws-enc-audit-persister.yml) and [sw-enc-audit-persister.yml](https://github.com/egovernments/configs/blob/UAT/egov-persister/sw-enc-audit-persister.yml) for the same.

Here is the Postman collection for all _**property, water**_ and _**sewerage**_ services for _**old Data encryption**_ :\
[https://www.getpostman.com/collections/b3858ec2020462a6407d](https://www.getpostman.com/collections/b3858ec2020462a6407d)

### **Re-indexing Old Data In The Base Indexes**

There is **no need** to re-index the base indexes(_**viz.**_ water-services/ sewerage-services) once the API for old data encryption is executed as this will happen during the API execution itself.\
For any new data getting created, the new data will get saved in the encrypted format only in the indexes.

There are some changes in the Indexer file that need to be made for W\&S to get the encrypted data from the external service like Property-service.

```
externalUriMapping:
          - path: http://property-services.egov:8080/property-services/property/_search
            queryParam: propertyIds=$.propertyId,tenantId=$.tenantId
            apiRequest: {"RequestInfo":{"apiId":"org.egov.pt","ver":"1.0","ts":1502890899493,"action":"asd","did":"4354648646","key":"xyz","msgId":"654654","requesterId":"61","authToken":"d9994555-7656-4a67-ab3a-a952a0d4dfc8","userInfo":{"id":1,"uuid":"1fec8102-0e02-4d0a-b283-cd80d5dab067","type":"EMPLOYEE","tenantId":"pb.amritsar","roles":[{"name":"Reindexing Role","code":"REINDEXING_ROLE","tenantId":"pb.amritsar"}]}}}
            uriResponseMapping:
            - inJsonPath: $.Properties[0].usageCategory
              outJsonPath: $.Data.propertyUsageType
            - inJsonPath: $.Properties[0].owners[*].mobileNumber
              outJsonPath: $.Data.ownerMobileNumbers
```

So, in the URL mentioned above in `apiRequest`, change the role from EMPLOYEE to REINDEXING\_ROLE.\
Reference for changes :\
[<img src="https://github.com/fluidicon.png" alt="" data-size="line">\[UM-4382\]- Updated indexer for water service by hinamakhija-eGov · Pull Request #2342 · egovernments/configs](https://github.com/egovernments/configs/pull/2342)\
[<img src="https://github.com/fluidicon.png" alt="" data-size="line">\[UM-4382\]-Updated indexer for sewerage by hinamakhija-eGov · Pull Request #2345 · egovernments/configs](https://github.com/egovernments/configs/pull/2345)\
This role is a newly defined role in MDMS as already mentioned in the changes at the top.\
This Role helps in getting the Encrypted data in accordance to  `firstLevelVisibilty` defined for it.\
\
For W\&S, we need encrypted MobileNumber in the index because W\&S inbox uses Elastic search and we require mobileNumber search for the same hence owner MobileNumber has to be there mandatorily in the index for search.\
\
The changes need to be made in all the topics for W\&S indexes. For more details find the changes [here](https://github.com/egovernments/configs/blob/66b14e09aa03604e67c2e4966a4c833a2fb38c72/egov-indexer/water-service.yml#L91).

### **Enabling / Disabling Privacy** <a href="#enabling-disabling-privacy" id="enabling-disabling-privacy"></a>

To enable or disable decryption in privacy, we need to make changes to only the privacy variable present in the environment file in DevOps.

For enabling, its value should be “true” else “false”.

For water-services variable is as follows:

```
water-decryption-abac-enabled: "true"
```

For sewerage-services:

```
sewerage-decryption-abac-enabled: "true"
```

For user-service:

```
decryption-abac-enabled: "true"
```

The variable can be found in the file [here](https://github.com/egovernments/DIGIT-DevOps/blob/master/deploy-as-code/helm/environments/qa.yaml).

{% hint style="info" %}
**Note:** Privacy decryption means: For any new application creation/ old application updation Internal data will be stored in the encrypted form itself, just that during decryption disabled it would give PLAIN text rather than masked one.
{% endhint %}

{% hint style="info" %}
All the above changes need to be done for sw-services as well.
{% endhint %}

For detailed steps to configure the above changes refer to document: [Detailed Steps to configure privacy in W\&S module](https://digit-discuss.atlassian.net/l/cp/fFwvnmY8)

\
