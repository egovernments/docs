# Navigation Between Old & New UI

## **Problem Statement**

Since not all modules are in the new UI, and the user has access to modules in both the new and old UI, navigating between them creates confusion. So framework needs to be designed to avoid this confusion.

## **Solution**

The default landing page will be that of the new UI home screen for a user

1. When the user is on a module that is in old UI (eg: Fire NOC) and clicks on the \{{Home\}} screen button from the sidebar, then the screen should be navigated to the New UI Home screen
2. When the user is on a module that is in the new UI, then clicking on the \{{Home\}} button should redirect to the new UI home screen.
3. There will be no changes in the side panel and it will remain the same for the respective new UI or old UI
4. This change will be applicable to both citizen-side and employee-side interfaces

## **Technical Implementation:**

* As per the Requirement, the changes were made in both old and new UIs such that always **Home/ Landing** screen will be **New UI Landing Screen**. (This is applicable in both citizen and employee Screens )
* So the old UI Home screen will be always redirected to New UI.
* To access the Old UI Modules, you can access them through Sidebar navigation links.\
  Check this link to add a sidebar link for navigation [Citizen Home screen card | How cards are rendered along with links and icons:](https://digit-discuss.atlassian.net/wiki/spaces/DD/pages/2100658177/Citizen+Home+screen+card#How-cards-are-rendered-along-with-links-and-icons%3A) and [Mdms UI configurations](https://digit-discuss.atlassian.net/wiki/spaces/EGR/pages/122290485)
* To configure any sidebar link to navigate to Old UI citizen as follow

```
 {
      "id": 2367,
      "name": "FirenocCitizen",
      "url": "digit-ui-card",
      "displayName": "FireNoc Search",
      "orderNumber": 1,
      "parentModule": "FireNoc",
      "enabled": true,
      "serviceCode": "",
      "code": "",
      "path": "",
      "navigationURL": "/citizen/fire-noc/home",
      "leftIcon": "FirenocIcon",
      "rightIcon": "",
      "queryParams": "",
      "sidebar": "digit-ui-links",
      "sidebarURL": "/citizen/fire-noc/home"
    }
```

and employees as follows:

```
 {
      "id": 1800,
      "name": "FIRE-NOC",
      "url": "url",
      "displayName": "Search",
      "orderNumber": 3,
      "parentModule": "",
      "enabled": true,
      "serviceCode": "FIRE-NOC",
      "code": "null",
      "navigationURL": "fire-noc/search",
      "path": "FIRE-NOC.Search",
      "leftIcon": "social:people"
    },
```

The following commit has to be added

[<img src="https://github.com/fluidicon.png" alt="" data-size="line">RAIN-7250 :: Navigation of Old and New UI Changes incorporated · egovernments/DIGIT-OSS@1ea152e](https://github.com/egovernments/DIGIT-OSS/commit/1ea152e5a485aa16794f8236a019bebaf11a81b6)

[<img src="https://github.com/fluidicon.png" alt="" data-size="line">RAIN-7250 : Added the Action for Firenoc to Digit-ui Citizen · egovernments/egov-mdms-data@bfe73a9](https://github.com/egovernments/egov-mdms-data/commit/bfe73a9dc4906aa0e0b3f4c41717fd2240046284)

[<img src="https://github.com/fluidicon.png" alt="" data-size="line">RAIN-7250 :: Birth and death module navigation added to new ui sidebar · egovernments/egov-mdms-data@5944135](https://github.com/egovernments/egov-mdms-data/commit/594413581175369c3192dc7034136812cc887d9d)\
[<img src="https://github.com/fluidicon.png" alt="" data-size="line">RAIN-7250 : Added the Action for Birth & death of Digit-ui Citizen · egovernments/egov-mdms-data@dccfceb](https://github.com/egovernments/egov-mdms-data/commit/dccfcebcceaab3e0742d4fe3a77a1b23494c6d55#diff-d15069f48cf5be0f57ddf304ea349e7606f67f8f223b1bf56bb528332e1c9943)\
