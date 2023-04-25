---
description: About and Purpose page for National Dashboard Enhancement
---

# National Dashboard - About & FAQs

## Overview - About Page

An about the dashboard page that describes the purpose of the dashboard as well as the source of the data is required to be built as per the feedback received from the demos.

**Web URL:-**[![](https://cdn.jsdelivr.net/npm/@egovernments/digit-ui-css/img/browser-icon.png)**mSeva**](https://qa.digit.org/digit-ui/employee/dss/national-about)&#x20;

The file location in Digit-Dev:- ../modules/dss/src/pages/About.js

The file location in egov-mdms-data:- ../../pb/dss-dashboard/About.json

code

```
{
                        "titleHeader": "DSS_QUES_WHAT_CAN_DASBOARD_VIEWER_SEE_N_DO",
                        "define": [
                            "DSS_ANS_WHAT_CAN_DASBOARD_VIEWER_SEE_N_DO"
                        ],
                        "subdefine": [
                            "FOLLOWING_VIEWER_DO_ON_DASHBOARD"
                        ],
                        "definePoints": [
                            {
                                "point": "PERFORMANCE_METRICS"
                            },
                            {
                                "point": "RESPECTIVE_STATE'S_PERFORMANCE"
                            },
                            {
                                "point": "PERFORMANCES_IN_FORM_VISUALIZATIONS"
                            },
                            {
                                "point": "SERVICE-WISE_PERFORMANCE"
                            },
                            {
                                "point": "YEAR_PERFORMANCE"
                            }
                        ],
                        "subdefinePoints": [
                            {
                                "point": "STUDY_THE_PERFORMANCES"
                            },
                            {
                                "point": "SEE_COMPARISONS_OF_INTER-STATE"
                            },
                            {
                                "point": "SEE_COMPARISON_ON_YEAR-WISE"
                            },
                            {
                                "point": "DOWNLOAD_THE_DATASET"
                            },
                            {
                                "point": "SHARE_DATA_ANALYTICS"
                            }
                        ]
                    }
```

**OUTPUT**

<figure><img src="../../../../../.gitbook/assets/image (464).png" alt=""><figcaption></figcaption></figure>

## **Add Content**

To add a question we need to mention `titleHeader`

To add the first point we need to mention `define`

To add the first sub-points we need to mention `definePoints`

To add the second point we need to mention `subdefine`

To add the second sub-points we need to mention `subdefinePoints`

## **Remove Content**

If we need to remove the content we need to delete it according `titleHeader,define,definePoints, subdefine`, `subdefinePoints`

<figure><img src="../../../../../.gitbook/assets/image (353).png" alt=""><figcaption></figcaption></figure>

## **Overview - FAQ Page**&#x20;

To enhance the dashboard and make it more user-friendly, an FAQ page is to be developed so that users can access it from any page for any queries that they may have regarding any acronyms or how to navigate.

**Web URL:-**[![](https://cdn.jsdelivr.net/npm/@egovernments/digit-ui-css/img/browser-icon.png)**mSeva**](https://qa.digit.org/digit-ui/employee/dss/national-faqs)\
\
**The File location in Digit-Dev:- ../dss/src/pages/FAQs**

**The File location in egov-mdms-data:- ../../pb/dss-dashboard/FAQs.json**

**code**

```
{
                        "question": "QUES_THREE_HOW_CAN_I_VIEW_VALUES_GRAPH",
                        "answer": [
                            {
                                "ans": "FOR_PIE_CHARTS"
                            },
                            {
                                "point": "HOVER_OVER_THE_INDIVIDUAL_SLICES"
                            }
                        ],
                        "subAnswer" : [
                          {
                            "ans": "FOR_LINE/BAR_GRAPHS"
                        },
                        {
                            "point": "HOVER_OVER_HE_INE/BAR"
                        }
                        ]
                      }
```

**OUTPUT**

<figure><img src="../../../../../.gitbook/assets/image (413).png" alt=""><figcaption></figcaption></figure>

## **Add Content**

To add a question we need to mention `question`

To add the First point we need to mention `answer, ans`

To add the First sub-points we need to mention `answer, point`

To add the Second point we need to mention `subAnswer, ans`

To add the Second sub-points we need to mention `subAnswer, point`

## **Remove Content**

If we need to remove the content we need to delete it according `question, answer, subAnswer, ans, point`

<figure><img src="../../../../../.gitbook/assets/image (469).png" alt=""><figcaption></figcaption></figure>

#### roleactions.json:- path:- ../../pb/ACCESSCONTROL-ACTIONS-TEST/actions-test.json <a href="#roleactions.json-hardbreak-path-..-..-pb-accesscontrol-actions-test-actions-test.json-hardbreak" id="roleactions.json-hardbreak-path-..-..-pb-accesscontrol-actions-test-actions-test.json-hardbreak"></a>

```
   {
      "rolecode": "EMPLOYEE",
      "actionid": 2373,
      "actioncode": "",
      "tenantId": "pb"
    },
    {
      "rolecode": "EMPLOYEE",
      "actionid": 2374,
      "actioncode": "",
      "tenantId": "pb"
    }
```

#### _**actions-test.json:-**_ **path:- ../../../ACCESSCONTROL-ACTIONS-TEST/actions-test.json** <a href="#hardbreak-actions-test.json-hardbreak-path-..-..-..-accesscontrol-actions-test-actions-test.json-har" id="hardbreak-actions-test.json-hardbreak-path-..-..-..-accesscontrol-actions-test-actions-test.json-har"></a>

```
{
      "id": 2373,
      "name": "ABOUT DASHBOARD",
      "url": "url",
      "displayName": "About Dashboard",
      "orderNumber": 11,
      "parentModule": "ndss-dashboard",
      "enabled": true,
      "serviceCode": "NDSS",
      "code": "null",
      "path": "NatDashboard.About",
      "navigationURL": "/digit-ui/employee/dss/national-about",
      "leftIcon": "places:business-center",
      "rightIcon": ""
    },
    {
      "id": 2374,
      "name": "FAQS",
      "url": "url",
      "displayName": "FAQs",
      "orderNumber": 12,
      "parentModule": "ndss-dashboard",
      "enabled": true,
      "serviceCode": "NDSS",
      "code": "null",
      "path": "NatDashboard.FAQs",
      "navigationURL": "/digit-ui/employee/dss/national-faqs",
      "leftIcon": "places:business-center",
      "rightIcon": ""
    }
```

