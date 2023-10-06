# Survey Service Configuration

## Overview <a href="#overview" id="overview"></a>

Surveys are an important way to close the feedback loop on the services that are delivered by ULBs. Without proper surveys, ULB employees will never know how happy the citizens are, about the services they consume and what the areas of improvement are.

The surveys section will be used by ULB employees to create citizen surveys to make better-informed decisions while issuing new policies/ feedback on existing services.

## Pre-requisites <a href="#pre-requisites" id="pre-requisites"></a>

1. Prior knowledge of Java/J2EE.
2. Prior knowledge of SpringBoot.
3. Prior knowledge of PostgresSQL.
4. Prior knowledge of REST APIs and related concepts like path parameters, headers, JSON etc.
5. Prior knowledge of JSONQuery in Postgres. (Similar to PostgresSQL with a few aggregate functions.)

## Key Functionalities  <a href="#key-functionalities-and-configurations" id="key-functionalities-and-configurations"></a>

This service allows -

* Employees - to create, edit, delete surveys
* Employees - to share survey results with other employees/citizens
* Citizens - to fill out surveys

Each survey entity will have questions associated with it. Questions can be of -

1. short answer type
2. long answer type&#x20;
3. multiple answers type
4. checkbox answer type
5. date answer type
6. time answer type

## Configuration Details <a href="#key-functionalities-and-configurations" id="key-functionalities-and-configurations"></a>

Survey entities will have a collectCitizenInfo flag associated with them If that flag is set to true, the mobile number and email address of the citizens responding to the survey will be captured. If it is set to false, responding to the survey will be completely anonymous.

Surveys will have a startDate and endDate associated with them. Within that period, those surveys will be shown in the active section. However, in case the survey has been manually marked inactive by the employee during its active period, that survey will be shown under the inactive surveys section. Citizens can look at active survey entities and submit their responses for that survey.

Once a survey is created, it can be searched with the following parameters -&#x20;

1. tenantIds - To search surveys based on multiple ULBs
2. title - To search surveys based on survey names
3. postedBy - To search surveys based on employees who created the survey
4. status - To search surveys based on status&#x20;

Also, if any created survey needs to be updated -

1. Before the survey becomes active, users can edit all the fields.
2. While editing, we can add, delete, and modify questions.
3. Once the survey becomes live user can only change&#x20;

a. Survey Description

b.End date and time of the survey

In case of deletion of a survey, the survey will be soft deleted i.e. the ‘active’ boolean field will be set to false and it will not appear in search results.

{% hint style="info" %}
NOTE:\
1\. In search of a survey we display only questions which are in active status\
2\. While editing, if a question of a survey is deleted, then we mark the question as inactive in db&#x20;
{% endhint %}

### Swagger Documentation

The link to the swagger documentation can be found below -

[Survey Service Contract](https://editor.swagger.io/?url=https://raw.githubusercontent.com/egovernments/DIGIT-OSS/master/core-services/docs/survey-service.yml)

[https://github.com/egovernments/DIGIT-Dev/blob/master/core-services/egov-survey-services/src/main/resources/egov-survey-service.yml](https://github.com/egovernments/DIGIT-Dev/blob/master/core-services/egov-survey-services/src/main/resources/egov-survey-service.yml)

## API Details <a href="#api-details" id="api-details"></a>

APIs for interacting with survey service can be found in this collection

[https://api.postman.com/collections/24408626-ba14832c-38e0-42db-af88-598d8fedb2ff?access\_key=PMAT-01GR8DH6JWKMPK2FNT1WH62T1T](https://api.postman.com/collections/24408626-ba14832c-38e0-42db-af88-598d8fedb2ff?access\_key=PMAT-01GR8DH6JWKMPK2FNT1WH62T1T)

**Survey persister**

{% code lineNumbers="true" %}
```
serviceMaps:
  serviceName: egov-survey-services
  mappings:
    - version: 1.0
      description: Persists surveys in eg_ss_survey table
      fromTopic: save-ss-survey
      isTransaction: true
      queryMaps:
        - query: INSERT INTO eg_ss_survey( uuid,tenantid,title,description,status,postedby,startDate,endDate,collectCitizenInfo,active,createdby,lastmodifiedby,createdtime,lastmodifiedtime) VALUES (?,?,?,?, ?, ?, ?, ?, ?, ?, ?, ?, ?, ?);
          basePath: SurveyEntity
          jsonMaps:
            - jsonPath: $.SurveyEntity.uuid

            - jsonPath: $.SurveyEntity.tenantId

            - jsonPath: $.SurveyEntity.title

            - jsonPath: $.SurveyEntity.description

            - jsonPath: $.SurveyEntity.status

            - jsonPath: $.SurveyEntity.postedBy

            - jsonPath: $.SurveyEntity.startDate

            - jsonPath: $.SurveyEntity.endDate

            - jsonPath: $.SurveyEntity.collectCitizenInfo

            - jsonPath: $.SurveyEntity.active

            - jsonPath: $.SurveyEntity.auditDetails.createdBy

            - jsonPath: $.SurveyEntity.auditDetails.lastModifiedBy

            - jsonPath: $.SurveyEntity.auditDetails.createdTime

            - jsonPath: $.SurveyEntity.auditDetails.lastModifiedTime

        - query: INSERT INTO eg_ss_question( uuid,surveyid,questionstatement,options,status,type,required,createdby,lastmodifiedby,createdtime,lastmodifiedtime,qorder) VALUES (?,?,?,?,?,?,?,?,?,?,?,?);
          basePath: SurveyEntity.questions.*
          jsonMaps:
            - jsonPath: $.SurveyEntity.questions.*.uuid

            - jsonPath: $.SurveyEntity.questions.*.surveyId

            - jsonPath: $.SurveyEntity.questions.*.questionStatement

            - jsonPath: $.SurveyEntity.questions.*.options
              type: ARRAY
              dbType: STRING

            - jsonPath: $.SurveyEntity.questions.*.status

            - jsonPath: $.SurveyEntity.questions.*.type

            - jsonPath: $.SurveyEntity.questions.*.required

            - jsonPath: $.SurveyEntity.questions.*.auditDetails.createdBy

            - jsonPath: $.SurveyEntity.questions.*.auditDetails.lastModifiedBy

            - jsonPath: $.SurveyEntity.questions.*.auditDetails.createdTime

            - jsonPath: $.SurveyEntity.questions.*.auditDetails.lastModifiedTime
            
            - jsonPath: $.SurveyEntity.questions.*.qorder

    - version: 1.0
      description: Persists answers in eg_ss_answer table
      fromTopic: save-ss-answer
      isTransaction: true
      queryMaps:
        - query: INSERT INTO eg_ss_answer( uuid,questionid,surveyid,answer,citizenid,mobilenumber,emailid,createdby,lastmodifiedby,createdtime,lastmodifiedtime) VALUES (?,?,?,?,?,?,?,?,?,?,?);
          basePath: AnswerEntity.answers.*
          jsonMaps:
            - jsonPath: $.AnswerEntity.answers.*.uuid

            - jsonPath: $.AnswerEntity.answers.*.questionId

            - jsonPath: $.AnswerEntity.surveyId

            - jsonPath: $.AnswerEntity.answers.*.answer
              type: ARRAY
              dbType: STRING

            - jsonPath: $.AnswerEntity.answers.*.citizenId

            - jsonPath: $.AnswerEntity.answers.*.mobileNumber

            - jsonPath: $.AnswerEntity.answers.*.emailId

            - jsonPath: $.AnswerEntity.answers.*.auditDetails.createdBy

            - jsonPath: $.AnswerEntity.answers.*.auditDetails.lastModifiedBy

            - jsonPath: $.AnswerEntity.answers.*.auditDetails.createdTime

            - jsonPath: $.AnswerEntity.answers.*.auditDetails.lastModifiedTime

    - version: 1.0
      description: Updates survey in tables
      fromTopic: update-ss-survey
      isTransaction: true
      queryMaps:
        - query: UPDATE eg_ss_survey SET tenantid=?, title=?, description=?, status=?, postedBy=?, startDate = ?, endDate = ?, collectCitizenInfo = ?, lastmodifiedby=?, lastmodifiedtime=? WHERE uuid=?;
          basePath: SurveyEntity
          jsonMaps:
            - jsonPath: $.SurveyEntity.tenantId

            - jsonPath: $.SurveyEntity.title

            - jsonPath: $.SurveyEntity.description

            - jsonPath: $.SurveyEntity.status

            - jsonPath: $.SurveyEntity.postedBy

            - jsonPath: $.SurveyEntity.startDate

            - jsonPath: $.SurveyEntity.endDate

            - jsonPath: $.SurveyEntity.collectCitizenInfo

            - jsonPath: $.SurveyEntity.auditDetails.lastModifiedBy

            - jsonPath: $.SurveyEntity.auditDetails.lastModifiedTime

            - jsonPath: $.SurveyEntity.uuid

        - query: UPDATE eg_ss_question SET questionstatement = ?, options = ?, status = ?, type = ?, required = ?, lastmodifiedby = ?, lastmodifiedtime = ? WHERE uuid = ?;
          basePath: SurveyEntity.questions.*
          jsonMaps:

            - jsonPath: $.SurveyEntity.questions.*.questionStatement

            - jsonPath: $.SurveyEntity.questions.*.options
              type: ARRAY
              dbType: STRING

            - jsonPath: $.SurveyEntity.questions.*.status

            - jsonPath: $.SurveyEntity.questions.*.type

            - jsonPath: $.SurveyEntity.questions.*.required

            - jsonPath: $.SurveyEntity.questions.*.auditDetails.lastModifiedBy

            - jsonPath: $.SurveyEntity.questions.*.auditDetails.lastModifiedTime

            - jsonPath: $.SurveyEntity.questions.*.uuid

        - query: INSERT INTO eg_ss_question( uuid,surveyid,questionstatement,options,status,type,required,createdby,lastmodifiedby,createdtime,lastmodifiedtime,qorder) VALUES (?,?,?,?,?,?,?,?,?,?,?,?);
          basePath: SurveyEntity.insertQuestionsForUpdate.*
          jsonMaps:
          - jsonPath: $.SurveyEntity.insertQuestionsForUpdate.*.uuid

          - jsonPath: $.SurveyEntity.insertQuestionsForUpdate.*.surveyId

          - jsonPath: $.SurveyEntity.insertQuestionsForUpdate.*.questionStatement

          - jsonPath: $.SurveyEntity.insertQuestionsForUpdate.*.options
            type: ARRAY
            dbType: STRING

          - jsonPath: $.SurveyEntity.insertQuestionsForUpdate.*.status

          - jsonPath: $.SurveyEntity.insertQuestionsForUpdate.*.type

          - jsonPath: $.SurveyEntity.insertQuestionsForUpdate.*.required

          - jsonPath: $.SurveyEntity.insertQuestionsForUpdate.*.auditDetails.createdBy

          - jsonPath: $.SurveyEntity.insertQuestionsForUpdate.*.auditDetails.lastModifiedBy

          - jsonPath: $.SurveyEntity.insertQuestionsForUpdate.*.auditDetails.createdTime

          - jsonPath: $.SurveyEntity.insertQuestionsForUpdate.*.auditDetails.lastModifiedTime

          - jsonPath: $.SurveyEntity.insertQuestionsForUpdate.*.qorder

    - version: 1.0
      description: Deletes survey in tables
      fromTopic: delete-ss-survey
      isTransaction: true
      queryMaps:
        - query: UPDATE eg_ss_survey SET active=? WHERE uuid=?;
          basePath: SurveyEntity
          jsonMaps:
            - jsonPath: $.SurveyEntity.active

            - jsonPath: $.SurveyEntity.uuid
```
{% endcode %}
