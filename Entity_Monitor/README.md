# Entity Health Chech
This configuration keeps track dynamically of all devices with entities reporting state as unknown, unavailable or dead.  It includes template sensors, group for exluding devices, a lovelace card to display entities in error and a NodeRed flow for notifications.  

# How To Install
## Dependencies
  * Node-Red for notifications or write your own :-)
    This uses an input boolean that tracks if Home Assistant started.  remove or replace with your logic for this.

## Install Process  
  * Copy the yaml from sensors.yaml and place it in your configuration.yaml file under the sensors: heading.  This will create a sensor called entities_with_issues.  The state field will equal the number of entities in error and an attribute entities is a cmma delimited list of entities in error

  * Copy the automation from automations.yaml and place it in your automations.yaml file.  This will control the frequency the sensor is updated.  By default we are updating every minute.
  
  * Create a group called entities_exclude_from_monitoring.  This group is an array of entities you want to disregard from this process.
  ```
  entities_exclude_from_monitoring:
    name: "Entities to exclude from alerting on bad status"
    - switch.test_switch
  ```
  
  Optional:
  * Copy the contents of EntitiesWithIssues.lovelace to create a markup card which will display the entities with issues
  * Import the nodered flow from EntitiesWithIssueNotification.NodeRed and customize any messaging and notifications

# Configuration
## Add devices to ignore
   Devices to ignore are part of the group entities_exclude_from_monitoring:.  Add your entities to this array in groups.yaml.

## Lovelace Card
   The lovelace card can be customized to whatever look and feel you like.  It is currently and conditional card and will only display when their are errors to report.

## Notifications
   The notifications flow was created in Node Red.  Updated the Notify and message blocks to meet your specific configuration.  The default flow uses the iOS app Notifications.