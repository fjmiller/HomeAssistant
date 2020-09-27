# AeoTec Water Sensor 6
This configuration manged the alerting and dashboarding of the [AeoTec Water Sensor 6](https://aeotec.com/z-wave-water-sensor/).  This sensor has 4 pins which generate 2 binary sensors and 2 leak zones.  In my configuration these are used under a sink so I combine the 2 zones to 1 zone and report a wet/dry status with the icon set to change based on state.

# How To Install
## Dependencies
  * AeoTec Water Sensor 6 paired to your Zwave Network and available in Home Assistant.  
  * Notifications are done via Node-Red.  This can also easily be done in native home assistant.
  

## Install Process  
  * Copy the yaml from sensors.yaml and place it in your configuration.yaml file under the sensors: heading.  This will create sensor for the new combined sensor.  You will need to name it and update the tracked sensors to be the 2 binary sensors created by your Aeotec Water Sensor 6 installation.  The state will be "Wet" or "Dry" with an icon of mdi:water-off or mdi:water-alert depending on the state.  
  
  * Copy the contents of the Lovelace card to a manual card and replace the entity with your leak detector or a list of leak detector's.

  * Paste the node red flow into your Node Red installation.  Update the leak detector entity to your leak detector entity.
  
# Configuration
## Configuring the template for your entities
   The Sensor will look like the code below.  Update:
   * leak_detector_entity_name : Change this to be the entity name for the template.
   * friendly_name: Update to be the name you see in the UI for this entity
   * binary_sensor.detector_leak and leak_2: These are listed in both the value and attribute.  Update them to be your sensors created by the AeoTec sensor when you installed it.

     
   ```
      leak_detector_entity_name:
        friendly_name: "Leak Detector"
        value_template: >-
               {% if is_state("binary_sensor.detector_leak","on") or is_state("binary_sensor.detector_leak_2","on") -%}
                    Wet
               {%- else -%}
                    Dry
                {%- endif %}   
        attribute_templates:
          icon: >-
            {% if is_state("binary_sensor.detector_leak","on") or is_state("binary_sensor.detector_leak_2","on") -%}
                mdi:water-alert
             {%- else -%}
                 mdi:water-off
             {%- endif %}   
   ```

## Lovelace Card
   The lovelace card can be customized to whatever look and feel you like.  It has a state filter to only display when Wet.

## Notifications
   The notifications flow was created in Node Red.  Updated the Notify and message blocks to meet your specific configuration.  The default flow uses the iOS app Notifications.
