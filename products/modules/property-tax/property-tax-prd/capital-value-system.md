# Capital Value System

## Objective

The objective of this document is to compare the capital value method of property tax assessment with other available methods i.e. annual rental value and unit area value method and evolve the approach to incorporate the capital value system in DIGIT with bare minimum changes.&#x20;

## Source of Information

Uttarakhand  - Draft for capital value system, IGRS system study.

Andhra Pradesh - Draft for capital value system, IGRS system study.

## Abbreviation&#x20;

<table><thead><tr><th width="247">Acronym</th><th>Value</th></tr></thead><tbody><tr><td>ARVM</td><td>Annual Rental Value Method</td></tr><tr><td>UAVM</td><td>Unit Area Value Method</td></tr><tr><td>CVM</td><td>Capital Value Method</td></tr><tr><td>IGRS</td><td>Inspector General of Registration and Stamps</td></tr><tr><td>CV</td><td>Capital Value</td></tr></tbody></table>

## Process Overview

The process of assessment of property tax will remain the same as the UAV method for assessment of property tax.

### Methods of property tax assessment

There are broadly 3 methods which are being used for property tax assessment.

1. Annual Rental Value - In this method tax is calculated on the annual rental value.
2. Unit Area Value  - In this method tax is calculated on annual value.
3. Capital Value - In this method tax is calculated on capital value.

DIGIT already supports the first 2 methods of property tax assessment while the capital value method is relatively new and needs to be incorporated into DIGIT. DIGIT to provide the configuration to define the method of assessment of property tax upfront.

## Masters Data&#x20;

### State Level Masters

DIGIT already supports masters which are required to calculate the annual rental/ annual value. Below given table illustrate which of those are relevant for the capital value method.

<table><thead><tr><th width="205.33333333333331">ARVM/UAVM</th><th width="190">CVM</th><th>Comments</th></tr></thead><tbody><tr><td>Property Type</td><td>Property Type</td><td>It is to define the structure of property as a property would be a vacant land, or a building.</td></tr><tr><td>Property Usage</td><td>Property Usage</td><td>It is upto 3 levels of categorization of usage of a property.</td></tr><tr><td>Floors</td><td>Floors</td><td>It is to define the floors e.g. Ground Floor, First Floor etc.</td></tr><tr><td>Occupancy</td><td>Not Applicable</td><td>Occupancy defines whether a property is occupied by the owner itself or rented out to a tenant.</td></tr><tr><td>Ownership Type</td><td>Ownership Type</td><td>It is upto 2 levels of categorization of ownership of a property.</td></tr><tr><td>Owner’s Category</td><td>Owner’s Category</td><td>It is a category of owner based on which owner would be eligible for certain exemption on property tax. E.g. Freedom Fighter,  Army Personal etc.</td></tr><tr><td>Construction Type</td><td>Construction Type</td><td>It is to define the consumption category of a building. A building would be a Pakka, Kachha or Semi Pakka etc. </td></tr><tr><td>Not Applicable</td><td>Distance From Road</td><td>Distance of the building from the main road plays the role to calculate the capital value. It is applicable to vacant land properties only.</td></tr></tbody></table>

### ULB Specific Masters

#### Boundaries

ULBs are divided into definite smaller units of boundaries to define the unit/ rental rates. In the same way, boundaries are defined by the registration and stamp duty department to define the circle rates. DIGIT has to provide the option to define the boundaries from the registration and stamp duty department.

District → SRO → Block or Segment

<table><thead><tr><th width="180.33333333333331">ARVM/UAVM</th><th width="159">CVM</th><th>Comments</th></tr></thead><tbody><tr><td>ULB</td><td>ULB</td><td>It is to define the ULB with all its attributes like District, Address, Grade etc.</td></tr><tr><td>Ward</td><td>Not Applicable</td><td>All the ULBs in the state have only one boundary hierarchy i.e. Admin Boundary which is used for both Revenue and Administration purposes. Ward is the smallest boundary in this hierarchy and placed at second level just below the ULB boundary itself.</td></tr><tr><td>Locality</td><td>Not Applicable</td><td>Locality or Mohalla is the smallest boudry unit within the ULB which defines the state of the bounded area. So a locality would be specified as posh, modest, slum etc. and the rares are defined accordingly. Rental and Unit Area rates are defined based on the locality.</td></tr><tr><td>Not Applicable</td><td>SRO</td><td>Name of sub registrar office within the given district. For smaller cities there is only one SRO.</td></tr><tr><td>Not Applicable</td><td>Segment/ Block</td><td>Localities are further segmented into multiple blocks to define the circle rates.</td></tr></tbody></table>

#### Cross Boundaries Mapping

1. ULB - SRO mapping - It is mandatory to have and list the SROs on the screen linked with a ULB.
2. Locality - Segment/ Block mapping - It is nice to have, but not mandatory. Having this mapping will make the segment/ block list refined to select by the applicant.

### Fee, Rates, Penalty and Rebates

<table><thead><tr><th width="170.33333333333331">ARVM/UAVM</th><th width="178">CVM</th><th>Comments</th></tr></thead><tbody><tr><td>Rental Rates</td><td>Not Applicable</td><td>Rental rates are generally defined based on the locality, usage, and the construction type of the property.</td></tr><tr><td>Unit Rates</td><td>Not Applicable</td><td>Rental rates are generally defined based on the locality, usage, and the construction type of the property.</td></tr><tr><td>Not Applicable</td><td>Circle Rates</td><td>Circle rates are generally defined based on the Segment or Block, Usage, Property Type, Construction Type, and Distance of property from the road.</td></tr><tr><td>Tax Rates</td><td>Tax Rates</td><td><br></td></tr><tr><td>Penal Interest</td><td>Penal Interest</td><td><br></td></tr><tr><td>Penalties</td><td>Penalties</td><td><br></td></tr><tr><td>Rebates</td><td>Rebates</td><td><br></td></tr></tbody></table>

## Property Attributes

Below given table lists all the fields/attributes which are captured to record the property detail and use for various purposes like assessing the property tax using the current capital value of the property, generating the demand bills, locating the property, and sending the notification to owners of property etc.

### Location Details

ARV and UAV-specific boundaries are not applicable for the calculation of capital value. CVS has a completely different set of boundaries used by the registration and stamp duty department to define the circle rates and the same is given below. SRO and Block are to be added to the location detail of the property to enable CVM.

<table><thead><tr><th width="151">Field Name</th><th width="140">Field Type</th><th width="155">Is Mandatory</th><th>Comments</th></tr></thead><tbody><tr><td>Pincode</td><td>Textbox</td><td>No</td><td>Pincode of the locality property belongs to. Though it is non-mandatory.</td></tr><tr><td>Locality</td><td>Dropdown</td><td>Yes</td><td>Locality to which property belongs to. It is internally mapped to ward and ULB boundary. </td></tr><tr><td>Street Name</td><td>Textbox</td><td>No</td><td>Street name on which property is situated.</td></tr><tr><td>Door No.</td><td>Textbox</td><td>Yes</td><td>It is mandatory for Buildings and Flats</td></tr><tr><td>SRO</td><td>Dropdown</td><td>Yes</td><td>SRO will be populated based on the district of ULB.</td></tr><tr><td>Block/ Segment</td><td>Dropdown</td><td>Yes</td><td>It is a non-editable field. It is populated on SRO selected and cross hierarchy mapping if it exists.</td></tr></tbody></table>

### Construction Details

In the construction detail, occupancy of the property is irrelevant for the calculation of the property’s capital value while other masters like property type, usage, nature of business, and the construction type are used as it is. Though there would be changes in that the values are a little bit different and defined according to the registration and stamp duty department.

### Ownership Details

No change is required in existing ownership details.

### Required Documents

Documents which are required to avail of the service are already configurable.

**Property**

**Property Registration From (UI)**

<figure><img src="../../../../.gitbook/assets/image (403).png" alt=""><figcaption></figcaption></figure>

<figure><img src="https://lh5.googleusercontent.com/AiE0yyMUKTVD7d5MuP5Wp3pnhR68MgbnSldrz2q8gSGzdjkCDjynabf64Vip3RdfO00FhoSURqTiKXU7VzS7JCidBqPlmmQjZWLFKhvYEic00ikfQ40aZcNmTAquat_ubXyhtEZODcTdTjUP9zhqqmEu3lsGrpUNzZSRop1RkW0PW8W05Bs790MkJZZb9Q" alt=""><figcaption></figcaption></figure>

<figure><img src="https://lh3.googleusercontent.com/rtR08mszHTEvXAsMbsTe9swxuNkhBFlTbAuKuCkH4K84krfd__HDTBw8QcAT7p85b8t34ohlOXtQsQf39rXuaCRln9UvUN7nzTprau62czyKcfORsdoa9Jcad6qJLmOXD3-MG4wic299E6prhj-nftsIobNHcqQwDZ0odJcjmEp-1h7ApHPZTiWTC9oO0w" alt=""><figcaption></figcaption></figure>

<figure><img src="https://lh6.googleusercontent.com/jDBJKDoXJAsxE_LojB_vWpqacAGHdI3jX3IYtl3EpGw4nFJDmZn_6iINT4mOp2WCyj5Q7rNdVjBwSjeo6r9fw6FrsOvmEbBBa76jVB3ArXoNZ5E-5Dm62I9aqvEfAe34ASeCRn52JVtzuDeR8qDtuz6Vze3ywpeFAUBTfCejsztXO4u1BOrwClAnvzz__w" alt=""><figcaption></figcaption></figure>

### UOM, Rules and Calculations

#### Unit of Measurement

This needs to be configurable, configured with the start of using the product and can not be changed once the product is live and in use.

#### Calculation of Depreciation

It is @1% for every completed year after 10 years up to a maximum of 70%. Up to 10 years of building age depreciation are not provided. For the capital value of land, no depreciation is applicable.

#### Calculation of Capital Value

To calculate the capital value of a building which is not a flat in the apartment, the capital value of the constructed area and land on which the building is constructed are calculated separately and then add up to arrive at the property's capital value. The capital value is calculated floor-wise.

* Capital Value (Vacant Land)  = Area of vacant land \* circle rate defined for vacant land;
* Capital Value (Individual Building) = Land Capital Value + Builtup area of building \* circle rate defined for the building;

The capital value for the apartment is calculated on the super built-up area of the flat. In this case, land capital value is not added to flat capital value.

* Capital Value (Flat In Apartment) = Super built-up area of flat \* circle rate defined for the building;
* Calculation of Property Tax - Property Tax = Capital Value \* Tax Rates;

## Integration Approach

### No Integration

In this approach capital value calculation logic, circle rates and associated masters are maintained in DIGIT itself and any change/ revision in respect of calculation logic, and rates are done at IGRS system, which is manually done in DIGIT.&#x20;

1. Masters are maintained in DIGIT.
2. Circle rates are maintained in DIGIT and get updated when required.
3. Capital value calculation logic is maintained in DIGIT along with depreciation calculation.
4. Any change in rate and calculation logic needs a change in DIGIT in terms of configuration/ customization.

### Capital Rate API Integration

In this approach circle rates are maintained in the IGRS system. While capital value calculation logic and the masters are maintained DIGIT. The API is called to fetch the circle rates from the IGRS system.

1. Masters are maintained in DIGIT in such a way that values can easily be associated with the master values maintained at the IGRS system.
2. Circle rates are maintained only at the IGRS system and fetched by DIGIT on the fly. It avoids the need to manually maintain the rates in DIGIT.
3. Capital value calculation logic is maintained in DIGIT along with depreciation calculation, hence a change in capital value calculation needs a change in DIGIT.

### Capital Value API Integration

In this approach capital value calculation logic rates are maintained in the IGRS system. While only associated masters are maintained in DIGIT. API is called to fetch the capital value from the IGRS system by passing appropriate values.&#x20;

1. Masters are maintained in DIGIT in such a way that values can easily be associated with the master values maintained at the IGRS system.
2. Circle rates are maintained only at the IGRS system.
3. Capital value calculation logic is also maintained in the IGRS system only.&#x20;
4. DIGIT performs the API call to fetch the capital value from the IGRS system by passing all required data to IGRS.
5. This approach avoids the need of maintaining rates and calculation logic in DIGIT. Hence any change in rate and capital value calculation will require a change in DIGIT.

### Use cases  - Capital Value Calculation

Suppose circle rates are defined as given below.

<table><thead><tr><th width="154">Type</th><th width="121">Usage 1</th><th width="139">Construction</th><th width="181">Usage 2</th><th>Rate</th></tr></thead><tbody><tr><td>Individual</td><td>Residential </td><td>Pakka </td><td><br></td><td>12000</td></tr><tr><td>Individual</td><td>Residential </td><td>Kachcha </td><td><br></td><td>10000</td></tr><tr><td>Individual</td><td>Non-residential</td><td><br></td><td>Shop/ Restaurant/ Office</td><td>64000</td></tr><tr><td>Individual</td><td>Non-residential</td><td><br></td><td>Others</td><td>58000</td></tr><tr><td>Flat</td><td><br></td><td><br></td><td><br></td><td>30000</td></tr><tr><td>Plot</td><td><br></td><td><br></td><td><br></td><td>16000</td></tr></tbody></table>

\*\* Rates are defined per Sq. Mt.

### Vacant Land

Suppose there is an open plot with an area of 167 sq. mt. Then the capital value calculated will be.

Capital Value = 167 \* 16000 = 26,72,000;

### Individual Building (Residential)&#x20;

**The age of the building is less than 10 Years.**

* Plot Area = 1000 sq. mt.
* Built-up Area = 800 sq. mt.
* Usage = Pakka

The calculation of capital value will be as illustrated below.

* Capital value for land = 1000 \* 16000 = 1,60,00,000;
* Capital value for construction = 800 \* 12000 = 96,00,000;
* Capital Value of Property = 1,60,00,000 + 96,00,000 = 25,600,000;

**The age of the building is less than 21 Years.**

* Plot Area = 1000 sq. mt.
* Built-up Area = 800 sq. mt.
* Usage = Pakka

The calculation of capital value will be as illustrated below.

* Capital value for land = 1000 \* 16000 = 1,60,00,000;
* Capital value for construction = 800 \* 12000 = 96,00,000;
* Depreciated capital value of construction = 96,00,000 - 96,00,000\*11/100 = 85,44,000;
* Capital Value of Property = 1,60,00,000 + 85,44,400 = 24,544,000;

### Individual Building (Non-residential)

* Plot Area = 1000 sq. mt.
* Built-up Area = 800 sq. mt.
* Usage = Shop/ Restaurant/ Office

The calculation of capital value will be as illustrated below.

* Capital value for land = 1000 \* 16000 = 1,60,00,000;
* Capital value for construction = 800 \* 64000 = 5,12,00,000;
* Capital Value of Property = 1,60,00,000 + 5,12,00,000 = 52,80,03,200;

### Flat In an Apartment

* Super built-up area = 139.355 sq. Mt.
* Capital value = 139.355 \* 30000 = 41,80,650;

## System Studies

### IGRS UTTARAKHAND

### Screenshots

<figure><img src="https://lh5.googleusercontent.com/oVO1hlPc0VqJRQb3AnDlJ_2-4oy0oHKnoASO-X6jhMBn8Vveb8d0S4JPzh9qABufclo-qOlVMGe0mBn7_3av915_YMsTODRDAR4Lwg_F42-fLnVpywlRithfN09JHAAJmAZO9GfKQ4ekCqXM6bXeMvt30VZ1hzon8LX0iQFXAj0rDwFvcI4ZMYkpDfn1bA" alt=""><figcaption></figcaption></figure>



<figure><img src="https://lh5.googleusercontent.com/cqHvMWUz3BLpUbLuhUo3JwjlPeAwCivyaU0JpqIN5-9bHZSDFM5eUcCBti84JTFhEDhn081fvnYGKffwxDNUGaYa30uBHgEpzxDe9gOOlk3ICVp9Ykz9ZqAauc8wMp4SZetO4Xt6WWS69zzfmgySGw_STpGLv8RgvU7UgosccgxktafFeMTMyCjfKkEkvA" alt=""><figcaption></figcaption></figure>

<figure><img src="https://lh6.googleusercontent.com/5B8gbuM9xwLzLb9fW8cp3rh1QsciB92CMG5FM4EHgl9GtExxFf-1DuxtIrevSVcqk82BPFKxD8kVxn8YTDq0rXtc9eAGWxKs6PdB_yLzVfAGlGjHR24a1oq37SZK1lqrl5KwZOrK7BWhLcHPdXGIeecl787oU_BJXzC2CF34XfmMwjeAnEswsxhqYSFhFA" alt=""><figcaption></figcaption></figure>

<figure><img src="https://lh6.googleusercontent.com/QMMH7Ejc463wS5jQl0vPHX8d-TYMU82CFCn4pDYaAPQmGMLPX0QScYWfCz9KJp0O3UQHghhGsa-JPE0DMPKSkwX4N17LtkmjJ_j95fjhUrbnvMQH8fNnxv6K6S9LUzWHY6gwOqLN_6Qugv8HYLs0ZchILYI9LK_v7RbUYbTJC_S3r7nqyfgdVeZ5KCLiAQ" alt=""><figcaption></figcaption></figure>

<figure><img src="https://lh6.googleusercontent.com/rE1Znpl6woGBfwwyw1X_WLeQ6b4NcrJ6bzy9S2t63z4RbwmKRTV5Rz7VYHDAC7eLW5bQn26MFETrjLcnlLmOMGfbuYC2dCQoGHcCmOUVNhXfeM8ldeyG6Np55K2NzXJuS3IYJUaF4xMl41vPHMIwLHsRx254oYgTIJjg-1fJj2qYiUUwOFH3IqyjNSqFYg" alt=""><figcaption></figcaption></figure>

### Masters Data Relationship&#x20;

<table><thead><tr><th>Property Type</th><th>Property Type (Hindi)</th><th width="115">Usage</th><th>Nature Of Business</th><th>Construction Type</th><th>Distance From Road</th></tr></thead><tbody><tr><td>Forming Land</td><td>कृषि भूमि</td><td> </td><td> </td><td> </td><td> </td></tr><tr><td><p>Vacant Land</p><p>(Land area In Sq. Mt.)</p></td><td>अकृषि भूमि</td><td>NA</td><td>NA</td><td> </td><td>0 से 50 मीटर तक</td></tr><tr><td>51 से 350 मीटर तक</td><td></td><td></td><td></td><td></td><td></td></tr><tr><td>350 मीटर से अधिक</td><td></td><td></td><td></td><td></td><td></td></tr><tr><td>0-50 मीटर</td><td></td><td></td><td></td><td></td><td></td></tr><tr><td>51 से 200 मीटर तक</td><td></td><td></td><td></td><td></td><td></td></tr><tr><td>200 मीटर से अधिक</td><td></td><td></td><td></td><td></td><td></td></tr><tr><td>0 से 200 मीटर तक</td><td></td><td></td><td></td><td></td><td></td></tr><tr><td><p>Flat in apartment</p><p>(Super builtup area In Sq. Mt.)</p></td><td>बहुमंजलीय आवासीय भवन में स्थित आवासीय फ्लैट</td><td>Residential</td><td>NA</td><td>NA</td><td>NA</td></tr><tr><td><p>Individual building</p><p>(Builtup area in Sq. Mt.)</p></td><td>वाण्ज्यििक भवन/ गैर वाण्ज्यििक भवन</td><td>Residential</td><td>NA</td><td>प्रथम श्रेणी (लिन्टरपोष)/ (पक्का )</td><td>NA</td></tr><tr><td>द्वितीय श्रेणी (टीनपोश)/ (सेमी पक्का/ कच्चा)</td><td>NA</td><td></td><td></td><td></td><td></td></tr><tr><td>Non-residential</td><td>दुकान/रेस्टेरेन्ट/कार्यालय</td><td>NA</td><td>NA</td><td></td><td></td></tr><tr><td>अन्य वाण्ज्यििक प्रतिष्ठान</td><td>NA</td><td>NA</td><td></td><td></td><td></td></tr></tbody></table>

### Data Elements To Calculate CV

**Boundaries (IGRS Boundary Hierarchy)**

1. District
2. SRO
3. Location Area
4. Village/ Mauza

**Property Level**

1. Property Type
2. Property Sub-type
3. Usage - AP classifies open plots also into residential and non-residential categories.

**Floor Level**

1. Floor Type
2. Sub-usage - Applicable only to commercial properties.
3. Construction Type - It is termed as construction type as well.
4. Construction Year - It is calculated from the date of construction.
5. Area - In some other places it is the built-up area/ super built-up area considered for calculation.

There are 2 masters from IGRS values which covers Property Type, Usage, Sub-usage, and Construction Type. It also consists of the distance of the property from the road which is currently not available in the DIGIT. Hence the option to establish the mapping between IGRS and DIGIT masters is to be provided.

1. Area Major Class
2. Area Class

### IGRS Andhra Pradesh

### Screenshots

<figure><img src="https://lh4.googleusercontent.com/EGr2fDMIYvu_RxRFf91XiTs958iu9aGRIVZ_estxiwo5IB7z97tNX0yL5SSAeQmA0tyZvRQGbPPqr34sgTZZ44Or6bjGZ_okOrBFvDNhpZXiEibyCXv8cXpxChJ8Addq_s1BQaeFw2I8tIi4zWshDuFh4r9Sz04FTmFu796NLnzZ7G_rcop69cuWeTzdUg" alt=""><figcaption></figcaption></figure>

<figure><img src="https://lh6.googleusercontent.com/3Wt7UCdN379ohRelM29AZnYwpc8iMOMM1s-u2Lf047Da2xg4Hhsy-VdjckfBLf4I7wridZAZLtVoBjPTAo-MEClkNGxdenIi3rwc9puEdr535eFjKJd489YT-nms4GnPSmDqXpC1GWjKfEoFExoySZAPMVQN8MuzoTc_2wznbK8hPh0_xSsw6hmaF55fmg" alt=""><figcaption></figcaption></figure>

### Master Data Relationship

| Property Type       | Usage (Applicable all other than Forming Land) | Construction Type (Applicable to all irrespective of residential or non-residential) |
| ------------------- | ---------------------------------------------- | ------------------------------------------------------------------------------------ |
| Forming Land        |                                                |                                                                                      |
| Vacant Land         | Residential                                    | RCC                                                                                  |
| Non-residential     | Mud Roof                                       |                                                                                      |
| Flat in apartment   | Residential                                    | Roof with palm/grass etc. with brick wall                                            |
| Non-residential     | Roof with palm/grass etc. without brick wall   |                                                                                      |
| Individual building | Residential                                    | ACC/M. T/ Pan Tile/ Shabad Stone/Zn Sheet                                            |
| Non-residential     | ACC/TIN/Zn Sheet etc. with walls above 10 ft.  |                                                                                      |
| <p><br></p>         | <p><br></p>                                    | Poultry Form                                                                         |
| <p><br></p>         | <p><br></p>                                    | Apartment without common walls at least 3 sides                                      |

### Data Elements To Calculate CV

Boundaries (IGRS Boundary Hierarchy)

1. District
2. SRO
3. Village
4. Habitation/Locality
5. Ward
6. Block
7. Door No.

Property Level

1. Property Type
2. Property Sub-type
3. Usage - AP classifies open plots also into residential and non-residential categories.

Floor Level

1. Floor No.
2. Structure Type - It is termed a construction type as well.
3. Plinth Area - In some other places it is the built-up area/ super built-up area considered for calculation.
4. Stage of construction -  ULBs assess the completed properties only. Under-construction properties are considered for property tax assessment.
5. Age of building - It is calculated from the date of construction.

## Open Questions

* [x] Is it possible to categorize the SROs into URBAN and RURAL? As we are interested in urban areas only.

**UKD:** SROs follow different hierarchies - decided based on tehsil boundary. cannot be categorised as purely urban or rural, can be mixed

**AP:** SROs have their own jurisdiction which is independent of the ULB.  Typically SRO has Urban and Rural areas under its jurisdiction.  Some ULBs have more than one SRO.  In AP, NIC is the solution provider for IGRS.  NIC has shared the Capital Rates data with CDMA.  ULBs are asked to share the SRO Codes which fall under their jurisdiction.  So, relevant data is pushed to the respective masters of the ULB.  Provision was enabled to disable those Areas which doesn't fall under the ULB.

* [x] To calculate the capital value, is it necessary to have the deed type and deed sub-type or these are needed only to calculate stamp duty?

**UKD:** yes, these details are required.

**AP:**  To calculate Capital Value, Deed Type and Sub-type is not required.  Provision is enabled to capture Deep Type at the time of applying for New Assessment and Title Transfer.

* [x] What are the cases where the distance of the property from the road is needed?

**UKD:** in all cases, the circle rate is calculated based on this

**AP:** This is not a criterion in AP - might be specific to UKD.&#x20;

* [x] Is it necessary to capture the property detail floor-wise to calculate the capital value? If not, then what is the role of the floor in capital value calculation?

**UKD:** since earlier, they have floor-based calculation, recommended to keep floor details even though it is not being used in CV calculation. also for subsequently constructed floors, the cost of construction will be different

**AP:** Yes – floor details need to be captured as:

1. depreciation is given based on the year of construction.  There might be cases where all floors are not constructed at the same time.
2. usage \[Residence/ Non-Residence] might be different for each floor.

* [x] In capital value calculation, what is the role of the land area on which a building is constructed?

**UKD:** land area does not impact CV

**AP:** Capital Value is calculated in 2 different ways for buildings:&#x20;

1. For Apartments, Floorwise Composite Rate is defined for the specific Door No. is considered.  In this case, Land Value is not considered.
2. For Non-Apartment, Structure Value based on the type of construction is considered for the calculation of Structure Capital Value \[SCV].  The piece of Land that is used to construct the Structure is used to calculate Land Capital Value \[LCV].  SCV + LCV is the total Capital Value of the Property.

* [x] Are the capital value of land and the building both calculated and then summed up to arrive at the capital value of the built-up structure?

**UKD:** yes land and building CV are calculated separately and then added.

**AP:** Yes – Land Value and Structure Value are calculated separately and summed up for Non-Apartments.

* [x] What is the Village/ Mauza and how is it different from the Area of land?

**UKD:** this is based on tehsil revenue records/maps. not used for the calculation of CV but important in MIS

**AP:**  Not familiar with this terminology – might be specific to UKD.

* [x] What is the role of the construction year in capital value calculation?

**UKD:** this is considered in calculating depreciation

**AP:** Construction Date is required to calculate Depreciation.&#x20;

* [x] What type of rebate is provided, is it applicable to the calculation of capital value or stamp duty or both?

**UKD:** not decided yet but needs to be kept configurable. early payment + one configurable (based on ULB) are recommended heads.

**AP:**  There is no rebate given at the time of calculation of Capital Value.

* [x] What is the role of the age of the building in capital value calculation?

**UKD:** based on the year of construction. recommended keeping the year of construction rather than this

**AP:**  Age is dependent on the Date of Construction of the floor which is required for the calculation of Depreciation.&#x20;

* [x] It looks like Distance from road values is not common across the ULBs. Are the SROs following different values? Please see the table below for more details.

**UKD:** this will be decided by the Revenue Dept / SRO. ULBs will not have a say also, this needs to be maintained as part of the master data setup.

**AP:** This might be specific to UKD.

### IGRS - Boundaries (Uttarakhand)

### **Districts**

| dcode           | dname        | dname\_eng        | census\_code | distict\_order |
| --------------- | ------------ | ----------------- | ------------ | -------------- |
| DISTRICT MASTER |              |                   |              |                |
| 01              | अल्मोडा      | ALMORA            | 64           | 10             |
| 02              | बागेश्वर     | BAGESWAR          | 63           | 11             |
| 03              | चम्पावत      | CHAMPAWAT         | 65           | 13             |
| 04              | देहरादून     | DEHRADUN          | 60           | 1              |
| 05              | पौडी गढ़वाल  | PAURI GARHWAL     | 61           | 5              |
| 06              | चमोली        | CHAMOLI           | 57           | 8              |
| 07              | हरिद्वार     | HARIDWAR          | 68           | 2              |
| 08              | नैनीताल      | NAINITAL          | 66           | 4              |
| 09              | टिहरी गढ़वाल | TEHRI GARHWAL     | 59           | 6              |
| 10              | पिथौरागढ़    | PITHORAGARH       | 62           | 12             |
| 11              | रुद्रप्रयाग  | RUDRAPRAYAG       | 58           | 9              |
| 12              | उधम सिंह नगर | UDHAM SINGH NAGAR | 67           | 3              |
| 13              | उत्तरकाशी    | UTTARKASHI        | 56           | 7              |

### Sub-registrar Office (SRO)

| dcode                       | srocode | sroname                                   | sroname\_eng                 |
| --------------------------- | ------- | ----------------------------------------- | ---------------------------- |
| Sub Registrar Office Master |         |                                           |                              |
| 01                          | 01      | अल्मोडा                                   | ALMORA                       |
| 01                          | 02      | भिकियासैण                                 | BHIKIYASEN                   |
| 01                          | 03      | रानीखेत                                   | RANIKHET                     |
| 02                          | 01      | बागेश्वर                                  | BAGESWAR                     |
| 02                          | 02      | कपकोट                                     | KAPKOT                       |
| 03                          | 00      | कैम्प कार्यालय टनकपुर ,चम्पावत            | CHWAT                        |
| 03                          | 01      | चम्पावत                                   | CHAMPAWAT                    |
| 04                          | 00      | डिस्ट्रिक्ट रजिस्ट्रार, देहारादून         | DISTRICT REGISTRAR, DEHRADUN |
| 04                          | 01      | देहरादून,प्रथम                            | DEHRADUN-I                   |
| 04                          | 02      | देहरादून,द्वितीय                          | DEHRADUN-II                  |
| 04                          | 03      | देहरादून,तृतीय                            | DEHRADUN-III                 |
| 04                          | 04      | देहरादून,चतु्र्थ                          | DEHRADUN-IV                  |
| 04                          | 05      | ऋषिकेश                                    | RISHIKESH                    |
| 04                          | 06      | विकासनगर ,प्रथम                           | VIKASNAGAR-I                 |
| 04                          | 07      | विकासनगर द्वितीय                          | VIKASNAGAR-II                |
| 04                          | 08      | चकराता                                    | CHAKRATA                     |
| 04                          | 09      | मसूरी कैम्प कार्यालय                      | MUSSOORIE                    |
| 04                          | 10      | त्यणी                                     | TYUNI                        |
| 04                          | 11      | कालसी                                     | KALSI                        |
| 04                          | 12      | देहरादून तृतीय 1995-1999                  | DEHRADUN-III 1995-1999       |
| 04                          | 51      | देहरादून                                  | Dehradun                     |
| 04                          | 52      | विकासनगर                                  | Vikasnagar                   |
| 05                          | 00      | कैम्प कार्यालय यमकेश्वर, कोटद्वार         | KOTDWAR                      |
| 05                          | 01      | कोटद्वार                                  | KOTDWAR                      |
| 05                          | 02      | लेन्सडौन                                  | LANSDOWNE                    |
| 05                          | 03      | पौड़ी                                     | PAURI                        |
| 05                          | 04      | श्रीनगर                                   | SRINAGAR                     |
| 06                          | 01      | चमोली                                     | CHAMOLI                      |
| 06                          | 02      | जोशीमठ                                    | JOSHIMATH                    |
| 06                          | 03      | कर्णप्रयाग                                | KARNPRAYAG                   |
| 06                          | 04      | थराली                                     | THARALI                      |
| 07                          | 01      | हरिद्वार,प्रथम                            | HARIDWAR-I                   |
| 07                          | 02      | हरिद्वार,द्वितीय                          | HARIDWAR-II                  |
| 07                          | 03      | लकसर                                      | LAKSAR                       |
| 07                          | 04      | रुड़की,प्रथम                              | ROORKEE-I                    |
| 07                          | 05      | रुड़की,द्वितीय                            | ROORKEE-II                   |
| 07                          | 06      | रुड़की,तृतीय                              | ROORKEE-III                  |
| 07                          | 51      | हरिद्वार                                  | Haridwar                     |
| 07                          | 52      | रुड़की                                    | Roorkee                      |
| 08                          | 00      | कैम्प कार्यालय कालाढूंगी ,                | हल्द्वानी,द्वितीय            |
| 08                          | 01      | कैम्प कार्यालय कालाढूंगी ,हल्द्वानी,प्रथम | HALDWANI-I                   |
| 08                          | 02      | हल्द्वानी,द्वितीय                         | HALDWANI-II                  |
| 08                          | 03      | नैनीताल                                   | NAINITAL                     |
| 08                          | 04      | रामनगर                                    | RAMNAGAR                     |
| 08                          | 05      | धारी                                      | DHARI                        |
| 08                          | 51      | हल्द्वानी                                 | Haldwani                     |
| 09                          | 01      | देवप्रयाग                                 | DEVPRAYAG                    |
| 09                          | 02      | घनसाली                                    | GHANSALI                     |
| 09                          | 03      | जाखणीधार                                  | JAKHNIDHAR                   |
| 09                          | 04      | टिहरी                                     | TEHRI                        |
| 10                          | 01      | डीडीहाट                                   | DIDIHAT                      |
| 10                          | 02      | गंगोलीहाट                                 | GANGOLIHAT                   |
| 10                          | 03      | पिथौरागढ़                                 | PITHORAGARH                  |
| 11                          | 01      | रुद्रप्रयाग                               | RUDRAPRAYAG                  |
| 11                          | 02      | ऊखीमठ                                     | UKHIMATH                     |
| 12                          | 01      | बाजपुर                                    | BAZPUR                       |
| 12                          | 02      | जसपुर                                     | JASPUR                       |
| 12                          | 03      | काशीपुर                                   | KASHIPUR                     |
| 12                          | 04      | किच्छा                                    | KICHHA                       |
| 12                          | 05      | सितारगंज                                  | SITARGANJ                    |
| 12                          | 06      | रुद्रपुर                                  | RUDRAPUR                     |
| 13                          | 01      | बड़कोट                                    | BARKOT                       |
| 13                          | 02      | पुरोला                                    | PUROLA                       |
| 13                          | 03      | उत्तरकाशी                                 | UTTARKASHI                   |

### Blocks

<table><thead><tr><th width="115">dcode</th><th width="119">srocode</th><th width="135">circle_rate_id</th><th width="123">Block Code</th><th>Block Name</th></tr></thead><tbody><tr><td>Segment Master</td><td></td><td></td><td></td><td></td></tr><tr><td>4</td><td>1</td><td>5</td><td>3070</td><td>रायपुर मार्ग पर काली  मन्दिर से नालापानी चौक होते हुये सहस्त्रधारा मार्ग तक</td></tr><tr><td>4</td><td>1</td><td>5</td><td>3071</td><td>डोईवाला - बुल्लावाला मार्ग</td></tr><tr><td>4</td><td>1</td><td>5</td><td>3072</td><td>डोईवाला - खत्ता मार्ग</td></tr><tr><td>4</td><td>1</td><td>5</td><td>3073</td><td>डोईवाला - धर्मूचक मार्ग</td></tr><tr><td>4</td><td>1</td><td>5</td><td>3074</td><td>मियॉवाला नहर वाली सड़क से रायपुर राझांवाला तक</td></tr><tr><td>4</td><td>1</td><td>5</td><td>3075</td><td>नकरौन्दा-घिसर पडी रोड</td></tr><tr><td>4</td><td>1</td><td>5</td><td>3076</td><td>गूलरघाटी रायपुर रोड</td></tr><tr><td>4</td><td>1</td><td>5</td><td>3077</td><td>मुख्य हिरद्वार मार्ग मियॉवाला चौक से चकतुनाला होते हये हाथीखाना चौक तक</td></tr><tr><td>4</td><td>1</td><td>5</td><td>3078</td><td>मुख्य हरिद्वार मार्ग से माजरी माफी (रेलवे फाटक), हरिपुर/नवादा होते हुए इन्दरपुर तक</td></tr><tr><td>4</td><td>1</td><td>5</td><td>3079</td><td>जोगीवाला चौक से बद्रीपुर होते हुए इन्दरपुर तक, बद्रीपुर चौक से माजरी माफी तक</td></tr><tr><td>4</td><td>1</td><td>5</td><td>3080</td><td>विधान सभा के बाद स्थित रेलवे फाटक के बाद से एम0डी0डी0ए0 कालोनी केदारपुरम तक</td></tr><tr><td>4</td><td>1</td><td>5</td><td>3081</td><td>हरिद्वार रोड पर कुऑवाला से गूलरघाटी चौक तक</td></tr><tr><td>4</td><td>1</td><td>5</td><td>3082</td><td>फयरिंग रेंज के बाद से दौडवाला होते हुये दुधली डोईवाला मार्ग तक, केदारपुर सचिवालय कालोनी के बाद से दुधली डोईवाला मार्ग तक</td></tr><tr><td>4</td><td>1</td><td>5</td><td>3083</td><td>दून यूनिवर्सिटी से मोथरोवाला लिंक रोड</td></tr><tr><td>4</td><td>1</td><td>5</td><td>3084</td><td>सहारनपुर हरिद्वार बाईपास मार्द से दक्षिण दिशा की ओर जाने वाली मोथरोवाला मार्ग से दून यूनिवर्सिटी के सामने से केदारपुर / सचिवालय कालोनी होकर जाने वाला मार्ग जो अन्त में फाईरिंग रैज के पुल पर मिल जाता है ।</td></tr><tr><td>4</td><td>1</td><td>5</td><td>3085</td><td>सहारनपुर हरिद्वार बाईपास मार्ग पर पुलिस चैक पोस्ट के सामने, महिन्द्रा शोरूम के बाराबर से मोथरोवाला रोड बंगाली कोठी के बाद ,केदारपुर, प्राथमिक पाठशाला होते हुए दुधली-डोईवाला मार्ग के पुल तक,</td></tr><tr><td>4</td><td>1</td><td>5</td><td>3086</td><td>सहारनपुर हरिद्वार बाईपास मार्द से दक्षिण दिशा की ओर जाने वाली कारगी / कारगी चौक से बंजारावाला तक,</td></tr><tr><td>4</td><td>1</td><td>5</td><td>3087</td><td>मौथरोवाला दूधली डोईवाला मार्ग</td></tr><tr><td>4</td><td>1</td><td>5</td><td>3088</td><td>चकराता रोड आई0एम0ए0 के सामने से प्रेमनगर-गोरखपुर रोड ग्राम आरकेडियाग्रान्ट की सीमा तक तथा तेलपुरा चौक तक</td></tr><tr><td>4</td><td>1</td><td>5</td><td>3089</td><td>डाईवर्जन रोड से सिनौला-जोहडी-अनारवाला वाला मार्ग</td></tr><tr><td>4</td><td>1</td><td>5</td><td>3090</td><td>जाखन-जोहडी मार्ग</td></tr><tr><td>4</td><td>1</td><td>5</td><td>3091</td><td>रिखोली-मसूरी  बाईपास रोड</td></tr><tr><td>4</td><td>1</td><td>5</td><td>3092</td><td>कुठाल गेट से मसूरी तक मुख्य मार्ग</td></tr><tr><td>4</td><td>1</td><td>5</td><td>3093</td><td>पुराना पोस्ट आफिस (जोगीवाला) से किद्दूवाला चौक तक</td></tr><tr><td>4</td><td>1</td><td>5</td><td>3094</td><td>पुलिया नं0 6 से किद्दूवाला चौक होते हुये महाराणा प्रताप चौक तक</td></tr><tr><td>4</td><td>1</td><td>5</td><td>3095</td><td>मसूरी बाईपास रोड-रिंग रोड (पुलिया नं0 6 के बाद से रायपुर रोड तक )</td></tr><tr><td>4</td><td>1</td><td>5</td><td>3096</td><td>मालसी पुलिया से दोनाली चौक तक</td></tr><tr><td>4</td><td>1</td><td>5</td><td>3097</td><td>रायपुर चौक (शिव मन्दिर) से मालदेवता मार्ग वाया वाण्डा वाली</td></tr><tr><td>4</td><td>1</td><td>5</td><td>3098</td><td>किरसाली चौक से काला गॉव तक</td></tr><tr><td>4</td><td>1</td><td>5</td><td>3099</td><td>सहस्त्रधारा रोड ( कुल्हान करनपुर के बाद से मालदेवता तक)</td></tr><tr><td>4</td><td>1</td><td>5</td><td>3100</td><td>मालदेवता सिल्ला क्यारा रोड</td></tr><tr><td>4</td><td>1</td><td>5</td><td>3101</td><td>रायपुर रोड पर चक्की नम्बर चार से दोनाली चौक तक</td></tr><tr><td>4</td><td>1</td><td>5</td><td>6285</td><td>रायपुर - थानो मार्ग (रायपुर चौक से थानो चौक तक)</td></tr><tr><td>4</td><td>1</td><td>5</td><td>3102</td><td>सहस्त्रधारा मार्ग पर स्थित किरसाली चौक से मसूरी बाई पास मार्ग पड़नेवाले समस्त राजस्व ग्राम एवं उक्त मार्ग के अन्त में स्थित साई मन्दिर के बराबर पर पहॅुचने वाले मार्ग तक</td></tr><tr><td>4</td><td>1</td><td>5</td><td>3103</td><td>गुनियाल गांव-भगवतपुर मार्ग पुरूकुल गॉव तक</td></tr><tr><td>4</td><td>1</td><td>5</td><td>3104</td><td>हरिद्वार रोड पर लच्छीवाला फलाईओवर के बाद से डोईवाला टाउन एरिया क्षेत्र के प्रारम्भ होने तक</td></tr><tr><td>4</td><td>1</td><td>5</td><td>3105</td><td>शिमला बाईपास राड पर मेहुवाला ग्राम के बाद से ग्राम बडोवाल की सीमा समाप्ति तक</td></tr><tr><td>4</td><td>1</td><td>5</td><td>3106</td><td>सहारनपुर रोड पर चन्द्रबनी चौक से वाईल्ड लाईफ संस्थान तक</td></tr><tr><td>4</td><td>1</td><td>5</td><td>3107</td><td>सहारनपुर रोड से ब्राहमणवाला रोड माजरा क्षेत्र</td></tr><tr><td>4</td><td>1</td><td>5</td><td>3108</td><td>सहारनपुर रोड से इन्द्रा गाधी मार्ग माजरा क्षेत्र</td></tr><tr><td>4</td><td>1</td><td>5</td><td>3109</td><td>सहस्त्रधारा रोड पर छतरी के बाद से सहस्त्रधारा तक</td></tr><tr><td>4</td><td>1</td><td>5</td><td>3110</td><td>रायपुर रोड से काली मन्दिर से रायपुर तक</td></tr><tr><td>4</td><td>1</td><td>5</td><td>3111</td><td>रायपुर रोड पर सहस्त्रधारा  चौक से काली मंदिर तक</td></tr><tr><td>4</td><td>1</td><td>5</td><td>3112</td><td>सहस्त्रधारा मार्ग पर स्थित आई0टी0 पार्क वाले मार्ग पर पड़नेवाले समस्त राजस्व ग्राम एवं उक्त मार्ग के अन्त में स्थित उप्पल टावर से होते हुये कैनाल रोड से पूर्व तक</td></tr><tr><td>4</td><td>1</td><td>5</td><td>3113</td><td>सहस्त्रधारा रोड पर आई0 टी0 पार्क के आगे से छतरी तक</td></tr><tr><td>4</td><td>1</td><td>5</td><td>3114</td><td>मसूरी बाईपास रोड-रिंग रोड (जोगीवाला चौक से पोस्ट आफिस होते हुये पुलिया नं0 6 तक)</td></tr><tr><td>4</td><td>1</td><td>5</td><td>3115</td><td>लक्ष्मी रोड के चौराहे से बद्रीश कालोनी होते हुए पुलिया नं0 6 तक)</td></tr><tr><td>4</td><td>1</td><td>5</td><td>3116</td><td>मोथरोवाला रोड (धर्मपुर चौक के निकट से बाईपास रोड तक)</td></tr><tr><td>4</td><td>1</td><td>5</td><td>3117</td><td>माता मन्दिर रोड (धर्मपुर चौक से बाईपास रोड पर स्थित पुलिस चौक पोस्ट तक)</td></tr><tr><td>4</td><td>1</td><td>5</td><td>3118</td><td>हरिद्वार रोड पर कुऑवाला से लच्छीवाला फ्लाई ओवर तक</td></tr><tr><td>4</td><td>1</td><td>5</td><td>3119</td><td>कौलागढ रोड पर सैन्ट्रल स्कूल से आगे कौलागढ की सीमा तक</td></tr><tr><td>4</td><td>1</td><td>5</td><td>3120</td><td>चकराता रोड पर प्रेननगर बस स्टैन्ड से नदी तक</td></tr><tr><td>4</td><td>1</td><td>5</td><td>3121</td><td>बाईपास रोड (सहारनपुररोड से हरिद्वार रोड तक)</td></tr><tr><td>4</td><td>1</td><td>5</td><td>3122</td><td>शिमला बाईपास रोड पर सहारनपुर रोड के 350 मीटर बाद से मेहुवाला ग्राम की सीमा समाप्ति तक</td></tr><tr><td>4</td><td>1</td><td>5</td><td>3123</td><td>सहारनपुर रोड पर सुभाष नगर चौक से आगे वन क्षेत्र तक</td></tr><tr><td>4</td><td>1</td><td>5</td><td>3124</td><td>सहारनपुर रोड लाल पुल से महन्त इन्द्रेश अस्पताल- देहराखास होते हुये कारगी चौक तक</td></tr><tr><td>4</td><td>1</td><td>5</td><td>3125</td><td>सर्वे चौक से रायपुर रोड पर रिस्पना पुल, सहस्त्रधारा चौक होते हुये आई0टी0पार्क तक</td></tr><tr><td>4</td><td>1</td><td>5</td><td>3126</td><td>हरिद्वार रोड पर जोगीवाला से कुँवावाला तक</td></tr><tr><td>4</td><td>1</td><td>5</td><td>3127</td><td>सहारनपुर रोड पर टर्नर रोड से सुभाष नगर चौक तक</td></tr><tr><td>4</td><td>1</td><td>5</td><td>3128</td><td>एफ आर आई के सामने से बसन्त विहार चौक तक</td></tr><tr><td>4</td><td>1</td><td>5</td><td>3129</td><td>अनुराग नर्सरी रोड पर बल्लीवाला चौक से बसन्त विहार चौक- लवली मार्किट- पंडितवाडी चकराता रोड तक</td></tr><tr><td>4</td><td>1</td><td>5</td><td>3130</td><td>अनुराग नर्सरी से इन्द्रानगर- सीमाद्वार- जी0एम0एस0 रोड तक</td></tr><tr><td>4</td><td>1</td><td>5</td><td>3131</td><td>कांवली रोड/शिवाजी मार्ग पर सहारनपुर चौक से बल्लीवाला चौक तक</td></tr><tr><td>4</td><td>1</td><td>5</td><td>3132</td><td>मौरवियन इन्स्टीटयूट वाली ओल्ड मसूरी रोड पर राजपुर तिराहे से कुठालगेट तक</td></tr><tr><td>4</td><td>1</td><td>5</td><td>3133</td><td>शहंशाही आश्रम वाली ओल्ड मसूरी रोड पर राजपुर तिराहे से कुठालगेट तक</td></tr><tr><td>4</td><td>1</td><td>5</td><td>3134</td><td>जी0एम0एस0 रोड (बल्लीवाला चौक से सेवला कलां ट्रान्सपोर्ट नगर होते हुए मौहब्बेवाला, सहारनपुर रोड तक) तथा सकलानी गैस गोदाम क्रासिंग से सहारनपुर रोड पर सब्जी मण्डी तिराहे तक</td></tr><tr><td>4</td><td>1</td><td>5</td><td>3135</td><td>सहारनपुर रोड पर बिन्दाल पुल से टर्नर रोड तक</td></tr><tr><td>4</td><td>1</td><td>5</td><td>3136</td><td>गढी चौक से बल्लुपुर चौक वाली- कैनाल रोड</td></tr><tr><td>4</td><td>1</td><td>5</td><td>3137</td><td>चकराता रोड पर बल्लुपुर चौक से प्रेमनगर बस स्टैण्ड तक</td></tr><tr><td>4</td><td>1</td><td>5</td><td>3138</td><td>हरिद्वार रोड रिस्पना पुल से जोगीवाला तक</td></tr><tr><td>4</td><td>1</td><td>5</td><td>3139</td><td>जी0एम0एस0 रोड (बल्लुपुर चौक से बल्लीवाला चौक तक)</td></tr><tr><td>4</td><td>1</td><td>5</td><td>3140</td><td>कौलागढ़ रोड पर किशन नगर चौक से सैन्ट्रल स्कूल तक</td></tr><tr><td>4</td><td>1</td><td>5</td><td>3141</td><td>सहारनपुर रोड पर सहारनपुर चौक से बिन्दाल पुल तक</td></tr><tr><td>4</td><td>1</td><td>5</td><td>3142</td><td>डायवर्जन रोड पर मालसी डीयर पार्क से कुठाल गेट तक</td></tr><tr><td>4</td><td>1</td><td>5</td><td>3143</td><td>डायवर्जन रोड पर मसूरी बाईपास से मालसी डीयर पार्क तक</td></tr><tr><td>4</td><td>1</td><td>5</td><td>3144</td><td>राजपुर रोड के समानान्तर कैनाल रोड काठबंगला तक</td></tr><tr><td>4</td><td>1</td><td>5</td><td>3145</td><td>राजपुर रोड पर मसूरी बाईपास से राजपुर तक (साई मन्दिर होते हुए)</td></tr><tr><td>4</td><td>1</td><td>5</td><td>3146</td><td>सुभाष रोड</td></tr><tr><td>4</td><td>1</td><td>5</td><td>3147</td><td>ईस्ट कैनाल राड</td></tr><tr><td>4</td><td>1</td><td>5</td><td>3148</td><td>न्यू कैन्ट रोड (कैंट सीमा तक)</td></tr><tr><td>4</td><td>1</td><td>5</td><td>3149</td><td>हरिद्वार रोड प्रिन्स चौक से रिस्पना पुल तक</td></tr><tr><td>4</td><td>1</td><td>5</td><td>3150</td><td>चकराता रोड पर घंटाघर से बिन्दाल पुल-किशन नगर चौक होते हुये बल्लुपुर चौराहे तक</td></tr><tr><td>4</td><td>1</td><td>5</td><td>3151</td><td>गांधी रोड पर रेलवे स्टेशन से आढत बाजार होते हुये सहारनपुर चौक तक</td></tr><tr><td>4</td><td>1</td><td>5</td><td>3152</td><td>सहारनपुर रोड पर रेलवे स्टेशन से सहारनपुर चौक तक</td></tr><tr><td>4</td><td>1</td><td>5</td><td>3153</td><td>घंटाघर से लक्खीबाग चौकी तक के मध्य स्थित पल्टन बाजार/धामावाला/पीपल मण्डी/दर्शनी गेट</td></tr><tr><td>4</td><td>1</td><td>5</td><td>3154</td><td>गांधी रोड पर घंटाघर से दर्शन लाल चौक/ प्रिन्स चौक होते हुये रेलवे सटशन तक</td></tr><tr><td>4</td><td>1</td><td>5</td><td>3155</td><td>राजपुर रोड पर आर0टी0ओ0  कार्यालय से मसूरी बाईपास तक</td></tr><tr><td>4</td><td>1</td><td>5</td><td>3157</td><td>राजपुर रोड पर घण्टाघर से आर0टी0ओ0  कार्यालय तक</td></tr><tr><td>4</td><td>1</td><td>5</td><td>3218</td><td>अजबपुर कलां</td></tr><tr><td>4</td><td>1</td><td>5</td><td>3420</td><td>बिन्दाल रोड</td></tr><tr><td>4</td><td>1</td><td>5</td><td>3421</td><td>खदरी मौहल्ला</td></tr><tr><td>4</td><td>1</td><td>5</td><td>3422</td><td>छबील बाग</td></tr><tr><td>4</td><td>1</td><td>5</td><td>3423</td><td>जटिया मौहल्ला</td></tr><tr><td>4</td><td>1</td><td>5</td><td>3424</td><td>इन्द्रश नगर</td></tr><tr><td>4</td><td>1</td><td>5</td><td>3425</td><td>प्रेमनगर</td></tr><tr><td>4</td><td>1</td><td>5</td><td>3426</td><td>कांवली शेष क्षेत्र (कांवली क्षेत्र की उल्लिखित कालोनी / मौहल्लों को छोड़कर)</td></tr><tr><td>4</td><td>1</td><td>5</td><td>3427</td><td>चक सेवलाखर्द</td></tr><tr><td>4</td><td>1</td><td>5</td><td>3428</td><td>कारगी ग्राण्ट</td></tr><tr><td>4</td><td>1</td><td>5</td><td>3429</td><td>निरंजनपुर</td></tr><tr><td>4</td><td>1</td><td>5</td><td>3430</td><td>ब्राहमणवाला</td></tr><tr><td>4</td><td>1</td><td>5</td><td>3431</td><td>सत्यान मौहल्ला</td></tr><tr><td>4</td><td>1</td><td>5</td><td>3432</td><td>पुराना राजपुर</td></tr><tr><td>4</td><td>1</td><td>5</td><td>3433</td><td>राजपुर माफी</td></tr><tr><td>4</td><td>1</td><td>5</td><td>3434</td><td>प्रेमपुर माफी</td></tr><tr><td>4</td><td>1</td><td>5</td><td>3435</td><td>लोहारवाला</td></tr><tr><td>4</td><td>1</td><td>5</td><td>3436</td><td>गोपीवाला</td></tr><tr><td>4</td><td>1</td><td>5</td><td>3437</td><td>धरतावाला</td></tr><tr><td>4</td><td>1</td><td>5</td><td>3438</td><td>डुगालगांव</td></tr><tr><td>4</td><td>1</td><td>5</td><td>3439</td><td>थानीगांव</td></tr><tr><td>4</td><td>1</td><td>5</td><td>3440</td><td>गढी कैन्ट</td></tr><tr><td>4</td><td>1</td><td>5</td><td>3441</td><td>कौलागढ मय चक भूड</td></tr><tr><td>4</td><td>1</td><td>5</td><td>3442</td><td>चक शाहनगर</td></tr><tr><td>4</td><td>1</td><td>5</td><td>3443</td><td>शाहनगर</td></tr><tr><td>4</td><td>1</td><td>5</td><td>3444</td><td>शाहपुर सन्तौर</td></tr><tr><td>4</td><td>1</td><td>5</td><td>3445</td><td>इन्दरपुर</td></tr><tr><td>4</td><td>1</td><td>5</td><td>3446</td><td>केदारपुर</td></tr><tr><td>4</td><td>1</td><td>5</td><td>3447</td><td>चक डालनवाला</td></tr><tr><td>4</td><td>1</td><td>5</td><td>3448</td><td>धर्मपुर डांडा</td></tr><tr><td>4</td><td>1</td><td>5</td><td>3449</td><td>डिफेन्स कालोनी, शाहनगर</td></tr><tr><td>4</td><td>1</td><td>5</td><td>3450</td><td>एम0डी0डी0ए0 कालोनी अजबपुर</td></tr><tr><td>4</td><td>1</td><td>5</td><td>3451</td><td>एम0डी0डी0ए0 कालोनी केदारपुर</td></tr><tr><td>4</td><td>1</td><td>5</td><td>3452</td><td>अजबपुर चक-2 (चक अजबपुरकला)</td></tr><tr><td>4</td><td>1</td><td>5</td><td>3453</td><td>अजबपुर चक- 1 (चक अजबपुरकला)</td></tr><tr><td>4</td><td>1</td><td>5</td><td>3454</td><td>अजबपुर खुर्द</td></tr><tr><td>4</td><td>1</td><td>5</td><td>3455</td><td>ब्रहमावाला</td></tr><tr><td>4</td><td>1</td><td>5</td><td>3456</td><td>चिडोवाली</td></tr><tr><td>4</td><td>1</td><td>5</td><td>3457</td><td>धोरण खास</td></tr><tr><td>4</td><td>1</td><td>5</td><td>3458</td><td>कण्डोली (केन्द्रीयदून)</td></tr><tr><td>4</td><td>1</td><td>5</td><td>3459</td><td>हथड़ीगांव</td></tr><tr><td>4</td><td>1</td><td>5</td><td>3460</td><td>रांघडवाला</td></tr><tr><td>4</td><td>1</td><td>5</td><td>3461</td><td>बाजावाला</td></tr><tr><td>4</td><td>1</td><td>5</td><td>3462</td><td>माजरा</td></tr><tr><td>4</td><td>1</td><td>5</td><td>3464</td><td>धर्मपुर</td></tr><tr><td>4</td><td>1</td><td>5</td><td>3465</td><td>पंडितवाडी</td></tr><tr><td>4</td><td>1</td><td>5</td><td>3466</td><td>अजीत प्रसाद मार्ग</td></tr><tr><td>4</td><td>1</td><td>5</td><td>3467</td><td>आनन्द चौक</td></tr><tr><td>4</td><td>1</td><td>5</td><td>3468</td><td>रामेश्वर मौहल्ला</td></tr><tr><td>4</td><td>1</td><td>5</td><td>3469</td><td>अखाडा मौहल्ला</td></tr><tr><td>4</td><td>1</td><td>5</td><td>3470</td><td>मुस्लिम कालोनी</td></tr><tr><td>4</td><td>1</td><td>5</td><td>3471</td><td>खुडबुडा समस्त ब्लांक</td></tr><tr><td>4</td><td>1</td><td>5</td><td>3472</td><td>गुजराती मौहल्ला</td></tr><tr><td>4</td><td>1</td><td>5</td><td>3473</td><td>डांडीपुर मौहल्ला</td></tr><tr><td>4</td><td>1</td><td>5</td><td>3474</td><td>मन्नूगंज</td></tr><tr><td>4</td><td>1</td><td>5</td><td>3475</td><td>हकीकतराय नगर</td></tr><tr><td>4</td><td>1</td><td>5</td><td>3476</td><td>नेताजी मौहल्ला</td></tr><tr><td>4</td><td>1</td><td>5</td><td>3477</td><td>मालियाना मौहल्ला</td></tr><tr><td>4</td><td>1</td><td>5</td><td>3478</td><td>लक्खीबाग</td></tr><tr><td>4</td><td>1</td><td>5</td><td>3479</td><td>रामनगर</td></tr><tr><td>4</td><td>1</td><td>5</td><td>3480</td><td>सिंगल मण्डी</td></tr><tr><td>4</td><td>1</td><td>5</td><td>3481</td><td>रीठा मण्डी</td></tr><tr><td>4</td><td>1</td><td>5</td><td>3482</td><td>पथरीबाग</td></tr><tr><td>4</td><td>1</td><td>5</td><td>3483</td><td>भण्डारी बाग समस्त ब्लांक</td></tr><tr><td>4</td><td>1</td><td>5</td><td>3484</td><td>ट्रान्सपोर्ट नगर</td></tr><tr><td>4</td><td>1</td><td>5</td><td>3485</td><td>बाडीगार्ड</td></tr><tr><td>4</td><td>1</td><td>5</td><td>3486</td><td>टीचर्स कालोनी</td></tr><tr><td>4</td><td>1</td><td>5</td><td>3487</td><td>कुम्हारमण्डी</td></tr><tr><td>4</td><td>1</td><td>5</td><td>3488</td><td>गोविन्दगढ</td></tr><tr><td>4</td><td>1</td><td>5</td><td>3489</td><td>कौलागढ मय चक</td></tr><tr><td>4</td><td>1</td><td>5</td><td>3491</td><td>सैय्यद मौहल्ला</td></tr><tr><td>4</td><td>1</td><td>5</td><td>3492</td><td>हाथीबडकला</td></tr><tr><td>4</td><td>1</td><td>5</td><td>3493</td><td>विजय कालोनी</td></tr><tr><td>4</td><td>1</td><td>5</td><td>3494</td><td>चक सालावाला</td></tr><tr><td>4</td><td>1</td><td>5</td><td>3495</td><td>सालावाला</td></tr><tr><td>4</td><td>1</td><td>5</td><td>3496</td><td>पथरियापीर</td></tr><tr><td>4</td><td>1</td><td>5</td><td>3497</td><td>अहीर मण्डी</td></tr><tr><td>4</td><td>1</td><td>5</td><td>3498</td><td>परसोलीवाला मय चक नरसिह वाला</td></tr><tr><td>4</td><td>1</td><td>5</td><td>3499</td><td>डोभालवाला</td></tr><tr><td>4</td><td>1</td><td>5</td><td>3500</td><td>बकराल वाला</td></tr><tr><td>4</td><td>1</td><td>5</td><td>3501</td><td>डंगवाल मार्ग</td></tr><tr><td>4</td><td>1</td><td>5</td><td>3502</td><td>ओंकार रोड</td></tr><tr><td>4</td><td>1</td><td>5</td><td>3503</td><td>मित्रलोक कालोनी</td></tr><tr><td>4</td><td>1</td><td>5</td><td>3504</td><td>चुक्खुवाला</td></tr><tr><td>4</td><td>1</td><td>5</td><td>3505</td><td>चुक्खुवाला नई बस्ती</td></tr><tr><td>4</td><td>1</td><td>5</td><td>3506</td><td>इन्द्रा कालोनी चुक्खुवाला</td></tr><tr><td>4</td><td>1</td><td>5</td><td>3507</td><td>गढ़ी उद्दीवाला</td></tr><tr><td>4</td><td>1</td><td>5</td><td>3508</td><td>गढ़ी</td></tr><tr><td>4</td><td>1</td><td>5</td><td>3509</td><td>आराघर</td></tr><tr><td>4</td><td>1</td><td>5</td><td>3510</td><td>शास्त्रीनगर (समस्त लेन)</td></tr><tr><td>4</td><td>1</td><td>5</td><td>3511</td><td>नेहरू कालोनी (क्रमांक 4-D-15 में वर्णित क्षेत्र को छोड़कर)</td></tr><tr><td>4</td><td>1</td><td>5</td><td>3512</td><td>वीरगिरवाली</td></tr><tr><td>4</td><td>1</td><td>5</td><td>3513</td><td>घास मण्डी</td></tr><tr><td>4</td><td>1</td><td>5</td><td>3514</td><td>द्वारिका पुरी</td></tr><tr><td>4</td><td>1</td><td>5</td><td>3515</td><td>शक्ति एन्कलेव</td></tr><tr><td>4</td><td>1</td><td>5</td><td>3516</td><td>व्योमप्रस्थ एन्कलेव</td></tr><tr><td>4</td><td>1</td><td>5</td><td>3517</td><td>अलकनन्दा एन्कलेव</td></tr><tr><td>4</td><td>1</td><td>5</td><td>3518</td><td>मिलन विहार/ एन्कलेव</td></tr><tr><td>4</td><td>1</td><td>5</td><td>3519</td><td>काली मंदिर एन्कलेव</td></tr><tr><td>4</td><td>1</td><td>5</td><td>3520</td><td>पुष्पांजली एन्कलेव</td></tr><tr><td>4</td><td>1</td><td>5</td><td>3521</td><td>मेघा एन्कलेव</td></tr><tr><td>4</td><td>1</td><td>5</td><td>3522</td><td>नर्मदा एन्कलेव</td></tr><tr><td>4</td><td>1</td><td>5</td><td>3523</td><td>अंकित पुरम एन्कलेव</td></tr><tr><td>4</td><td>1</td><td>5</td><td>3524</td><td>संगम विहार</td></tr><tr><td>4</td><td>1</td><td>5</td><td>3525</td><td>नेहरूपुरम एन्कलेव</td></tr><tr><td>4</td><td>1</td><td>5</td><td>3526</td><td>विवेक विहार</td></tr><tr><td>4</td><td>1</td><td>5</td><td>3527</td><td>दुर्गा विहार</td></tr><tr><td>4</td><td>1</td><td>5</td><td>3528</td><td>कालिन्दी एन्कलेव</td></tr><tr><td>4</td><td>1</td><td>5</td><td>3529</td><td>उत्सव विहार</td></tr><tr><td>4</td><td>1</td><td>5</td><td>3530</td><td>वन विहार</td></tr><tr><td>4</td><td>1</td><td>5</td><td>3531</td><td>महारानी बाग</td></tr><tr><td>4</td><td>1</td><td>5</td><td>3532</td><td>हिल व्यू कालोनी</td></tr><tr><td>4</td><td>1</td><td>5</td><td>3533</td><td>दत्ता इन्कलेव</td></tr><tr><td>4</td><td>1</td><td>5</td><td>3534</td><td>इंजीनियर्स इन्कलेव (समस्त फेज कॅावली क्षेत्र)</td></tr><tr><td>4</td><td>1</td><td>5</td><td>3535</td><td>आशीर्वाद इन्कलेव</td></tr><tr><td>4</td><td>1</td><td>5</td><td>3536</td><td>मोहित नगर</td></tr><tr><td>4</td><td>1</td><td>5</td><td>3537</td><td>बसंत विहार</td></tr><tr><td>4</td><td>1</td><td>5</td><td>3538</td><td>इन्दिरा नगर कालोनी</td></tr><tr><td>4</td><td>1</td><td>5</td><td>3539</td><td>कलालोवाली गली</td></tr><tr><td>4</td><td>1</td><td>5</td><td>3659</td><td>लूनिया मौहल्ला</td></tr><tr><td>4</td><td>1</td><td>5</td><td>3661</td><td>नेहरू नगर</td></tr><tr><td>4</td><td>1</td><td>5</td><td>3662</td><td>गांधी ग्राम</td></tr><tr><td>4</td><td>1</td><td>5</td><td>3667</td><td>देहराखास</td></tr><tr><td>4</td><td>1</td><td>5</td><td>3668</td><td>लक्ष्मण चौक</td></tr><tr><td>4</td><td>1</td><td>5</td><td>3670</td><td>वेस्ट पटेल नगर</td></tr><tr><td>4</td><td>1</td><td>5</td><td>3671</td><td>ईस्ट पटेल नगर</td></tr><tr><td>4</td><td>1</td><td>5</td><td>3672</td><td>गुरू रोड</td></tr><tr><td>4</td><td>1</td><td>5</td><td>3673</td><td>सरस्वती सोनी मार्ग</td></tr><tr><td>4</td><td>1</td><td>5</td><td>3674</td><td>केशव रोड</td></tr><tr><td>4</td><td>1</td><td>5</td><td>3675</td><td>पार्क रोड</td></tr><tr><td>4</td><td>1</td><td>5</td><td>3676</td><td>विचारनन्द मार्ग</td></tr><tr><td>4</td><td>1</td><td>5</td><td>3677</td><td>पी0डी0 टंडन रोड</td></tr><tr><td>4</td><td>1</td><td>5</td><td>3678</td><td>नैशनल रोड</td></tr><tr><td>4</td><td>1</td><td>5</td><td>3679</td><td>मालवीय रोड</td></tr><tr><td>4</td><td>1</td><td>5</td><td>3680</td><td>महन्त रोड</td></tr><tr><td>4</td><td>1</td><td>5</td><td>3681</td><td>केशव विहार</td></tr><tr><td>4</td><td>1</td><td>5</td><td>3682</td><td>काली मंदिर एन्कलेव</td></tr><tr><td>4</td><td>1</td><td>5</td><td>3683</td><td>शाम्भबी लोक</td></tr><tr><td>4</td><td>1</td><td>5</td><td>3684</td><td>वसंत विहार एन्कलेव</td></tr><tr><td>4</td><td>1</td><td>5</td><td>3685</td><td>साई लोक</td></tr><tr><td>4</td><td>1</td><td>5</td><td>3686</td><td>अशोक विहार</td></tr><tr><td>4</td><td>1</td><td>5</td><td>3688</td><td>जनकपुरी एन्कलेव</td></tr><tr><td>4</td><td>1</td><td>5</td><td>3689</td><td>गढवाल कालोनी</td></tr><tr><td>4</td><td>1</td><td>5</td><td>3691</td><td>शिवालिकपुरम</td></tr><tr><td>4</td><td>1</td><td>5</td><td>3692</td><td>प्रियदर्शनी एन्कलेव</td></tr><tr><td>4</td><td>1</td><td>5</td><td>3694</td><td>ओल्ड सहस्त्रधारा रोड (अरविन्द मार्ग)</td></tr><tr><td>4</td><td>1</td><td>5</td><td>3695</td><td>मानसिंहवाला</td></tr><tr><td>4</td><td>1</td><td>5</td><td>3696</td><td>ओल्ड डालनवाला</td></tr><tr><td>4</td><td>1</td><td>5</td><td>3697</td><td>करनपुर बाजार</td></tr><tr><td>4</td><td>1</td><td>5</td><td>3698</td><td>आर्य नगर</td></tr><tr><td>4</td><td>1</td><td>5</td><td>3699</td><td>किशनपुर</td></tr><tr><td>4</td><td>1</td><td>5</td><td>3700</td><td>ढाकपट्टी</td></tr><tr><td>4</td><td>1</td><td>5</td><td>3701</td><td>जाखन</td></tr><tr><td>4</td><td>1</td><td>5</td><td>3702</td><td>राजपुर</td></tr><tr><td>4</td><td>1</td><td>5</td><td>3703</td><td>प्रतीतपुर संतौर</td></tr><tr><td>4</td><td>1</td><td>5</td><td>3704</td><td>आकाशदीप कालोनी</td></tr><tr><td>4</td><td>1</td><td>5</td><td>3705</td><td>विजयपार्क एक्सटेशन</td></tr><tr><td>4</td><td>1</td><td>5</td><td>3706</td><td>विजयपार्क</td></tr><tr><td>4</td><td>1</td><td>5</td><td>3707</td><td>यमुना कालोनी</td></tr><tr><td>4</td><td>1</td><td>5</td><td>3708</td><td>ईदगाह</td></tr><tr><td>4</td><td>1</td><td>5</td><td>3709</td><td>प्रकाश नगर</td></tr><tr><td>4</td><td>1</td><td>5</td><td>3710</td><td>राम विहार</td></tr><tr><td>4</td><td>1</td><td>5</td><td>3711</td><td>महेंद्र विहार</td></tr><tr><td>4</td><td>1</td><td>5</td><td>3712</td><td>आनन्द विहार</td></tr><tr><td>4</td><td>1</td><td>5</td><td>3713</td><td>नरेन्द्र विहार</td></tr><tr><td>4</td><td>1</td><td>5</td><td>3714</td><td>दीप लोक कालोनी</td></tr><tr><td>4</td><td>1</td><td>5</td><td>3715</td><td>चायबाग कौलागढ</td></tr><tr><td>4</td><td>1</td><td>5</td><td>3717</td><td>कौलागढ</td></tr><tr><td>4</td><td>1</td><td>5</td><td>3718</td><td>बल्लुपुर</td></tr><tr><td>4</td><td>1</td><td>5</td><td>3721</td><td>किशन नगर</td></tr><tr><td>4</td><td>1</td><td>5</td><td>3722</td><td>राजेन्द्र नगर</td></tr><tr><td>4</td><td>1</td><td>5</td><td>3723</td><td>एम0डी0डी0ए0 कालोनी चन्दर रोड</td></tr><tr><td>4</td><td>1</td><td>5</td><td>3725</td><td>डिफेन्स कालोनी चक शाहनगर</td></tr><tr><td>4</td><td>1</td><td>5</td><td>3729</td><td>उषा कालोनी</td></tr><tr><td>4</td><td>1</td><td>5</td><td>3731</td><td>अमन विहार</td></tr><tr><td>4</td><td>1</td><td>5</td><td>3732</td><td>गंगोत्री विहार</td></tr><tr><td>4</td><td>1</td><td>5</td><td>3733</td><td>सुमन विहार</td></tr><tr><td>4</td><td>1</td><td>5</td><td>3735</td><td>मन्दाकिनी विहार</td></tr><tr><td>4</td><td>1</td><td>5</td><td>3736</td><td>गोविन्द नगर</td></tr><tr><td>4</td><td>1</td><td>5</td><td>3737</td><td>मयूर विहार</td></tr><tr><td>4</td><td>1</td><td>5</td><td>3741</td><td>करनपुर खास (सहस्त्रधारा मार्ग पर स्थित )</td></tr><tr><td>4</td><td>1</td><td>5</td><td>3743</td><td>केवल विहार</td></tr><tr><td>4</td><td>1</td><td>5</td><td>3744</td><td>नालापानी रोड</td></tr><tr><td>4</td><td>1</td><td>5</td><td>3745</td><td>नदी रिस्पना</td></tr><tr><td>4</td><td>1</td><td>5</td><td>3747</td><td>अधोईवाला</td></tr><tr><td>4</td><td>1</td><td>5</td><td>3748</td><td>बिष्णु रोड</td></tr><tr><td>4</td><td>1</td><td>5</td><td>3749</td><td>सेवक आश्रम रोड</td></tr><tr><td>4</td><td>1</td><td>5</td><td>3750</td><td>डी0एल0 रोड</td></tr><tr><td>4</td><td>1</td><td>5</td><td>3751</td><td>बंगाली लाईब्रेरी रोड</td></tr><tr><td>4</td><td>1</td><td>5</td><td>3753</td><td>करनपुर मौहल्ला</td></tr><tr><td>4</td><td>1</td><td>5</td><td>3754</td><td>प्रिन्सिपल रोड</td></tr><tr><td>4</td><td>1</td><td>5</td><td>3755</td><td>नेगी रोड</td></tr><tr><td>4</td><td>1</td><td>5</td><td>3756</td><td>सीमेंट रोड</td></tr><tr><td>4</td><td>1</td><td>5</td><td>3757</td><td>डी0ए0वी0 कालेज रोड</td></tr><tr><td>4</td><td>1</td><td>5</td><td>3758</td><td>बंगाली मौहल्ला</td></tr><tr><td>4</td><td>1</td><td>5</td><td>3760</td><td>एम0डी0डी0ए0 कालोनी, सहस्त्रधारा रोड</td></tr><tr><td>4</td><td>1</td><td>5</td><td>3761</td><td>उप्पल टावर</td></tr><tr><td>4</td><td>1</td><td>5</td><td>3764</td><td>राजेश्वर नगर</td></tr><tr><td>4</td><td>1</td><td>5</td><td>3766</td><td>नैशविला रोड पर काम्बोज स्वीट शॅाप से छोटी बिन्दाल नदी तक</td></tr><tr><td>4</td><td>1</td><td>5</td><td>3767</td><td>राजपुर रोड, करनपुरखास, एंव खेडा मानसिहवाला का वह क्षेत्र जो कि राजपुर रोड से 350 माटर दूरी के बाद स्थित है (अर्थात क्रमांक 1-A-में वणिर्त क्षेत्र को छोड़कर)</td></tr><tr><td>4</td><td>1</td><td>5</td><td>3768</td><td>एम0डी0डी0ए0 कालोनी लोहियापुरम</td></tr><tr><td>4</td><td>1</td><td>5</td><td>3769</td><td>सन्त विनोबा भावे मार्ग (अम्बर पैलेस से बाद)</td></tr><tr><td>4</td><td>1</td><td>5</td><td>3770</td><td>सन्त विनोबा भावे मार्ग (अम्बर पैलेस से पूर्व)</td></tr><tr><td>4</td><td>1</td><td>5</td><td>3771</td><td>त्यागी रोड</td></tr><tr><td>4</td><td>1</td><td>5</td><td>3772</td><td>चन्दर नगर</td></tr><tr><td>4</td><td>1</td><td>5</td><td>3773</td><td>सिक्का ग्रीन</td></tr><tr><td>4</td><td>1</td><td>5</td><td>3774</td><td>रिवर वैली</td></tr><tr><td>4</td><td>1</td><td>5</td><td>3775</td><td>ओर्किड / ओर्चिड पार्क</td></tr><tr><td>4</td><td>1</td><td>5</td><td>3776</td><td>विहस्प्रिंग विलोज</td></tr><tr><td>4</td><td>1</td><td>5</td><td>3777</td><td>पैसिफिक गोल्फ इस्टेट</td></tr><tr><td>4</td><td>1</td><td>5</td><td>3778</td><td>पनाष वैली</td></tr><tr><td>4</td><td>1</td><td>5</td><td>4253</td><td>रैस्ट कैम्प</td></tr><tr><td>4</td><td>1</td><td>5</td><td>6286</td><td>शिव लोक कॉलोनी</td></tr><tr><td>4</td><td>1</td><td>5</td><td>6287</td><td>बद्रीश कॉलोनी</td></tr><tr><td>4</td><td>1</td><td>5</td><td>3780</td><td>धर्मपुर सब्जी मण्डी चौराहे से लक्ष्मी रोड के चौराहे तक सड़क से 100 माटर दूरी तक (नेहरू कालोनी क्षेत्र की ओर पड़ने वाला क्षेत्र)</td></tr><tr><td>4</td><td>1</td><td>5</td><td>3781</td><td>हरिद्वार रोड पर रिस्पना पुल तिराहे से विधान सभा होते हुये रेलवे फाटक तक</td></tr><tr><td>4</td><td>1</td><td>5</td><td>3782</td><td>पो0ओ0 रोड (सुभाष नगर क्षेत्र)</td></tr><tr><td>4</td><td>1</td><td>5</td><td>3783</td><td>टर्नर रोड (क्लेमेनटाउन क्षेत्र)</td></tr><tr><td>4</td><td>1</td><td>5</td><td>3784</td><td>कृष्णा विहार</td></tr><tr><td>4</td><td>1</td><td>5</td><td>3785</td><td>आनन्द विहार</td></tr><tr><td>4</td><td>1</td><td>5</td><td>3786</td><td>इंजीनियर्स इन्कलेव जाखन क्षेत्र</td></tr><tr><td>4</td><td>1</td><td>5</td><td>3787</td><td>दून विहार</td></tr><tr><td>4</td><td>1</td><td>5</td><td>3788</td><td>अंसल ग्रीन वैली</td></tr><tr><td>4</td><td>1</td><td>5</td><td>3789</td><td>भागीरथीपुरम - जाखन क्षेत्र</td></tr><tr><td>4</td><td>1</td><td>5</td><td>3790</td><td>दिलाराम बाजार</td></tr><tr><td>4</td><td>1</td><td>5</td><td>3791</td><td>ओल्ड सर्वे रोड</td></tr><tr><td>4</td><td>1</td><td>5</td><td>3792</td><td>विदेश संचार कालोनी</td></tr><tr><td>4</td><td>1</td><td>5</td><td>3793</td><td>आयकर कालोनी</td></tr><tr><td>4</td><td>1</td><td>5</td><td>3794</td><td>नेहरू कालोनी (सी0 ब्लांक)</td></tr><tr><td>4</td><td>1</td><td>5</td><td>3795</td><td>इन्द्रा मार्केट</td></tr><tr><td>4</td><td>1</td><td>5</td><td>3796</td><td>कचहरी रोड</td></tr><tr><td>4</td><td>1</td><td>5</td><td>3797</td><td>नरदेव शास्त्री मार्ग</td></tr><tr><td>4</td><td>1</td><td>5</td><td>3798</td><td>पंत रोड</td></tr><tr><td>4</td><td>1</td><td>5</td><td>3799</td><td>कॅान्वेन्ट रोड</td></tr><tr><td>4</td><td>1</td><td>5</td><td>3800</td><td>न्यू रोड</td></tr><tr><td>4</td><td>1</td><td>5</td><td>3801</td><td>पटेल रोड</td></tr><tr><td>4</td><td>1</td><td>5</td><td>3802</td><td>अंसारी रोड</td></tr><tr><td>4</td><td>1</td><td>5</td><td>3803</td><td>तिलक रोड</td></tr><tr><td>4</td><td>1</td><td>5</td><td>3805</td><td>इनद्रापुरम</td></tr><tr><td>4</td><td>1</td><td>5</td><td>3806</td><td>चन्द्रलोक कालोनी</td></tr><tr><td>4</td><td>1</td><td>5</td><td>3807</td><td>साकेत कालोनी</td></tr><tr><td>4</td><td>1</td><td>5</td><td>3808</td><td>इन्द्रबाबा मार्ग</td></tr><tr><td>4</td><td>1</td><td>5</td><td>3809</td><td>कश्मीरी कालोनी</td></tr><tr><td>4</td><td>1</td><td>5</td><td>3810</td><td>कोचर कालोनी</td></tr><tr><td>4</td><td>1</td><td>5</td><td>3811</td><td>जज कालोनी</td></tr><tr><td>4</td><td>1</td><td>5</td><td>3812</td><td>डिक रोड</td></tr><tr><td>4</td><td>1</td><td>5</td><td>3813</td><td>उग्र रोड</td></tr><tr><td>4</td><td>1</td><td>5</td><td>3814</td><td>नेमी रोड</td></tr><tr><td>4</td><td>1</td><td>5</td><td>3815</td><td>चन्दर रोड</td></tr><tr><td>4</td><td>1</td><td>5</td><td>3816</td><td>लक्ष्मी रोड</td></tr><tr><td>4</td><td>1</td><td>5</td><td>3817</td><td>कर्जन रोड</td></tr><tr><td>4</td><td>1</td><td>5</td><td>3818</td><td>नेहरू रोड</td></tr><tr><td>4</td><td>1</td><td>5</td><td>3819</td><td>सकुर्लर रोड</td></tr><tr><td>4</td><td>1</td><td>5</td><td>3820</td><td>तेग बहादुर रोड</td></tr><tr><td>4</td><td>1</td><td>5</td><td>3821</td><td>बलवीर रोड</td></tr><tr><td>4</td><td>1</td><td>5</td><td>3822</td><td>मोहिनी रोड</td></tr><tr><td>4</td><td>1</td><td>5</td><td>3823</td><td>प्रीतम रोड</td></tr><tr><td>4</td><td>1</td><td>5</td><td>3824</td><td>इन्दर रोड</td></tr><tr><td>4</td><td>1</td><td>5</td><td>3825</td><td>म्यूनिस्पिल रोड</td></tr><tr><td>4</td><td>1</td><td>5</td><td>3826</td><td>रेसकोर्स</td></tr><tr><td>4</td><td>1</td><td>5</td><td>3827</td><td>डालनवाला क्षेत्र में पड़नें वाले समस्त सड़के तथा मौजा धर्मपुर के अग्रवाल बेकर्स- सब्जी मण्डी से पुलियां नं0- 6  तक की सड़क के उत्तर पूर्व का डालनवाला में पड़ने वाला समस्त क्षेत्र</td></tr><tr><td>4</td><td>1</td><td>5</td><td>3828</td><td>कालीदास रोड</td></tr><tr><td>4</td><td>1</td><td>5</td><td>3829</td><td>न्यू कैन्ट रोड पर कैन्ट सीमा से आगे गढी डाकरा बाजार तक</td></tr><tr><td>4</td><td>1</td><td>5</td><td>3830</td><td>नैशविला रोड पर राजपुर रोड से काम्बोज स्वीट शॉप तक</td></tr><tr><td>4</td><td>1</td><td>5</td><td>3831</td><td>चकराता रोड पर चुक्खुवाला मार्ग,  नारी शिल्प मन्दिर मार्ग,  रामपुर मण्डी रोड (क्रमांक-8-एच-1 में वर्णित क्षेत्र को छोड़कर)</td></tr><tr><td>4</td><td>1</td><td>5</td><td>3832</td><td>लक्ष्मी पार्क जैन कासोनी</td></tr><tr><td>4</td><td>1</td><td>5</td><td>3833</td><td>व्हिस्पिरिंग विलोज</td></tr><tr><td>4</td><td>1</td><td>5</td><td>3834</td><td>शिवम विहार</td></tr><tr><td>4</td><td>1</td><td>5</td><td>3835</td><td>शिप्रा कॉलोनी</td></tr><tr><td>4</td><td>1</td><td>5</td><td>3836</td><td>फ्रेंड्स कॉलोनी</td></tr><tr><td>4</td><td>1</td><td>5</td><td>3837</td><td>प्लेजंट वैली</td></tr><tr><td>4</td><td>1</td><td>5</td><td>3838</td><td>एकता कॉलोनी (अकेटा एवेन्यू)</td></tr><tr><td>4</td><td>1</td><td>5</td><td>3839</td><td>एकता कॉलोनी (अकेटा एवेन्यू)</td></tr><tr><td>4</td><td>1</td><td>5</td><td>3840</td><td>रामलीला बाजार</td></tr><tr><td>4</td><td>1</td><td>5</td><td>3841</td><td>घोसी गली</td></tr><tr><td>4</td><td>1</td><td>5</td><td>3842</td><td>बाबूगंज</td></tr><tr><td>4</td><td>1</td><td>5</td><td>3843</td><td>झण्डा मौहल्ला/बाजार</td></tr><tr><td>4</td><td>1</td><td>5</td><td>3844</td><td>हनुमान चौक</td></tr><tr><td>4</td><td>1</td><td>5</td><td>3845</td><td>मोती बाजार</td></tr><tr><td>4</td><td>1</td><td>5</td><td>3846</td><td>सरनीमल बाजार</td></tr><tr><td>4</td><td>1</td><td>5</td><td>3847</td><td>डिस्पेन्सरी रोड</td></tr><tr><td>4</td><td>1</td><td>5</td><td>3848</td><td>अजमल खॉ रोड</td></tr><tr><td>4</td><td>1</td><td>5</td><td>3849</td><td>राजा रोड</td></tr><tr><td>4</td><td>1</td><td>5</td><td>3850</td><td>दर्शनी गेट/आढ़त बाजार (क्रमांक-8-एच -4/5 में वर्णित क्षेत्र को छोड़कर)</td></tr><tr><td>4</td><td>1</td><td>5</td><td>3851</td><td>पीपल मण्डी (क्रमांक-8-एच -4 में वर्णित क्षेत्र को छोड़कर)</td></tr><tr><td>4</td><td>1</td><td>5</td><td>3852</td><td>धामावाला (क्रमांक-8-एच -4 में वर्णित क्षेत्र को छोड़कर)</td></tr><tr><td>4</td><td>1</td><td>5</td><td>3853</td><td>क्रास रोड</td></tr><tr><td>4</td><td>1</td><td>5</td><td>3854</td><td>न्यू सर्वे रोड</td></tr><tr><td>4</td><td>1</td><td>5</td><td>3855</td><td>जबर क्षेत्र  से आगे नगर पालिका परिषद मसूरी सीमा में दोनों ओर की सम्पत्तियों हेतु ।</td></tr><tr><td>4</td><td>1</td><td>5</td><td>3856</td><td>सिस्टर बाजार से आगे जबर खेत का क्षेत्र मंलिगार गेट से आगे मसूरी-टिहरी रोड पर जवर खेत का क्षेत्र (कम्युनिटी हास्पिटल, बुड स्टाक स्कूल, बुड स्टाक धोबीघाट, के साथ ही इस मार्ग से सम्पत्तियों के पहुच तक के लिए तथा मसूरी-चम्बा टिहरी बाई पास मार्ग की दोनों ओर की सम्पत्तियों हेतु)</td></tr><tr><td>4</td><td>1</td><td>5</td><td>3857</td><td>350 मीटर (मसूरी चकराता रोड) कैम्पटी रोड के पश्चात भिलाडू के सम्पूर्ण क्षेत्र नगर पालिका परिषद, मसूरी सीमा तक</td></tr><tr><td>4</td><td>1</td><td>5</td><td>3858</td><td>लण्ढोर अनुपम होटल से नीचे भण्डारी निवास, रावत हाऊस के पश्चात खच्चरखाना लक्ष्मणपुरी क्षेत्र</td></tr><tr><td>4</td><td>1</td><td>5</td><td>3859</td><td>गांधी द्वारा के किंकेग मोटर मार्ग से 350 मीटर दूरी के पश्चात तथा देहरादून की ओर तथा आई.टी.बी.पी. का क्षेत्र तथा कार्टमेकेन्जी रोड नगर देवता मन्दिर का क्षेत्र गांधी द्वारा तथा उक्त मोटर मार्ग के दोनों ओर की भूमि (थापर टेरस, जय निवास, हुसैन गंज , विल्ला फॉल आदि का सम्पूर्ण क्षेत्र)</td></tr><tr><td>4</td><td>1</td><td>5</td><td>3860</td><td>अनुपम होटल से मंलिगार क्षेत्र चौक तक का पूरा (कैन्ट क्षेत्र)</td></tr><tr><td>4</td><td>1</td><td>5</td><td>3861</td><td>चार्लीविली गेट के नीचे हैप्पी वैली, के साथ ही पोलोग्राउण्ड का सम्पूर्ण  क्षेत्र तथा देवदार रोड होते हुए तिब्बतन होम फाउण्डेसन के साथ ही इस क्षेत्र में नगर पालिका परिषद, मसूरी सीमा तक</td></tr><tr><td>4</td><td>1</td><td>5</td><td>3862</td><td>हाथीपांव व आसपास के क्षेत्र जहां पर खनन कार्य किया जाता था, पार्क एस्टेट, क्लाउड एण्ड जार्ज एवरेस्ट का सम्पूर्ण क्षेत्र ग्राम दुधली तक नगर पालिका परिषद मसूरी सीमान्तर्गत)</td></tr><tr><td>4</td><td>1</td><td>5</td><td>3863</td><td>पिक्चर पैलेस से लण्ढौर बाजार का पूरा क्षेत्र अनुपम होटल तक (बूचडखाना, अनुपम चौक गुरूद्वारा रोड से भण्डारी निवास, रावत हाऊस तक)</td></tr><tr><td>4</td><td>1</td><td>5</td><td>3864</td><td>मसूरी इंटरनेशनल स्कूल सीमा समाप्ति पर उससे आगे कैम्पटी फाल रोड (मसूरी से चकराता) पर नगर पालिका सीमा मसूरी तक के दोनों ओर के भाग के लिए (श्रीनगर इस्टेट)</td></tr><tr><td>4</td><td>1</td><td>5</td><td>3865</td><td>मंलिगार होटल से ऊपर का क्षेत्र 4 दुकान होकर सिस्टर बाजार से दूरदर्शन केन्द्र तक का क्षेत्र चार दुकान से र्सीक वाली कोठी तक का क्षेत्र, र्सीक वाली कोठी से लाल टिब्बा के पिछे की ओर की सड़क का पूरा क्षेत्र</td></tr><tr><td>4</td><td>1</td><td>5</td><td>3866</td><td>कचहरी के उपर एवोलोन गनहिल रोड को जोड़ने वाला तिराहा के पाश्चात का पूरा क्षेत्र सेन्ट मेरी अस्पताल व साहू जैन इस्टेट व पोंदार हाउस के पश्चात का सम्पूर्ण ऊपरी भाग</td></tr><tr><td>4</td><td>1</td><td>5</td><td>3867</td><td>घंघटार लण्ढौर से साउथ रोड होकर  सिविल अस्पताल, वाईन वर्ग ऐलन स्कूल एवं बाला हिसार क्षेत्र (घन्टाघर से बालाहिसार तक जिसे पुराना राजपुर रोड से भी जाना जाता है)</td></tr><tr><td>4</td><td>1</td><td>5</td><td>3869</td><td>जीरो पॉइंट से आगे हरनाम सिंह रोड पर वेवरली कान्वेन्ट स्कूल (काला स्कूल गेट) से पूर्व का सम्पूर्ण क्षेत्र</td></tr><tr><td>4</td><td>1</td><td>5</td><td>3870</td><td>चार्लीविला गेट से डिक रोड होकर कम्पनी बाग, लौगी गार्डन, होलो ओक का सम्पूर्ण क्षेत्र</td></tr><tr><td>4</td><td>1</td><td>5</td><td>3871</td><td>नगर पालिका परिषद, मसूरी में सम्मिलित ग्राम मिसरासपट्टी का क्षेत्र</td></tr><tr><td>4</td><td>1</td><td>5</td><td>3872</td><td>भट्टा गॉव नगर पालिका सीमा के अन्दर का भाग के लिए मार्ग के दोनों ओर के भाग (देहरादून- मसूरी मार्ग हेतु निर्धारित 350 मीटर दूरी को छोड़ कर)</td></tr><tr><td>4</td><td>1</td><td>5</td><td>3873</td><td>होटल सेवेन ओक्स से आगे कैमल्स बैक रोड पर बहुगुणा पार्क से पूर्व तक (मार्ग के दोनों ओर पहुच सम्पत्तियों तक के लिए</td></tr><tr><td>4</td><td>1</td><td>5</td><td>3874</td><td>कम्पनी बाग लौगी गार्डेन के पश्चात हाथी पांव चौक तक</td></tr><tr><td>4</td><td>1</td><td>5</td><td>3875</td><td>घोबीघाट मसूरी झील के पश्चात ग्राम भट्टा तक नगर पालिका परिषद मसूरी सीमा में (देहरादून- मसूरी मार्ग हेतु निर्धारित 350 मीटर दूरी को छोड़ कर)</td></tr><tr><td>4</td><td>1</td><td>5</td><td>3876</td><td>बड़े मोड के अंतिम छोर के पाश्चात से किंकेग मोटर मार्ग पर दोनों ओर 350 मीटर की परिधि में किंकेग से नीचे घनानन्द रा.इ.का. के पश्चात देहरादून की ओर धोबीघाट का क्षेत्र नगर पालिका परिषद, मसूरी सीमा अन्तर्गत कीलिफ़ हाल इस्टेट का सम्पूर्ण क्षेत्र)</td></tr><tr><td>4</td><td>1</td><td>5</td><td>3877</td><td>राधा भवन इस्टेट, मुख्य भाग से आगे की ओर गुरूनानक स्कूल से सड़क से ऊपरी भाग न्यू सर्कुलर रोड से मानव भारती संगीला एस्टेट क्षेत्र कम्पनी बाग उपरी क्षेत्र वेवरली कान्वेंट स्कूल (काला स्कूल) गेट तक</td></tr><tr><td>4</td><td>1</td><td>5</td><td>3878</td><td>लाइब्रेरी चौक से होटल क्लासिक तथा लाइब्रेरी बस स्टैन्ड से नीचे की ओर 350 मीटर दूरी के पश्चात मुख्य मेनर हाउस भवन तथा सर्कुलर रोड एवं सप्रिंग रोड मोतीलाल नहरू रोड से लेकर सम्पूर्ण चमर खण्ड का क्षेत्र, मैकनेन पम्प क्षेत्र, ऐस्टल इस्टेट का सम्पूर्ण क्षेत्र, आई0टी0बी0पी0 गेट से पहले तक</td></tr><tr><td>4</td><td>1</td><td>5</td><td>3879</td><td>चकराता रोड पर सा0नि0वि0 निरीक्षण भवन मसूरी के क्षेत्र से आगे चकराता टोल में मसूरी इंटरनेशल स्कूल तक पोलो ग्राउन्ड क्षेत्र तक 100 मीटर रोड क्षेत्र की ओर(श्रीनगर इस्टेट)</td></tr><tr><td>4</td><td>1</td><td>5</td><td>3880</td><td>झडीपानी क्षेत्र (ओकग्रोव स्कूल का क्षेत्र, झडीपानी टोल के साथ ही राजपुर पुराना टोल नगर पालिका परिषद, मसूरी सीमान्तर्गत)</td></tr><tr><td>4</td><td>1</td><td>5</td><td>3881</td><td>बार्लोगंज क्षेत्र (जेपी बैड से बार्लोगंज मार्ग की सम्पूर्ण सम्पत्तियों हेतु, बालाहिसार मार्ग पर बालाहिसार के पश्चात सम्पूर्ण मैरीविल एस्टेट, भट्टा गॉव नगर पालिका सीमा तक, देहरादून-मसूरी मार्ग हेतु निर्धारित 350 मीटर दूरी को छोड़कर सम्पूर्ण बार्लोगंज-झडीपानी मार्ग पर स्थित भूमि भवन जो नगर पालिका परिषद मसूरी की सीमा के अन्तर्गत हो)</td></tr><tr><td>4</td><td>1</td><td>5</td><td>3882</td><td>लाइब्रेरी चौक से आगे मोतीलाल नहरू मार्ग पर दोनो ओर पहुच मार्ग (काला स्कूल) वेवरली कान्वेंट स्कूल तक का क्षेत्र ।</td></tr><tr><td>4</td><td>1</td><td>5</td><td>3883</td><td>मसूरी मार्डन स्कूल तिराहे से राधा भवन मसूरी मुख्य भवन से होते हुए मान काटेज, बडौदा हाऊस चण्डालगढी क्षेत्र एवं विन्सेट हिल का सम्पूर्ण ऊपरी क्षेत्र</td></tr><tr><td>4</td><td>1</td><td>5</td><td>6288</td><td>पिक्चरपैलेस के ऊपर नगर पालिका परिषद कार्यालय मसूरी, हिमालय क्लब नान पारा हो कर आर एन भार्गव इंटर कॉलेज मार्ग होते हुये वाइन वर्ग एलेन स्कूल प्राइमरी सेक्शन तक तथा घंटा घर से ओकबुश रोड होते हुये</td></tr><tr><td>4</td><td>1</td><td>5</td><td>3884</td><td>इन्द्राभवन से आगे चार्लीविली गेट तक (साथ ही इस मार्ग से सम्पत्तियों तक की पहुच हेतु)</td></tr><tr><td>4</td><td>1</td><td>5</td><td>3885</td><td>लाईब्रेरी चौक के बाद आगे इन्द्रा भवन तक (होटल ओएसेज मार्ग, गाडीखाना, सेवाय होटल स्टाफ क्वाटर्स का भाग, इन्दिरा भवन आदि के साथ ही इस मार्ग से सम्पत्तियों तक की पहुच हेतु)</td></tr><tr><td>4</td><td>1</td><td>5</td><td>3886</td><td>माल रोड पर रोजलीन होटल से होते हुए कैमल बैक रोड पर बहुगुणा पार्क तक का भाग (प्राईमरी पाठशाला लाईब्रेरी भिलाडू मार्ग पर मित्तल हाउस व धर निवास आदि तक का अन्तिम भाग )</td></tr><tr><td>4</td><td>1</td><td>5</td><td>3887</td><td>लाइब्रेरी चौक से संपूर्ण माल रोड कुलड़ी बाज़ार, जफर हाल , स्टुडियो लौज़, तिलक मार्ग , बारह कैंची पर डॉक्टर ठुकराल के आगे वाले किंक्रग की ओर वाले बंद तक सड़क के दोनों ओर 50 मीटर तक कैमल बैंक रोड पर होटल नन्द विला एवं होटल सोलिटेयर प्लाज़ा तक (दुग्गल विला का गुनसोला निवास दुग्गल विला कॉटेज, रोज़लीन होटल से कालाकाकर हाउस एवम चर्च रोड पर पोदार हाउस आदि तक का भाग, कचहरी रोड पर एवलॉन-गनहिल मार्ग को जोड़ने वाला तिराहा, हैकमन्स होटल मे शगुन पैलेस, घोडा लाइन, हम्पटन कोर्ट, क्रेग कालिज आदि के साथ ही एस्टेला कालिज, लॉलर बैक, तिब्बतन मार्केट मार्ग पर इन्दर निवास पदमनी आदि के साथ ही वासू सिनेमा बिल्डिंग आदि)</td></tr><tr><td>4</td><td>1</td><td>5</td><td>3991</td><td>डोईवाला टाउन एरिया का शेष क्षेत्र0</td></tr><tr><td>4</td><td>1</td><td>5</td><td>3992</td><td>डोईवाला चौक से शुगर मिल प्रेम नगर बाज़ार चादमारी चौक तक</td></tr><tr><td>4</td><td>1</td><td>5</td><td>3993</td><td>डोईवाला चौक से रेल्वे स्टेशन रोड पर रेल्वे स्टेशन तक</td></tr><tr><td>4</td><td>1</td><td>5</td><td>3994</td><td>डोईवाला चौक से देहारादून रोड पर टाउन एरिया सीमा समाप्ती तक</td></tr><tr><td>4</td><td>1</td><td>5</td><td>3995</td><td>डोईवाला चौक से ऋषिकेश रोड पर सौंग नदी तक</td></tr><tr><td>4</td><td>1</td><td>5</td><td>3996</td><td>मारखम ग्रन्ट- ।</td></tr><tr><td>4</td><td>1</td><td>5</td><td>3997</td><td>मिस्सरवाला खुर्द</td></tr><tr><td>4</td><td>1</td><td>5</td><td>3999</td><td>हंसूवाला</td></tr><tr><td>4</td><td>1</td><td>5</td><td>4000</td><td>डोईवाला</td></tr><tr><td>4</td><td>1</td><td>5</td><td>4001</td><td>घिसरपड़ी</td></tr><tr><td>4</td><td>1</td><td>5</td><td>4002</td><td>मिस्सरवाला कलां</td></tr><tr><td>4</td><td>1</td><td>5</td><td>4003</td><td>लच्छीवाला</td></tr><tr><td>4</td><td>1</td><td>5</td><td>4004</td><td>डैशवाला</td></tr><tr><td>4</td><td>1</td><td>5</td><td>4005</td><td>गुजरमी</td></tr><tr><td>4</td><td>1</td><td>5</td><td>4006</td><td>जगातखाना, जगातखाना करनपुर</td></tr><tr><td>4</td><td>1</td><td>5</td><td>4007</td><td>डोमगांव</td></tr><tr><td>4</td><td>1</td><td>5</td><td>4008</td><td>भंडारीवाला मयचक</td></tr><tr><td>4</td><td>1</td><td>5</td><td>4009</td><td>मंगलूवाला</td></tr><tr><td>4</td><td>1</td><td>5</td><td>6289</td><td>भण्डारी वाला</td></tr><tr><td>4</td><td>1</td><td>5</td><td>4010</td><td>विजयपुर गोपीवाला</td></tr><tr><td>4</td><td>1</td><td>5</td><td>4011</td><td>लाडपुर</td></tr><tr><td>4</td><td>1</td><td>5</td><td>4012</td><td>गुजराडा मानसिंह</td></tr><tr><td>4</td><td>1</td><td>5</td><td>4013</td><td>आरकेडिया ग्रांट</td></tr><tr><td>4</td><td>1</td><td>5</td><td>4014</td><td>नवादा</td></tr><tr><td>4</td><td>1</td><td>5</td><td>4015</td><td>नथुवावाला</td></tr><tr><td>4</td><td>1</td><td>5</td><td>4016</td><td>चंद्रबनी ग्रांट</td></tr><tr><td>4</td><td>1</td><td>5</td><td>4017</td><td>चकतुनवाला</td></tr><tr><td>4</td><td>1</td><td>5</td><td>4018</td><td>चकरायपुर</td></tr><tr><td>4</td><td>1</td><td>5</td><td>4019</td><td>दानियों का डांडा</td></tr><tr><td>4</td><td>1</td><td>5</td><td>4020</td><td>सेवलाखुर्द</td></tr><tr><td>4</td><td>1</td><td>5</td><td>4021</td><td>सुन्दरवाला</td></tr><tr><td>4</td><td>1</td><td>5</td><td>4022</td><td>सौन्धोवाली ,सौन्धोवाली धौरन</td></tr><tr><td>4</td><td>1</td><td>5</td><td>4023</td><td>रायपुर</td></tr><tr><td>4</td><td>1</td><td>5</td><td>4024</td><td>हर्रावाला</td></tr><tr><td>4</td><td>1</td><td>5</td><td>4025</td><td>हरभजवाला</td></tr><tr><td>4</td><td>1</td><td>5</td><td>4026</td><td>हरबंश वाला</td></tr><tr><td>4</td><td>1</td><td>5</td><td>4027</td><td>हरिपुर</td></tr><tr><td>4</td><td>1</td><td>5</td><td>4028</td><td>सिनौला</td></tr><tr><td>4</td><td>1</td><td>5</td><td>4029</td><td>पित्थूवाला</td></tr><tr><td>4</td><td>1</td><td>5</td><td>4030</td><td>मियांवाला</td></tr><tr><td>4</td><td>1</td><td>5</td><td>4031</td><td>किरसाली पछवादून</td></tr><tr><td>4</td><td>1</td><td>5</td><td>4032</td><td>मेहुवाला माफी</td></tr><tr><td>4</td><td>1</td><td>5</td><td>4033</td><td>माजरी माफी</td></tr><tr><td>4</td><td>1</td><td>5</td><td>4034</td><td>मोहकमपुर कलां</td></tr><tr><td>4</td><td>1</td><td>5</td><td>4035</td><td>मोहकमपुर खुर्द</td></tr><tr><td>4</td><td>1</td><td>5</td><td>4036</td><td>मोहब्बेवाला</td></tr><tr><td>4</td><td>1</td><td>5</td><td>4037</td><td>मक्कावाला</td></tr><tr><td>4</td><td>1</td><td>5</td><td>4038</td><td>कुवांवाला</td></tr><tr><td>4</td><td>1</td><td>5</td><td>4039</td><td>कुठाल गांव</td></tr><tr><td>4</td><td>1</td><td>5</td><td>4040</td><td>आसारोडी</td></tr><tr><td>4</td><td>1</td><td>5</td><td>4041</td><td>चन्द्रबनी</td></tr><tr><td>4</td><td>1</td><td>5</td><td>4042</td><td>चन्द्रबनी खालसा</td></tr><tr><td>4</td><td>1</td><td>5</td><td>4043</td><td>विजयपुर हाथीबड़कला</td></tr><tr><td>4</td><td>1</td><td>5</td><td>4044</td><td>मिटठी भेडी</td></tr><tr><td>4</td><td>1</td><td>5</td><td>4045</td><td>मरेठा</td></tr><tr><td>4</td><td>1</td><td>5</td><td>4046</td><td>कुल्हान करनपुर</td></tr><tr><td>4</td><td>1</td><td>5</td><td>4047</td><td>कुल्हान मानसिंह</td></tr><tr><td>4</td><td>1</td><td>5</td><td>4048</td><td>सोन्धोवाली मानसिंह</td></tr><tr><td>4</td><td>1</td><td>5</td><td>4049</td><td>नागल हटनाला</td></tr><tr><td>4</td><td>1</td><td>5</td><td>4050</td><td>हटनाल गांव</td></tr><tr><td>4</td><td>1</td><td>5</td><td>4051</td><td>आमवाला करनपुर</td></tr><tr><td>4</td><td>1</td><td>5</td><td>4052</td><td>कालागांव</td></tr><tr><td>4</td><td>1</td><td>5</td><td>4053</td><td>चांलग</td></tr><tr><td>4</td><td>1</td><td>5</td><td>4054</td><td>आमवाला उपरला</td></tr><tr><td>4</td><td>1</td><td>5</td><td>4055</td><td>आमवाला मझला</td></tr><tr><td>4</td><td>1</td><td>5</td><td>4056</td><td>किरसाली परवादून</td></tr><tr><td>4</td><td>1</td><td>5</td><td>4057</td><td>तरलानांगल</td></tr><tr><td>4</td><td>1</td><td>5</td><td>4058</td><td>ननूरखेडा</td></tr><tr><td>4</td><td>1</td><td>5</td><td>4059</td><td>बालावाला</td></tr><tr><td>4</td><td>1</td><td>5</td><td>4060</td><td>बगराल गांव</td></tr><tr><td>4</td><td>1</td><td>5</td><td>6290</td><td>नकरौंदा</td></tr><tr><td>4</td><td>1</td><td>5</td><td>6291</td><td>जोहड़ी</td></tr><tr><td>4</td><td>1</td><td>5</td><td>6292</td><td>मोथरोंवाला</td></tr><tr><td>4</td><td>1</td><td>5</td><td>4061</td><td>भंडारगाँव</td></tr><tr><td>4</td><td>1</td><td>5</td><td>4062</td><td>खुरावा</td></tr><tr><td>4</td><td>1</td><td>5</td><td>4063</td><td>खाला गांव</td></tr><tr><td>4</td><td>1</td><td>5</td><td>4064</td><td>आमवाला तरला</td></tr><tr><td>4</td><td>1</td><td>5</td><td>4065</td><td>नत्थनपुर</td></tr><tr><td>4</td><td>1</td><td>5</td><td>4066</td><td>डांडा नूरीवाला</td></tr><tr><td>4</td><td>1</td><td>5</td><td>4067</td><td>डांडा लखौण्ड</td></tr><tr><td>4</td><td>1</td><td>5</td><td>4068</td><td>डांडा खुदानेवाला</td></tr><tr><td>4</td><td>1</td><td>5</td><td>4069</td><td>डांडा धोरण</td></tr><tr><td>4</td><td>1</td><td>5</td><td>4070</td><td>सेवलाकलां</td></tr><tr><td>4</td><td>1</td><td>5</td><td>4071</td><td>भारुवालाग्रान्ट</td></tr><tr><td>4</td><td>1</td><td>5</td><td>4072</td><td>मासली</td></tr></tbody></table>

\
\
