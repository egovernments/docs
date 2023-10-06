---
description: Backend technical documentation
---

# PT Privacy Changes

## Overview <a href="#overview" id="overview"></a>

This document highlights the changes that need to be done in a Property module to support the privacy feature.

## Pre-requisites <a href="#pre-requisites" id="pre-requisites"></a>

* Prior Knowledge of Java/J2EE.
* Prior Knowledge of Spring Boot.
* MDMS Service
* Encryption Service

### MDMS Changes <a href="#mdms-changes" id="mdms-changes"></a>

#### Update the SecurityPolicy.json file. <a href="#update-the-securitypolicy.json-file." id="update-the-securitypolicy.json-file."></a>

The Security Policy MDMS file must have the model configuration for fields to be encrypted/decrypted.\
The following models have been used for W\&S in SecurityPolicy.json file:

```
    {
      "model": "Property",
      "uniqueIdentifier": {
        "name": "uuid",
        "jsonPath": "/owners/0/uuid"
      },
      "attributes": [
        {
          "name": "street",
          "jsonPath": "address/street",
          "patternId": "005",
          "defaultVisibility": "PLAIN"
        },
        {
          "name": "doorNo",
          "jsonPath": "address/doorNo",
          "patternId": "005",
          "defaultVisibility": "PLAIN"
        },
        {
          "name": "landmark",
          "jsonPath": "address/landmark",
          "patternId": "005",
          "defaultVisibility": "PLAIN"
        }
      ],
      "roleBasedDecryptionPolicy": [
        {
          "roles": ["WS_CEMP","WS_DOC_VERIFIER","WS_FIELD_INSPECTOR","WS_APPROVER","WS_CLERK","SW_CEMP","SW_DOC_VERIFIER","SW_FIELD_INSPECTOR","SW_APPROVER","SW_CLERK","PT_APPROVER", "PT_CEMP", "PT_COLLECTION_EMP", "PT_FIELD_INSPECTOR", "PT_DOC_VERIFIER"],
          "attributeAccessList": [
            {
              "attribute": "street",
              "firstLevelVisibility": "MASKED",
              "secondLevelVisibility": "PLAIN"
            },
            {
              "attribute": "doorNo",
              "firstLevelVisibility": "MASKED",
              "secondLevelVisibility": "PLAIN"
            },
            {
              "attribute": "landmark",
              "firstLevelVisibility": "MASKED",
              "secondLevelVisibility": "PLAIN"
            }
          ]
        },
        {
          "roles": ["REINDEXING_ROLE"],
          "attributeAccessList": [
            {
              "attribute": "street",
              "firstLevelVisibility": "ENCRYPTED",
              "secondLevelVisibility": "PLAIN"
            },
            {
              "attribute": "doorNo",
              "firstLevelVisibility": "ENCRYPTED",
              "secondLevelVisibility": "PLAIN"
            },
            {
              "attribute": "landmark",
              "firstLevelVisibility": "ENCRYPTED",
              "secondLevelVisibility": "PLAIN"
            }
          ]
        }
      ]
    },
    {
      "model": "PropertyDecrypDisabled",
      "uniqueIdentifier": {
        "name": "propertyId",
        "jsonPath": "/propertyId"
      },
      "attributes": [
        {
          "name": "street",
          "jsonPath": "address/street",
          "patternId": null,
          "defaultVisibility": "PLAIN"
        },
        {
          "name": "doorNo",
          "jsonPath": "address/doorNo",
          "patternId": null,
          "defaultVisibility": "PLAIN"
        },
        {
          "name": "landmark",
          "jsonPath": "address/landmark",
          "patternId": null,
          "defaultVisibility": "PLAIN"
        }
      ],
      "roleBasedDecryptionPolicy": []
    },
```

Next, add the following (if not already there) under `roleBasedDecryptionPolicy` of **User model** (already existing):

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
_**ex**_: 1.) For user service we have two security policy models [_**User**_](https://github.com/egovernments/egov-mdms-data/blob/DEV/data/pb/DataSecurity/SecurityPolicy.json#L6) which is used when a user tries to search other user data and he/she will get the PII data in masked, plain or encrypted form depending on the visibility sets for an attribute in the MDMS.\
And another model is [_**UserSelf**_](https://github.com/egovernments/egov-mdms-data/blob/DEV/data/pb/DataSecurity/SecurityPolicy.json#L247) which is used when a user tries to search their own data, they get the data as per the configuration set there. For _report_ and _searcher_ config the model name should be similar to the value that we are setting in the field **decryptionPathId**.     ex:- [Employee Report](https://github.com/egovernments/configs/blob/DEV/reports/config/employee-report.yml#L3).   [Employee Report Security Model](https://github.com/egovernments/egov-mdms-data/blob/DEV/data/pb/DataSecurity/SecurityPolicy.json#L329)

2.) For Property we have a model `Property` which is for Address fields like street, doorNo, landmark encryption and decryption.
{% endhint %}

{% hint style="info" %}
For an attribute where its firstLevelVisibility is set as "**Masked**" and whenever the respective search API is called without the **plain Access Request** then in the API response for that attribute we will get the masked value\
**for ex**:- if for mobile number attribute’s firstLevelVisibility is masked and its plain value is 9089243280 then in response, we will get value as **\*\*\*\*\*\*3280** and the masking pattern is defined in the [**MaskingPattern**](https://github.com/egovernments/egov-mdms-data/blob/DEV/data/pb/DataSecurity/MaskingPatterns.json) MDMS file and the pattern is picked up based on **patternId.** Similarly, if firstLevelVisibility is set as "**ENCRYPTED**" we will get the encrypted value of that plain data (which is present in DB) in the response.
{% endhint %}

{% hint style="info" %}
_**NOTE:**_ For _adding of new attribute for encryption_, the following things need to be kept in mind:

We **do not have a direct approach** to it, but a workaround is as follows:

1. We need to make sure which property has to be encrypted and what is the path of the property in the Request/Response object of Property. We can add a new property to the existing model _Property._\
   The inclusion of any new attribute here would need encryption of the old data for this new property.\
   For that, in MDMS, we will have to replace the existing model attributes with only new attributes and hit the `_encryptOldData` API. Once old data encryption is done, we can put back all the required attributes (old and +new) in the model.\
   Also, before starting the encryption of old data, we will have to check the latest record of the table `eg_pt_enc_audit.` If the latest record has offset and record count value other than 0 then insert a random record with offset and record count as 0 and `createdtime` and `encryptiontime` as a current timestamp in millis in utc.
{% endhint %}

{% hint style="info" %}
For further info about adding models refer [here](https://digit-discuss.atlassian.net/wiki/spaces/DD/pages/2144862213/Encryption+Client+Library#Security-Policy)
{% endhint %}

## Backend Service Changes <a href="#backend-service-changes" id="backend-service-changes"></a>

#### Update the pom.xml file. <a href="#update-the-pom.xml-file." id="update-the-pom.xml-file."></a>

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

## Application Properties Changes <a href="#application-properties-changes" id="application-properties-changes"></a>

In property-services encryption and decryption endpoints should be declared as follows:

```
#--------enable/disable ABAC in encryption----------#
property.decryption.abac.enabled=true

encryption.batch.value=500
encryption.offset.value=0

#-------Persister topics for oldDataEncryption-------#
property.oldDataEncryptionStatus.topic=pt-enc-audit
persister.update.property.oldData.topic=update-property-encryption
persister.update.property.audit.oldData.topic=update-property-audit-enc
persister.save.property.fuzzy.topic=save-property-fuzzy-data
```

Now, update the following existing property in application-properties:\
`property.es.index=pt-fuzzy-search-index`

#### EncryptionDecryptionUtil.java: <a href="#encryptiondecryptionutil.java" id="encryptiondecryptionutil.java"></a>

We need an interfacing file for handling the encryption and decryption of attributes and for interacting with enc-client library directly.

For reference follow the below code snippet

```
package org.egov.pt.util;

import com.fasterxml.jackson.databind.ObjectMapper;
import com.fasterxml.jackson.databind.node.ObjectNode;
import com.fasterxml.jackson.databind.node.TextNode;
import lombok.extern.slf4j.Slf4j;
import org.egov.common.contract.request.RequestInfo;
import org.egov.common.contract.request.Role;
import org.egov.common.contract.request.User;
import org.egov.encryption.EncryptionService;
import org.egov.encryption.audit.AuditService;
import org.egov.pt.config.PropertyConfiguration;
import org.egov.tracer.model.CustomException;
import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.beans.factory.annotation.Qualifier;
import org.springframework.beans.factory.annotation.Value;
import org.springframework.stereotype.Component;
import org.springframework.util.CollectionUtils;
import org.springframework.web.client.HttpClientErrorException;
import org.springframework.web.client.HttpServerErrorException;
import org.springframework.web.client.ResourceAccessException;

import java.io.IOException;
import java.util.*;

@Slf4j
@Component
public class EncryptionDecryptionUtil {

    private EncryptionService encryptionService;

    @Autowired
    private PropertyConfiguration config;

    @Autowired
    private AuditService auditService;

    @Autowired
    private ObjectMapper objectMapper;

    @Value(("${state.level.tenant.id}"))
    private String stateLevelTenantId;

    @Value(("${property.decryption.abac.enabled}"))
    private boolean abacEnabled;
    public EncryptionDecryptionUtil(EncryptionService encryptionService) {
        this.encryptionService = encryptionService;
    }

    public <T> T encryptObject(Object objectToEncrypt, String key, Class<T> classType) {
        try {
            if (objectToEncrypt == null) {
                return null;
            }
            T encryptedObject = encryptionService.encryptJson(objectToEncrypt, key, config.getStateLevelTenantId(), classType);
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
            }

           if (!(objectToDecrypt instanceof List)) {
                objectToDecryptNotList = true;
                objectToDecrypt = Collections.singletonList(objectToDecrypt);
            }

            Map<String, String> keyPurposeMap = getKeyToDecrypt(objectToDecrypt);
            String purpose = keyPurposeMap.get("PropertyEncDisabledSearch");

            if(key.equalsIgnoreCase(PTConstants.PROPERTY_MODEL))
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

    /**
     * Setting a fake user Info in case of open API calls
     * 
     * @param requestInfo
     * @return
     */
	private RequestInfo copyRequestInfoForEncryption(RequestInfo requestInfo) {
		
		RequestInfo requestInfoForDecryption;
		User fakeUSerInfo = User.builder().uuid("no uuid").type("EMPLOYEE").build();
		
		if ( requestInfo != null ) {
			
			 requestInfoForDecryption = RequestInfo.builder()
		    			.correlationId(requestInfo.getCorrelationId())
		    			.authToken(requestInfo.getAuthToken())
		    			.apiId(requestInfo.getApiId())
		    			.msgId(requestInfo.getMsgId())
		    			.build();
			 
				if (requestInfo.getUserInfo() == null)
					requestInfoForDecryption.setUserInfo(fakeUSerInfo);
				else
					requestInfoForDecryption.setUserInfo(requestInfo.getUserInfo());

		} else {
			
			requestInfoForDecryption = RequestInfo.builder().
					userInfo(fakeUSerInfo)
					.build();
		}
		

		return requestInfoForDecryption;
	}

	private User getEncrichedandCopiedUserInfo(User userInfo) {

		List<Role> newRoleList = new ArrayList<>();
		Boolean isUserTypeRoleFound = false;
		List<Role> roles = userInfo.getRoles();

		if (!CollectionUtils.isEmpty(roles)) {

			for (Role role : roles) {

				if (role.getCode().equalsIgnoreCase(userInfo.getType()))
					isUserTypeRoleFound = true;

                Role newRole = Role.builder()
                		.tenantId(role.getTenantId())
                		.code(role.getCode())
                		.name(role.getName())
                		.id(role.getId())
                		.build();
                
                newRoleList.add(newRole);
            }
        }

        if (!isUserTypeRoleFound) {
        	
            Role roleFromtype = Role.builder()
            		.tenantId(userInfo.getTenantId())
            		.code(userInfo.getType())
            		.name(userInfo.getType())
            		.build();
            newRoleList.add(roleFromtype);
        }
        
        return User.builder()
        		.roles(newRoleList)
        		.id(userInfo.getId())
        		.name(userInfo.getName())
                .type(userInfo.getType())
                .uuid(userInfo.getUuid())
                .emailId(userInfo.getEmailId())
                .userName(userInfo.getUserName())
                .tenantId(userInfo.getTenantId())
                .mobileNumber(userInfo.getMobileNumber())
                .build();
    }

    public Map<String,String> getKeyToDecrypt(Object objectToDecrypt) {
        Map<String,String> keyPurposeMap = new HashMap<>();

        if (!abacEnabled){
            keyPurposeMap.put("key","PropertyDecrypDisabled");
            keyPurposeMap.put("purpose","AbacDisabled");
        }
        else{
            keyPurposeMap.put("key","Property");
            keyPurposeMap.put("purpose","PropertySearch");
        }

        return keyPurposeMap;
    }
}
```

You may find the file [here](https://github.com/egovernments/DIGIT-Dev/blob/master/municipal-services/property-services/src/main/java/org/egov/pt/util/EncryptionDecryptionUtil.java) in the repo.

**UnmaskingUtil.java:**

UnmaskingUtil.java file helps in extracting the plain data of the owner from the user service.

For reference follow the below code snippet

```
package org.egov.pt.util;

import java.util.ArrayList;
import java.util.HashSet;
import java.util.List;
import java.util.Set;

import org.egov.common.contract.request.PlainAccessRequest;
import org.egov.common.contract.request.RequestInfo;
import org.egov.pt.models.Address;
import org.egov.pt.models.OwnerInfo;
import org.egov.pt.models.Property;
import org.egov.pt.models.PropertyCriteria;
import org.egov.pt.models.user.UserDetailResponse;
import org.egov.pt.models.user.UserSearchRequest;
import org.egov.pt.service.PropertyService;
import org.egov.pt.service.UserService;
import org.egov.pt.validator.PropertyValidator;
import org.egov.pt.web.contracts.PropertyRequest;
import org.egov.tracer.model.CustomException;
import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.stereotype.Component;
import org.springframework.util.CollectionUtils;
import org.springframework.util.StringUtils;

@Component
public class UnmaskingUtil {
	
	private static List<String> ownerPlainRequestFieldsList;
	

	@Autowired
	private UserService userService;
	
	@Autowired 
	private PropertyService service;
	
	@Autowired
	private PropertyValidator validator;
	
	public Property getPropertyUnmasked(PropertyRequest request) {
		
		Property propertyFromRequest = request.getProperty(); 
        PropertyCriteria criteria = validator.getPropertyCriteriaForSearch(request);
        List<Property> propertiesFromSearchResponse = service.searchProperty(criteria, request.getRequestInfo());
		if (CollectionUtils.isEmpty(propertiesFromSearchResponse)) {
			throw new CustomException("EG_PT_PROPERTY_NOT_FOUND", "The property to be updated does not exist in the system");
		}
		Property propertyFromSearch = propertiesFromSearchResponse.get(0);
		
		Address addressFromRequest = propertyFromRequest.getAddress();
		
		if (null != addressFromRequest.getDoorNo() && addressFromRequest.getDoorNo().contains("*"))
			addressFromRequest.setDoorNo(propertyFromSearch.getAddress().getDoorNo());
		if (null != addressFromRequest.getStreet() && addressFromRequest.getStreet().contains("*"))
			addressFromRequest.setStreet(propertyFromSearch.getAddress().getStreet());
		if (null != addressFromRequest.getLandmark() && addressFromRequest.getLandmark().contains("*"))
			addressFromRequest.setLandmark(propertyFromSearch.getAddress().getLandmark());
		
		
		getOwnerDetailsUnmasked(request.getProperty(), request.getRequestInfo());
		return propertyFromSearch;
	}
	
	public void getOwnerDetailsUnmasked (Property property, RequestInfo requestInfo) {
		
		PlainAccessRequest apiPlainAccessRequest = requestInfo.getPlainAccessRequest();
		
		List<String> plainRequestFieldsList = getAllFieldsPlainAccessList();
		PlainAccessRequest plainAccessRequest = PlainAccessRequest.builder()
				.plainRequestFields(plainRequestFieldsList)
				.build();
		requestInfo.setPlainAccessRequest(plainAccessRequest);
		
		UserSearchRequest userSearchRequest = userService.getBaseUserSearchRequest(property.getTenantId(), requestInfo);
		
		Set<String> ownerIds = new HashSet<>();
		
		for (OwnerInfo ownerInfo : property.getOwners()) {
			
			String currentOwnerId = ownerInfo.getUuid();
			if(currentOwnerId == null)
				continue;
			
			/*
			 * once user module is updated to handle masked update 
			 * users will be unmasked on need, currently all. 
			 */
			ownerIds.clear();
			ownerIds.add(currentOwnerId);
			userSearchRequest.setUuid(ownerIds);
			plainAccessRequest.setRecordId(currentOwnerId);

			UserDetailResponse userDetailResponse = userService.getUser(userSearchRequest);

			OwnerInfo unmaskedUser = userDetailResponse.getUser().get(0);
			updateMaskedOwnerInfoWithUnmaskedFields(ownerInfo, unmaskedUser);
			requestInfo.setPlainAccessRequest(apiPlainAccessRequest);
		}

	}

	private void updateMaskedOwnerInfoWithUnmaskedFields(OwnerInfo ownerInfo, OwnerInfo unmaskedUser) {

		if (!StringUtils.isEmpty(ownerInfo.getFatherOrHusbandName()) && ownerInfo.getFatherOrHusbandName().contains("*")) {
			ownerInfo.setFatherOrHusbandName(unmaskedUser.getFatherOrHusbandName());
		}
		if (ownerInfo.getMobileNumber().contains("*")) {
			ownerInfo.setMobileNumber(unmaskedUser.getMobileNumber());
		}
		
		if (ownerInfo.getPermanentAddress() != null 
				&& ownerInfo.getPermanentAddress().contains("*")) {
			ownerInfo.setPermanentAddress(unmaskedUser.getPermanentAddress());
		}
		
		if (ownerInfo.getCorrespondenceAddress() != null 
				&& ownerInfo.getCorrespondenceAddress().contains("*")) {
			ownerInfo.setCorrespondenceAddress(unmaskedUser.getCorrespondenceAddress());
		}
		if (!StringUtils.isEmpty(ownerInfo.getUserName()) && ownerInfo.getUserName().contains("*")) {
			ownerInfo.setUserName(unmaskedUser.getUserName());
		}
		if (!StringUtils.isEmpty(ownerInfo.getName()) &&  ownerInfo.getName().contains("*")) {
			ownerInfo.setName(unmaskedUser.getName());
		}
		if (!StringUtils.isEmpty(ownerInfo.getGender()) && ownerInfo.getGender().contains("*")) {
			ownerInfo.setGender(unmaskedUser.getGender());
		}
	}

	public static List<String> getAllFieldsPlainAccessList() {

		if (ownerPlainRequestFieldsList == null) {
			
			ownerPlainRequestFieldsList = new ArrayList<>();
			ownerPlainRequestFieldsList.add("mobileNumber");
			ownerPlainRequestFieldsList.add("guardian");
			ownerPlainRequestFieldsList.add("fatherOrHusbandName");
			ownerPlainRequestFieldsList.add("correspondenceAddress");
			ownerPlainRequestFieldsList.add("userName");
			ownerPlainRequestFieldsList.add("name");
			ownerPlainRequestFieldsList.add("gender");
		}
		return ownerPlainRequestFieldsList;
	}
}
```

You may find the file [here](https://github.com/egovernments/DIGIT-Dev/blob/master/municipal-services/property-services/src/main/java/org/egov/pt/util/UnmaskingUtil.java) in the repo.

### Important Methods To Be Added In Service <a href="#important-methods-to-be-added-in-service" id="important-methods-to-be-added-in-service"></a>

If you want to get all the PII data in the plain format then in the search request add the search param **“isSearchInternal“** as **“true”**

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
                "street","doorNo","landmark"
            ]
        }
    }
}
```

`plainAccessRequest` contains :

1. `recordId` which will take the uuid of the user as an input for which PII data has to be unmasked, and
2. `plainRequestFields` will take an array of attributes that need to be unmasked. These attributes should comply with the attributes used in the Mdms SecurityPolicy.json’s models created.

### Encryption of Old Data In The DB <a href="#encryption-of-old-data-in-the-db" id="encryption-of-old-data-in-the-db"></a>

Before using the privacy feature in any environment the encryption of existing data in the dB should be done.

An API for the same is written in the service and needs to be triggered by port-forwarding the respective service pod.

The data encryption API uses the existing plainSearch method and the encryption shall take place _**tenantId-wise.**_ If tenantId is not specified then all the tenants are picked from the MDMS repository and the encryption happens for all the tenants. However, if the tenantId is specified, then the encryption happens only for that tenantId.

The following method is added to execute the oldDataEncryption

**In PropertyController.java**

```
/**
     * Encrypts existing property records
     *
     * @param requestInfoWrapper RequestInfoWrapper
     * @param propertyCriteria PropertyCriteria
     * @return list of updated encrypted data
     */
    /* To be executed only once */
    @RequestMapping(value = "/_encryptOldData", method = RequestMethod.POST)
    public ResponseEntity<PropertyResponse> encryptOldData(@Valid @RequestBody RequestInfoWrapper requestInfoWrapper,
                                                         @Valid @ModelAttribute PropertyCriteria propertyCriteria) {
        propertyCriteria.setIsRequestForOldDataEncryption(Boolean.TRUE);
        List<Property> properties = propertyEncryptionService.updateOldData(propertyCriteria, requestInfoWrapper.getRequestInfo());
        PropertyResponse response = PropertyResponse.builder().properties(properties).responseInfo(
                        responseInfoFactory.createResponseInfoFromRequestInfo(requestInfoWrapper.getRequestInfo(), true))
                .build();
        return new ResponseEntity<>(response, HttpStatus.OK);
    }
```

**In PropertyEncryptionService.java**\
This service is solely for old data encryption and can be referred from here:\
[PropertyEncryptionService.java](https://github.com/egovernments/DIGIT-Dev/blob/master/municipal-services/property-services/src/main/java/org/egov/pt/service/PropertyEncryptionService.java)

A _**new persister file**_ needs to be added for keeping track of the progress of oldDataEncryption.\
Refer to this [pt-enc-audit-persister.yml](https://github.com/egovernments/configs/blob/UAT/egov-persister/pt-enc-audit-persister.yml) for the same.

Here is the Postman collection for all _**property, water**_ and _**sewerage**_ services for _**old Data encryption**_ :\
[https://www.getpostman.com/collections/b3858ec2020462a6407d](https://www.getpostman.com/collections/b3858ec2020462a6407d)

## **Re-indexing Old Data In Base Indexes**

&#x20;There is **no need** to re-indexing the base indexes(_**viz.**_ property-services) once the API for old data encryption is executed as this will happen during the API execution itself.\
For any new data getting created, the new data will get saved in the encrypted format only in the indexes.

When talking about privacy changes, we would need 2 additional indexes to be added.\
both of them would be the copy of existing indexes.\
1\. A fuzzy index: Copy of index config under existing save topic

_Reference:_ [<img src="https://github.com/fluidicon.png" alt="" data-size="line">\[UM-5579\]- Added property fuzzy search topic and index in property-se… · egovernments/configs@5399adb](https://github.com/egovernments/configs/commit/5399adb0afae6e646550ca5c4c269632b6aac630)

2\. An index for Old data encryption: Copy of index config under existing update topic\
_Reference:_ [<img src="https://github.com/fluidicon.png" alt="" data-size="line">Enc-Property indexer and persister changes by hinamakhija-eGov · Pull Request #2516 · egovernments/configs](https://github.com/egovernments/configs/pull/2516)

### **Enabling / Disabling Privacy**

To enable or disable decryption in privacy, we need to make changes to only the privacy variable present in the environment file in DevOps. For enabling, its value should be “true” else “false”.

For property-services:

```
property-decryption-abac-enabled: "true"
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

For detailed steps to configure the above changes refer to the document: [Detailed Steps to configure privacy in Property module](https://digit-discuss.atlassian.net/l/cp/trPrW1UU).\


