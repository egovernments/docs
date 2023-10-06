# Notification Enhancement For Different Channels

## Overview <a href="#overview" id="overview"></a>

Configuration of the notification messages for a business service based on the channel for the same event.

## **Key Functionalities** <a href="#key-functionalities" id="key-functionalities"></a>

* For a specific action of the user, he/she will get an SMS and email as an acknowledgement.
* Users can get SMS, Event, and email based on different channels.
* The application allows one to either send different messages across all channels based on their actions.

## **Enhancement Details** <a href="#details-of-enhancement" id="details-of-enhancement"></a>

* To have this functionality for different business services, a channel names file was created and added to the MDMS data.&#x20;
* It contains information about the combination of different actions and channels for a particular business service. Example -

```
 "channelList": [
 {   "businessService": "PT.CREATE",
     "module": "PT",
     "action" : "OPEN",
     "channelNames": ["SMS", "EMAIL", "EVENT"]
 },
 {
      "businessService": "BPA.CREATE",
      "module": "BPA",
      "action" : "SENDBACKTOCITIZEN",
      "channelNames": ["SMS", "EMAIL", "EVENT"]
  },
  {
      "businessService": "NewTL",
      "module": "TL",
      "action": "FORWARD",
      "channelNames": ["SMS", "EMAIL", "EVENT"]
  },
  {
      "businessService": "WS.CREATE",
      "module": "WS",
      "action" : "ACTIVATE_CONNECTION",
      "channelNames": ["SMS", "EMAIL", "EVENT"]
  },
   {
      "businessService": "SW.CREATE",
      "module": "SW",
      "action" : "APPROVE_CONNECTION",
      "channelNames": ["SMS", "EMAIL", "EVENT"]
    },
  {	
      "businessService": "MCOLLECT.CREATE",	
      "module": "MCOLLECT",	
      "action" : "CREATE",	
      "channelNames": ["SMS", "EMAIL", "EVENT"]	
    },  
    {	
      "businessService": "PGR",	
      "module": "PGR",	
      "action" : "INITIATE",	
      "channelNames": ["SMS", "EMAIL", "EVENT"]	
    },
    {
      "businessService": "WS.CREATE",
      "module": "WS",
      "action" : "EXECUTE_DISCONNECTION",
      "channelNames": ["SMS", "EMAIL", "EVENT"]
    }
]
```

The different channels are

* SMS: ID (Mobile Number)
* Event&#x20;
* Email: ID (Email ID)

This feature enabled the functionality which would first check for the channels present in the file and send the notification accordingly.&#x20;

For the SMS event, it would send the SMS notification and log “Sending SMS Notification”. For Event it would log, “Event Notification Sent”, and for Email, it logs “Email Notification Sent”.

## **Steps**  <a href="#steps-for-enabling-disabling-channels-for-a-particular-business-service" id="steps-for-enabling-disabling-channels-for-a-particular-business-service"></a>

Follow the steps below to enable/disable channels for a particular business service

To add/delete any particular channel for a business service

* Update channelNames array in the [Channel List](https://github.com/egovernments/egov-mdms-data/blob/UAT/data/pg/Channel/ChannelList.json) file and add/delete the channel you want a business service’s action to have.
* Restart egov-mdms-service to apply the changes.
* Configure your business service with the steps mentioned below to



