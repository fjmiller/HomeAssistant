# Home Assistant Started
This configuration keeps track of recent Home Assistant Start events through an input_boolean.  This is useful for triggering or checking in Node-Red Flows.

# How To Install
## Dependencies
  * None
## Install Process  
  * Copy the yaml from input_booleans.yaml and place it in your configuration.yaml file under the input_boolean: heading.  This will create a sensor called hass_started.  The state field will be turned on 1 minute after boot and then turned off 10 seconds later. The delay is meant to give NodeRed a chance to start-up and connect to the HomeAssistant API.

  * Copy the automation from automations.yaml and place it in your automations.yaml file.  This will control the state changes and the timing can be tweaked to your specific situation.
  
  
# Configuration
* None
