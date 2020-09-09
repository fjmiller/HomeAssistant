# Battery Sensor
This configuration keeps track dynamically of all devices with battery in the name or battery_level as an attribute and reports any device that is currently below the provided threshold.  It includes template sensors, group for exluding devices, a lovelace card to display entities in error and a NodeRed flow for notifications.  Much of the core came from this thread. [HomeAssistant Forum](https://community.home-assistant.io/t/howto-create-battery-alert-without-creating-a-template-for-every-device/30576/5)

# How To Install
## Dependencies
  * None

## Install Process  
  * Copy the yaml from sensors.yaml and place it in your configuration.yaml file under the sensors: heading.  This will create sensor.low_battery_entities.  The state will be the number of entities in error state with an attribute of entities, a comma delimited list of the entity_id's.
  
  * Copy the automations.yaml and place it in your automations.ayaml.  This will control the frequence the sensor will check each device.

  * configure group.exclude_from_battery for entities that this process should disregard.
  ```
  exclude_from_battery:
    - sensor.iphone_battery_level
  ```
  
  Optional:
  * Copy the contents of EntitiesWithLowBattery.lovelace to create a markup card which will display the entities with issues
  * Import the nodered flow from LowBatteryNotification.NodeRed and customize any messaging and notifications

# Configuration
## Changing the reporting Threshold
   The reporting threshold is defined on the sensor.  In the sensors you added to configuration.yaml edit the threshold value!
   ```
     {%- set threshold = 40 -%}
   ```
## Add devices to ignore
   Devices to ignore are part of the group exclude_from_battery.  Add your entities to this array in groups.yaml.

## Lovelace Card
   The lovelace card can be customized to whatever look and feel you like.  It is currently and conditional card and will only display when their are errors to report.

## Notifications
   The notifications flow was created in Node Red.  Updated the Notify and message blocks to meet your specific configuration.  The default flow uses the iOS app Notifications.