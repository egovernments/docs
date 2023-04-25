# Birth & Death Service Configuration

**Objective:** This page provides the configuration details for the birth and death service.&#x20;

The module features enable users to

1. Register the birth and death information of the citizen into the system.
2. Correct any wrong information which is captured earlier.
3. Enable citizens to search and download their respective certificates.

## **Technical Details**

### **Birth Certificate - New Registration**

Both birth and death forms are quite similar.&#x20;

MDMS details for hospitals configured at the city level.

```
{
    "tenantId": "pb.amritsar",
    "moduleDetails": [
        {
            "moduleName": "birth-death-service",
            "masterDetails": [
                {
                    "name": "hospitalList"
                }
            ]
        }
    ]
}
```

Birth registration file link: frontend/mono-ui/web/rainmaker/dev-packages/egov-bnd-dev/src/ui-config/screens/specs/birth-employee/newRegistration.js

Death registration file link: frontend/mono-ui/web/rainmaker/dev-packages/egov-bnd-dev/src/ui-config/screens/specs/death-employee/newRegistration.js

![](<../../../../.gitbook/assets/image (183).png>)

Filename: newRegistrationFooter.js

It contains the logic related to the validation of the form, submission, and API call details.

**APIs** **used -**

Birth - Create and Update API

* <mark style="background-color:blue;">birth-death-services/common/saveBirthImport</mark>
* <mark style="background-color:blue;">birth-death-services/common/updateBirthImport</mark>

Death - Create and Update API

* <mark style="background-color:blue;">birth-death-services/common/saveDeathImport</mark>
* <mark style="background-color:blue;">birth-death-services/common/updateDeathImport</mark>

**Search Certificate**

The search certificate is the same for both employees and citizens.

The employee has a view option. Whereas citizens can download it for free for the first time. Second-time downloads requires the citizens to Pay & Download.&#x20;

![](<../../../../.gitbook/assets/image (281).png>)

`BIRTH_APPLICATION_CREATOR` & `DEATH_APPLICATION_CREATOR` - the Birth Registration button is enabled on the search screen for this role.

Citizen View

![](<../../../../.gitbook/assets/image (138).png>)

API Details

<mark style="background-color:blue;">`birth-death-services/death/_search`</mark>

<mark style="background-color:blue;">`birth-death-services/birth/_search`</mark>

File Details -&#x20;

```
frontend/mono-ui/web/rainmaker/dev-packages/egov-bnd-dev/src/ui-config/screens/specs/birth-common/getCertificate.js
```

```
frontend/mono-ui/web/rainmaker/dev-packages/egov-bnd-dev/src/ui-config/screens/specs/death-common/getCertificate.js
```

Clicking on the **Pay and download** button **-** Generates demand for making a payment and after completing the payment it downloads the certificate automatically.

Auto-download configuration file&#x20;

```
frontend/mono-ui/web/rainmaker/dev-packages/egov-common-dev/src/ui-config/screens/specs/egov-common/acknowledgement.js
```

`postPaymentSuccess` the method enables the auto-download.\
\
Clicking on the **Download** button - searches for the filestore id and downloads the file.

* birth-death-services/birth/\_getfilestoreid?tenantId=\{{tenantid\}}\&consumerCode=\{{consumercode\}}
* birth-death-services/death/\_getfilestoreid?tenantId=\{{tenantid\}}\&consumerCode=\{{consumercode\}}

**My Applications**

* Citizen

Citizens can download certificates and receipts from the My Applications screen.

![](<../../../../.gitbook/assets/image (137).png>)

Download receipt MDMS configuration to fetch the Birth and death in business service dropdown file link: [<img src="https://github.com/fluidicon.png" alt="" data-size="line">RAIN-6838 :: BND Download receipt config updated typt to adhoc · egovernments/egov-mdms-data@bc9efec](https://github.com/egovernments/egov-mdms-data/commit/bc9efec16a8c61e341e24be6a387939e36937675)

**How It Works Section**

The How It Works section shows the configured pdf to help citizens download certificates. Similarly in other environments, the same file is added to the Asset folder.

Also in the Global config file\
[https://qa.digit.org/egov-qa-assets/globalConfigs.js](https://qa.digit.org/egov-qa-assets/globalConfigs.js)\
`var assetS3Bucket = 'egov-qa-assets';`\
Refer to the [Citizen User Manual ](../../../../products/modules/birth-and-death/birth-and-death-user-manual/birth-and-death-citizen-user-manual.md)for details.

**Localization Module -** `rainmaker-bnd`

## **Role Action Mapping**

| **API**                                       | **ROLES**                                                                   | **ACTION ID** |
| --------------------------------------------- | --------------------------------------------------------------------------- | ------------- |
| `egov-mdms-service/v1/_search`                |                                                                             | `954`         |
| `birth-death-services/death/_search`          | `BND_CEMP`, `CITIZEN`,`DEATH_APPLICATION_VIEWER`,`DEATH_APPLICATION_EDITOR` |               |
| `birth-death-services/birth/_search`          | `BND_CEMP`, `CITIZEN`,`BIRTH_APPLICATION_VIEWER`,`BIRTH_APPLICATION_EDITOR` |               |
| birth-death-services/birth/\_getfilestoreid   | `BND_CEMP`, `CITIZEN`                                                       |               |
| birth-death-services/death/\_getfilestoreid   | `BND_CEMP`, `CITIZEN`                                                       |               |
| birth-death-services/common/saveDeathImport   | `BND_CEMP`,`DEATH_APPLICATION_CREATOR`                                      |               |
| birth-death-services/common/updateDeathImport | `BND_CEMP`,`DEATH_APPLICATION_EDITOR`                                       |               |
| birth-death-services/common/saveBirthImport   | `BND_CEMP`,`BIRTH_APPLICATION_CREATOR`                                      |               |
| birth-death-services/common/updateBirthImport | `BND_CEMP`,`BIRTH_APPLICATION_EDITOR`                                       |               |
