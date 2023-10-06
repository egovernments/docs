# Water Disconnection Calculator Service

## Overview <a href="#overview" id="overview"></a>

Water Calculator Service is used for creating meter readings, searching meter readings, updating existing meter readings, calculation of water charges, demand generation, SMS & email notification to ULB officials on-demand generation and estimation of water charge on basis of meter reading for existing water application until the application is disconnected.

## Configuration Details <a href="#configuration-details" id="configuration-details"></a>

### MDMS Configuration <a href="#mdms-configuration" id="mdms-configuration"></a>

There are no additional billing slabs to be configured for water disconnection, the calculation happens with the meter reading if added and uses existing billing slabs.

### **Billing Slabs** <a href="#billing-slabs" id="billing-slabs"></a>

Criteria -

1. connection type
2. building type
3. calculation attribute
4. property usage type

The combination of the above can be used to define the billing slab. Billing Slab is defined in MDMS under ws-services-calculation folder with the [WCBillingSlab](https://github.com/egovernments/mdms-mgramseva/blob/DEV/data/pb/ws-services-calculation/WCBillingSlab.json). The following is the sample slab.

```
{
      "id": "1",
      "buildingType": "RESIDENTIAL",
      "connectionType": "Metered",
      "calculationAttribute": "Water consumption",
      "minimumCharge": 100,
      
      "slabs": [
        {
          "from": 0,
          "to": 10,
          "charge": 2,
          "meterCharge": 50
        },
        {
          "from": 10,
          "to": 20,
          "charge": 2.5,
          "meterCharge": 50
        },
        {
          "from": 20,
          "to": 30,
          "charge": 8,
          "meterCharge": 150
        },
        {
          "from": 30,
          "to": 40,
          "charge": 12,
          "meterCharge": 150
        },
        {
          "from": 40,
          "to": 1000000000,
          "charge": 15,
          "meterCharge": 150
        }
      ]
    },
    {
      "id": "5",
      "buildingType": "RESIDENTIAL",
      "calculationAttribute": "No. of taps",
      "connectionType": "Non Metered",
      
      "minimumCharge": 100,
      "slabs": [
        {
          "from": 0,
          "to": 1000000000,
          "charge": 100
        }
      ]
    },
```

### **Estimation**

For the disconnection application fee, the estimation will return all the related tax heads based on the criteria.

Following are the exemptions and taxes that are calculated:

* Form fee
* Scrutiny fee
* Meter charge (For metered connection)
* Other charges
* Security charges
* Tax and cess

### Water Disconnection Charge & Tax <a href="#water-disconnection-charge-and-tax" id="water-disconnection-charge-and-tax"></a>

The water charge is based on the billing slab, and for water disconnection application charge will be based on the slab and tax based on the master configuration.

**Interest**

Below is a sample of the master data JSON for interest:

```
{
  "tenantId": "pb",
  "moduleName": "ws-services-calculation",
  "Interest": [
    {
      "rate": 5,
      "minAmount": null,
      "applicableAfterDays":0,
      "flatAmount": null,
      "maxAmount": null,
      "fromFY": "2019-20",
      "startingDay": "1/01/2019"
    }
  ]
}
```

**Penalty**

Below is a sample of the master data JSON for penalty -

```
{
  "tenantId": "pb",
  "moduleName": "ws-services-calculation",
  "Penalty": [
    {
      "rate": 10,
      "minAmount": null,
      "applicableAfterDays": 0,
      "flatAmount": null,
      "fromFY": "2019-20",
      "startingDay": "1/01/2019"
    }
  ]
}
```

**Round Off**

If the fraction is greater than equal to 0.5 the number is rounded up else it’s rounded down. eg: 100.4 will be rounded to 100 while 100.6 will be rounded to 101.

### Demand Generation

Whenever \_calculate API is called demand is first searched based on the connection no and the demand from and to period. If demand already exists the same demand is updated else new demand is generated with consumer code as connection no and demand from and to a period equal to the financial year start and end period.

In case of the update, if the tax head estimates change, the difference in amount for that tax head is added as new demand detail. For example, if the initial demand has one demand detail with WATER\_CHARGE equal to 120.

```
"demandDetails": [
                {
                    "id": "77ba1e93-a535-409c-b9d1-a312c409bd45",
                    "demandId": "687c3176-305b-461d-9cec-2fa26a30c88f",
                    "taxHeadMasterCode": "WATER_CHARGE",
                    "taxAmount": 120,
                    "collectionAmount": 120,
                    "additionalDetails": null,
                    "auditDetails": {
                        "createdBy": "04956309-87cd-4526-b4e6-48123abd4f3d",
                        "lastModifiedBy": "04956309-87cd-4526-b4e6-48123abd4f3d",
                        "createdTime": 1583675275873,
                        "lastModifiedTime": 1583675298705
                    },
                    "tenantId": "pb.amritsar"
                }
            ],

```

After updating if the WATER\_CHARGE increases to 150 we add one more demand detail to account for the increased amount. The demand detail will be updated to:

```
"demandDetails": [
                {
                    "id": "77ba1e93-a535-409c-b9d1-a312c409bd45",
                    "demandId": "687c3176-305b-461d-9cec-2fa26a30c88f",
                    "taxHeadMasterCode": "WATER_CHARGE",
                    "taxAmount": 120,
                    "collectionAmount": 0,
                    "additionalDetails": null,
                    "auditDetails": {
                        "createdBy": "04956309-87cd-4526-b4e6-48123abd4f3d",
                        "lastModifiedBy": "04956309-87cd-4526-b4e6-48123abd4f3d",
                        "createdTime": 1583675275873,
                        "lastModifiedTime": 1583675298705
                    },
                    "tenantId": "pb.amritsar"
                },
                {
                    "id": "0d83f4b0-6442-11ea-bc55-0242ac130003 ",
                    "demandId": "687c3176-305b-461d-9cec-2fa26a30c88f",
                    "taxHeadMasterCode": "WATER_CHARGE",
                    "taxAmount": 30,
                    "collectionAmount": 0,
                    "additionalDetails": null,
                    "auditDetails": {
                        "createdBy": "04956309-87cd-4526-b4e6-48123abd4f3d",
                        "lastModifiedBy": "04956309-87cd-4526-b4e6-48123abd4f3d",
                        "createdTime": 1583675275873,
                        "lastModifiedTime": 1583675298705
                    },
                    "tenantId": "pb.amritsar"
                }
            ],

```

The disconnection charges will be the addition of both demand details taxAmount and we can generate demand until the workflow is in `PENDING_FOR_DISCONNECTION_EXECUTION`.

{% hint style="info" %}
**Note :** if there no pending payment when the connection gets approved then the workflow gets updated from `PENDING_APPROVAL_FOR_DISCONNECTION` to `PENDING_FOR_DISCONNECTION_EXECUTION` (it skips payment step in the workflow internally).
{% endhint %}

Here the disconnection charges will be 120+30 = 150

RoundOff is bill based i.e every time bill is generated round off is adjusted so that the payable amount is the whole number. Individual WS\_ROUNDOFF in demand detail can be greater than 0.5 but the sum of all WS\_ROUNDOFF will always be less than 0.5.

**Final water charges calculation**

`Final Water Charges = Last Billing Period Amount * Days (Proposed disconnection date - Last Billing Date) / No. of days in last billing period`

The additional parameter is being sent in the calculation request for the disconnection application.

`disconnectRequest = true` if the request is for `_calculate` API disconnection application.

## API List

| <h4 id="title"><strong>Title</strong> </h4> | **Link**                                                                                                                   |
| ------------------------------------------- | -------------------------------------------------------------------------------------------------------------------------- |
| `/ws-calculator/meterConnection/_create`    | [https://www.getpostman.com/collections/b9a7bde133b0e1fa465f](https://www.getpostman.com/collections/b9a7bde133b0e1fa465f) |
| `/ws-calculator/meterConnection/_search`    | [https://www.getpostman.com/collections/b9a7bde133b0e1fa465f](https://www.getpostman.com/collections/b9a7bde133b0e1fa465f) |
| `/waterCalculator/_calculate`               | [https://www.getpostman.com/collections/c2011085418fe4642728](https://www.getpostman.com/collections/c2011085418fe4642728) |
| `/waterCalculator/_updateDemand`            | [https://www.getpostman.com/collections/b9a7bde133b0e1fa465f](https://www.getpostman.com/collections/b9a7bde133b0e1fa465f) |

_(Note: All the APIs are in the same postman collection therefore the same link is added in each row)_\
