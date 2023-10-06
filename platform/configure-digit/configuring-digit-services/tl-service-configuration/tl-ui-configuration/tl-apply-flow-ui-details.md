# TL Apply Flow UI Details

**Objective:** To provide the facility for the user to create a trade license application for the current year by citizen users or counter employees.

## Workflow Details

<div align="left">

<img src="../../../../../.gitbook/assets/image (198) (1).png" alt="TL Home Card">

</div>

#### **Apply for Trade License**

Users can apply for a trade license application by clicking on the Apply for Trade License button. Users can add all the information as per the questions asked across the workflow. The summary screen at the end of the flow displays all details for review. Users can click on the submit button after review. The application for a trade license is created for the current financial year.

**Apply Flow** - The trade license registration screen is displayed after login which helps users identify the documents required to apply for a trade license. A citizen info card at the bottom of the page displays any additional information about the maximum size of the file that can be uploaded.

<div align="left">

<img src="../../../../../.gitbook/assets/image (207) (3).png" alt="Information Screen">

</div>

**Trade License Details/Assessment Flow -** This flow captures the trade-specific information required for registering the trade.&#x20;

Trade Name - The user provides the name of the trade. An info card is displayed at the bottom of the screen stating that the license will be issued for the current financial year. The financial year value is retrieved from the MDMS.

<div align="left">

<img src="../../../../../.gitbook/assets/image (263) (1).png" alt="">

</div>

Structure Type - The users can select yes or no based on whether the trade has mobility or not. If yes, the next screen prompts you to enter the vehicle type. If no, the next screen moves to the building type page.

<div align="left">

<img src="../../../../../.gitbook/assets/image (238) (5).png" alt="">

</div>

Vehicle Type / Building Type - The options for vehicle and building type are fetched from the MDMS. The Building Type screen displays an information card about the pucca or kuccha options.

<div align="left">

<img src="../../../../../.gitbook/assets/image (193) (3).png" alt="Vehicle Type">

</div>

<div align="left">

<img src="../../../../../.gitbook/assets/image (243) (1).png" alt="Building Type">

</div>

Commencement Date - It defines the date on which the trade started or will start in the future.

<div align="left">

<img src="../../../../../.gitbook/assets/image (202) (1).png" alt="">

</div>

Trade Units - Users must provide the trade category as either goods or services. Based on the selected option the Trade Type is loaded from the MDMS as a drop-down list. The trade sub-type options are loaded based on the selected trade type. The unit of measure and UOM value get pre-populated from the MDMS as per the options selected above.

Users must enter at least one unit to move forward. Clicking on Add More Unit option enables users to enter additional units. Clicking on the delete icon on the top right corner of the unit card removes the unit.

<div align="left">

<img src="../../../../../.gitbook/assets/image (175) (1).png" alt="">

</div>

<div align="left">

<img src="../../../../../.gitbook/assets/image (155) (1).png" alt="">

</div>

Accessories - The Accessory page inquires if there are any accessories required for the business. Accessories may not be compulsory for all trades. If yes, it will move to the accessory details page. If not, it will skip it altogether and will load the address flow.

<div align="left">

<img src="../../../../../.gitbook/assets/image (182) (7).png" alt="">

</div>

Accessory details - The options for accessories are retrieved from the MDMS. The Unit of Measure or UOM is pre-populated and cannot be edited. The users can edit the UOM value and the accessory count. In some cases, these are pre-populated from the MDMS. Clicking on Add More Trade Accessory button allows users to add multiple accessories.

<div align="left">

<img src="../../../../../.gitbook/assets/image (161) (1).png" alt="">

</div>

#### TL Enhanced Flow

If the citizen selects Movable as the structure type in the previous screens, then the flow will jump to the owner details flow. Here the Same as Property Owner’s check box will not be visible.

If the citizen selects Immovable as the structure type then the user is allowed to add the property details. Once the property is added, the flow will redirect to the owner details flow where the Same as Property Owner check box is displayed. If the user checks it, the following details get auto-populated and the screen skips to the proof of Identity page.

![](<../../../../../.gitbook/assets/image (135).png>)

**Common PT integration with TL:** After entering the trade details, users have the option to either search and integrate the already created property or create new lightweight property data for the trade license. This step can be skipped and users can proceed with the normal address details flow.

Once a property is selected user can see the details of the property on the property details page. Refer to the [Common PT ](../../property-tax-service/common-pt.md)document for more details.

![](<../../../../../.gitbook/assets/Screenshot from 2022-05-20 16-51-00.png>)![](<../../../../../.gitbook/assets/Screenshot from 2022-05-20 16-54-09.png>)\


![](<../../../../../.gitbook/assets/Screenshot from 2022-05-20 16-54-32.png>)![](<../../../../../.gitbook/assets/Screenshot from 2022-05-20 16-54-53.png>)

**Address Details Flow -** In the next flow, users have to enter the trade address details. This flow is straightforward, without any conditional routing.

![](<../../../../../.gitbook/assets/image (117) (5).png>)

<div align="left">

<img src="../../../../../.gitbook/assets/image (203) (7).png" alt="">

</div>

Users can pinpoint the location in the Geo-location map, according to which pin code and city, as well as locality, is auto-filled.

**Owner Details Flow -** Finally, the users need to enter the trade owner details. Ownership can be Single or Multiple Owners. According to which the details are filled.

In the case of single/multiple owners, the following screen is displayed. The remaining flows remain the same.

<div align="left">

<img src="../../../../../.gitbook/assets/image (223) (1).png" alt="">

</div>

Users can add multiple owners by clicking on the add owner button - a similar functionality as in trade units and accessories. The Add Owner button is not visible in case the user selects a single owner on the previous page.

The user must provide the owner's primary address and upload three documents that include address proof, owner identity and owner photograph.

![](<../../../../../.gitbook/assets/image (250).png>)

**Check Page and Acknowledgement Screen -** Users can cross-verify the data entered throughout the flow in the Check page. Clicking on the change option adjacent to the data fields allows users to make any changes or updates to the data. The user is redirected back to a corresponding information page and the entire flow is repeated once again to submit the application.&#x20;

The Applying of Trade License Create API is called. Create API snippet:`1create: "/tl-services/v1/_create"`

If the API response is successful, then the Acknowledgement Screen is displayed, otherwise Failed Acknowledgement Screen is displayed.

<div align="left">

<img src="../../../../../.gitbook/assets/image (186) (1).png" alt="">

</div>

<div align="left">

<img src="../../../../../.gitbook/assets/image (205) (5).png" alt="">

</div>

Clicking on the Download Acknowledgement Form button downloads the PDF copy of the acknowledgement.

<div align="left">

<img src="../../../../../.gitbook/assets/image (247).png" alt="">

</div>

## **Release 2.8 Enhancements & Changes**

On the Trade Units page, values for trade type and trade subtype have been loaded by the following MDMS call:

{% code lineNumbers="true" %}
```
const { isLoading, data: Data = {} } = Digit.Hooks.tl.useTradeLicenseMDMS(stateId, "TradeLicense", "TradeUnits", "[?(@.type=='TL')]");
```
{% endcode %}

The following validations have been added for the same :

When users select trade type and then subtype, it is compared with the available billing slab. The hook for this is given below. In case the billing slab is not there it will not allow users to move forward and an error message is displayed.

{% code lineNumbers="true" %}
```
const { data: billingSlabTradeTypeData, isLoading : isBillingSlabLoading } = Digit.Hooks.tl.useTradeLicenseBillingslab({ tenantId: tenantId, filters: {} }, {
    select: (data) => {
    return data?.billingSlab.filter((e) => e.tradeType && e.applicationType === "NEW" && e.licenseType === "PERMANENT" && e.uom);
    }});
```
{% endcode %}

![](<../../../../../.gitbook/assets/image (395).png>)

Once the correct trade type and subtype are added and the correct billing slab is there, the UOM value validation is added. This checks the value in the given range, mentioned in the billing slab object and displays an error if the value is outside of the range.

![](<../../../../../.gitbook/assets/image (387).png>)

## **Technical Implementation Details**

All screens are developed using the new-UI structure followed previously in FSM, PGR and PT, except for multi-component.

The link for the Apply Trade License Main Index is given here and it helps understand the starting point of the flow: [https://github.com/egovernments/DIGIT-Dev/blob/master/frontend/micro-ui/web/micro-ui-internals/packages/modules/tl/src/pages/citizen/Create/index.js](https://github.com/egovernments/DIGIT-Dev/blob/master/frontend/micro-ui/web/micro-ui-internals/packages/modules/tl/src/pages/citizen/Create/index.js)

The TL (Trade License) module is segregated into a specified structure. The screen configuration is inside the PageComponent folder, and the configuration for routing of the pages are mentioned under the config folder which is common for both citizen users and employees. Below is the snippet for folder structure and routing configuration.

<div align="left">

<img src="../../../../../.gitbook/assets/image (265) (1).png" alt="">

</div>

```
export const newConfig = [
  {
    head: "",
    body: [
      {
        type: "component",
        component: "TLInfoLabel",
        key: "tradedetils1",
        withoutLabel: true,
        hideInCitizen: true,
      }
    ]
  },
```

The pages folder is where the high-level configuration for controlling the whole flow is mentioned, for citizens and employees. Citizen flows include Create, Edit Trade, Renewal, Applications and Search Trade. The index or the starting point of the entire flow is available in this folder.

In the Accessory-details page, the Billing slab search API `"/tl-calculator/billingslab/_search"` is called. This returns the array list of all the accessories for which the billing slab has been configured. If the response returns an empty array then the options are curated from the MDMS API mentioned in the MDMS data section.

After completing the flow the user can download the acknowledgement PDF form of the License created.  PDF generation config link: [https://github.com/egovernments/digit-ui-internals/blob/main/packages/modules/tl/src/utils/getTLAcknowledgementData.js](https://github.com/egovernments/digit-ui-internals/blob/main/packages/modules/tl/src/utils/getTLAcknowledgementData.js)

The Utils folder basically contains all the methods used throughout the TL module. Additional common methods can be imported and added to this folder.&#x20;

For creating an application the Create API from Trade License is called using the React hooks. This is declared in the hooks/elements/TL as TLService.

## **MDMS Data**

There are multiple pages within the workflows where data is imported from the MDMS. The table below lists the pages .js files for distinct page components.

| PageComponent            | MDMS Detail                                                    | Module Details Name | Master-Detail Name    |
| ------------------------ | -------------------------------------------------------------- | ------------------- | --------------------- |
| TradeLicense             | List of documents required for registration                    | `TradeLicense`      | `Documents`           |
| SelectTradeName          | Current Financial Year                                         | `egf-master`        | `FinancialYear`       |
| SelectVehicleType        | Type of mobility trade                                         | `common-masters`    | `StructureType`       |
| SelectBuildingType       | Type of Steady Trade                                           | `common-masters`    | `StructureType`       |
| SelectTradeUnits         | List of trade category and its corresponding type and sub-type | `TradeLicense`      | `TradeType`           |
| SelectAccessoriesDetails | Lit of Accessory and its Unit of measure and UOM value         | `TradeLicense`      | `AccessoriesCategory` |
| TLSelectAddress          | List of cities and its corresponding localities                | `TradeLicense`      | `tenants`             |
| SelectOwnerShipDetails   | categories imported are single and multiple owner.             | `common-masters`    | `OwnerShipCategory`   |
| SelectOwnerDetails       | List of Gender options.                                        | `common-masters`    | `GenderType`          |

React Hooks are used to call MDMS data that is shared across the modules. Below is the code snippet for the MDMS call.

```
const { isLoading, data: Documentsob = {} } = Digit.Hooks.tl.useTradeLicenseMDMS(stateId, "TradeLicense", "TLDocuments");
```

## **Localization**

Localization keys are added to the ‘_rainmaker-tl_’ locale module. In future, if any new labels are implemented in the Trade License (Citizen) it is pushed to the locale DB in the _rainmaker-tl_ locale module. Below is an example of a few locale labels.

<div align="left">

<img src="../../../../../.gitbook/assets/image (158) (1).png" alt="">

</div>

## **API Role Action Mapping**

| API                                   | Action ID | Roles     |
| ------------------------------------- | --------- | --------- |
| `/egov-mdms-service/v1/_search`       | `954`     | `CITIZEN` |
| `/tl-services/v1/_create`             | `1685`    | `CITIZEN` |
| `/filestore/v1/files/url`             | `1528`    | `CITIZEN` |
| `/billing-service/bill/v2/_fetchbill` | `1862`    | `CITIZEN` |
| `/tl-calculator/billingslab/_search`  | `1684`    | `CITIZEN` |
| `/tl-services/v1/_update`             | `1686`    | `CITIZEN` |
| `/localization/messages/v1/_search`   | `1531`    | `CITIZEN` |

