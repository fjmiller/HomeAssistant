# Home Occupied
Create a group that changes state to home or away if the home is occupied including person tracking and an options for guest presence override.

# How To Install
## Dependencies
  * None  

## Install Process  
  * Copy the yaml from input_booleans.yaml and place it in your configuration.yaml file under the input_booleans: heading.  This will create a sensor called guest_presence that will be used to toggle the override. 

  * Copy the the template from sensors.yaml and place it in your configuration.yaml file under the sensors: heading.  This will create a sensor which updates state based on the input boolean.  This keeps the state values in sync with the person presence which is required for the group to turn on/off correctly.

  * copy the group from groups.yaml to your groups.yaml file.  Added any entries for persons you would like to track.
  
  Optional:
  * Copy the contents of Presence_Card.lovelace to create a glance card which will display the input boolean and home occupied.  You can also add the entities for persons and they will display when they are home.

# Configuration
## Add people to track to the group
   Update group.home_occupied with all the person. entities you are going to track.  Keep the sensor.guest_presence to use the Guest Override.

## Lovelace Card
   The lovelace card can be customized to whatever look and feel you like.  It is currently a glance card that displays the home occupied and guest presence state and allows you to toggle guest presence.  You can add your person entities to it and they will display if they are home.
