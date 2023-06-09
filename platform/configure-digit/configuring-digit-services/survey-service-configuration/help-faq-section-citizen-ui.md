# Help/FAQ Section - Citizen UI

**Objective:** To enable citizens to access contextual help and information with links to various features such as Pay Via WhatsApp.&#x20;

## Help Section <a href="#objective" id="objective"></a>

### Workflow Details <a href="#objective" id="objective"></a>

The feature provides users with tenant-specific data.&#x20;

![](<../../../../.gitbook/assets/image (328).png>)

### Technical Implementation Details <a href="#objective" id="objective"></a>

#### **Dynamic Data**

The dynamic data are displayed in range cells. We get the dynamic data from the particular service APIs. These APIs enable open search so that citizen users can check these data even if they are not logged in.

#### **MDMS**

Static data like Helpline, Service Center, Pay Via WhatsApp link and validity of an application is fetched from the MDMS config.

If we do not want any of the cards to be displayed, this can be removed from MDMS for the particular service.

```
 "MdmsCriteria": {
        "tenantId": "pb",
        "moduleDetails": [
            {
                "moduleName": "common-masters",
                "masterDetails": [
                    {
                        "name": "StaticData"
                    }
                ]
            }
        ]
    }
```

#### Add links to FAQs and How it works for each module: <a href="#add-link-to-faqs-and-how-it-works-for-each-module" id="add-link-to-faqs-and-how-it-works-for-each-module"></a>

We can add FAQs and the How it works links in the MDMS for each service.

**Navigation URL for FAQs: `"/digit-ui/citizen/{module}-faq"`**&#x20;

(Replace `{module}` with moduleCode. For Ex: `"/digit-ui/citizen/pt-faq"`)

**Navigation URL for How it works : `"/digit-ui/citizen/{module}-how-it-works"`**&#x20;

(Replace `{module}` with moduleCode. For Ex: `"/digit-ui/citizen/pt-how-it-works"`)

![](<../../../../.gitbook/assets/image (331).png>)

**Object reference:**

`{"id": 2331,`

`"name": "PT_FAQ_S",`

`"url": "digit-ui-card",`

`"displayName": "FAQs",`

`"orderNumber": 1,`

`"parentModule": "PT",`

`"enabled": true,`

`"navigationURL": "/digit-ui/citizen/pt-faq",`

`"leftIcon": "propertyIcon",`

`"sidebar": "digit-ui-links",`

`"sidebarURL": "/digit-ui/citizen/pt-home" }`

## **FAQs** <a href="#faqs" id="faqs"></a>

### **Workflow Details**

Users can check for frequently asked / common questions on this page.

We are using a common screen for all module FAQs. Based on the module code, the FAQs are rendered from MDMS.

![](<../../../../.gitbook/assets/image (527).png>)

### Technical Implementation Details

**Add new FAQs to the list:** We can add new FAQs to the list by adding a new object in the MDMS config for the respective service.

**Object reference:**

`"TL" : {`

`"faqs": [{`

`"question": "TL_FAQ_QUES_ONE",`

`"answer": "TL_FAQ_ANS_ONE"}`

`]}`

#### **MDMS**

FAQs are added for each service from MDMS Config. More FAQs can be added in the MDMS and those will be shown in the UI.

```
 "MdmsCriteria": {
        "tenantId": "pb",
        "moduleDetails": [
            {
                "moduleName": "common-masters",
                "masterDetails": [
                    {
                        "name": "faqs"
                    }
                ]
            }
        ]
    }
```

## **How It Works Section**

### **Workflow Details**

Users can check what they can do or how they can get the benefits of a particular service.

A common screen is used for all the modules in the How it works section. Based on the module code, the cards are rendered from MDMS.

**Add a new Card to the list:** We can add a new Card to the list by adding a new object in the MDMS config for the respective service.

On Language change, the link to the videos also changes.

![](<../../../../.gitbook/assets/image (542).png>)

### Technical Implementation Details

**Object reference:**

`{"moduleCode" : "PT",`

`"videosJson": [{`

`"headerLabel": "ADD_PROPERTY",`

`"description": "ADD_PROPERTY_VIDEO_DESC",`

`"en_IN": "http://media.w3.org/2010/05/sintel/trailer.mp4",`

`"hi_IN": "http://media.w3.org/2010/05/sintel/trailer.mp4"},`

`"pdfHeader": "CITIZEN_CHARTER_DOCUMENT",`

`"pdfDesc": "CITIZEN_CHARTER_DOC_DESC"}`

#### **MDMS**

How it works properties and video links are added for each service from MDMS Config.

```
 "MdmsCriteria": {
        "tenantId": "pb",
        "moduleDetails": [
            {
                "moduleName": "common-masters",
                "masterDetails": [
                    {
                        "name": "howItWorks"
                    }
                ]
            }
        ]
    }
```

### **API Calls To Fetch Dynamic Data**

<table data-header-hidden><thead><tr><th width="76"></th><th width="103"></th><th></th><th></th><th></th></tr></thead><tbody><tr><td></td><td><strong>Service</strong></td><td><strong>Navigation Screen URL</strong></td><td><strong>API</strong></td><td><strong>Payload Params</strong></td></tr><tr><td>1</td><td>PT</td><td><code>digit-ui/citizen/pt-home</code></td><td><code>property-services/property/_search</code></td><td><code>{</code><br><code>tenantId : ""</code><br><code>fromDate :</code><br><code>toDate :</code><br><code>status : "ACTIVE"</code><br><code>}</code></td></tr><tr><td>2</td><td>TL</td><td><code>digit-ui/citizen/tl-home</code></td><td><code>tl-services/v1/_search</code></td><td><p><code>{</code><br><code>tenantId : ""</code></p><p><code>}</code></p></td></tr><tr><td>3</td><td>WS</td><td><code>digit-ui/citizen/ws-home</code></td><td><code>inbox/v1/dss/_search</code></td><td><p><code>{</code></p><p><code>module: "WS"</code></p><p><code>tenantId: ""</code></p><p><code>}</code></p></td></tr><tr><td>4</td><td>PGR</td><td><code>digit-ui/citizen/pgr-home</code></td><td><code>pgr-services/v2/request/_search</code></td><td><p><code>{</code><br><code>tenantId : ""</code></p><p><code>}</code></p></td></tr><tr><td>5</td><td>BPA</td><td><code>digit-ui/citizen/obps-home</code></td><td><code>inbox/v1/dss/_search</code></td><td><p><code>{</code></p><p><code>module: "BPA"</code></p><p><code>tenantId: ""</code></p><p><code>}</code></p></td></tr><tr><td>6</td><td>MCOLLECT</td><td><code>digit-ui/citizen/mcollect-home</code></td><td><code>echallan-services/eChallan/v1/_search</code></td><td><p><code>{</code><br><code>tenantId : ""</code></p><p><code>}</code></p></td></tr></tbody></table>
