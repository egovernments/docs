---
description: Service Request Module Configuration
---

# Service Request

## Overview

The service request functionality empowers users to define and then create services based on predefined service definitions. These service definitions can be in the form of surveys or checklists that users can refer to. Subsequently, a service created against a service definition can either serve as a response to a survey or represent a completed checklist.

## Pre-requisites <a href="#pre-requisites" id="pre-requisites"></a>

1. Prior knowledge of Java/J2EE.
2. Prior knowledge of SpringBoot.
3. Prior knowledge of PostgreSQL.
4. Prior knowledge of REST APIs and related concepts like path parameters, headers, JSON etc.

## Key Functionalities

Users can -

1. Create and search service definitions
2. Create and search services

## API Details

1. /service-request/service/definition/v1/\_create - Include the RequestInfo and ServiceDefinition within the request body. The ServiceDefinition encapsulates all the essential parameters linked to the creation of the service definition.
2. /service-request/service/definition/v1/\_search - Allows searching of existing service definitions. Takes RequestInfo, ServiceDefinitionCriteria and Pagination objects in the request body.
3. /service-request/service/v1/\_create - Takes RequestInfo and Service in the request body. Service has all the parameters related to the service being created against a particular ServiceDefinition.
4. /service-request/service/v1/\_search - Allows searching of existing services created against service definitions. Takes RequestInfo, ServiceCriteria and Pagination objects in the request body.

Detailed API payloads for interacting with Service Request for all four endpoints are available in the following collection - [Service Request Collection](https://api.postman.com/collections/12892142-f7bf3d00-6eed-4efc-8cbe-66dd22833f8e?access\_key=PMAT-01GST3SNZDFX2CZ5GW0A69M91K)

## Swagger Documentation

The link to the swagger documentation can be found here - [Service Request Contract](https://editor.swagger.io/?url=https://raw.githubusercontent.com/egovernments/DIGIT-OSS/health-checklist-final/core-services/service-request/src/main/resources/service-request-contract.yaml)
