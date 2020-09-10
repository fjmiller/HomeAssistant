# Virtual School Schedule Announcments
   This process uses a Google Calendar of class schedules to announce via Alexa Devices and text notification when class is about to start (Offset) and when class is starting.  The Title of the event is provided so the student will know which class they need to be ready for.  In addition you can add text to the body which will be announced and can be different in the offset and time message events.

# How To Install
## Dependencies
  * [Google Calendar Integration](https://www.home-assistant.io/integrations/calendar.google/) 
  * [Alexa Media Player Integration](https://github.com/custom-components/alexa_media_player): If you are installeing this please consider using the [HACS store](https://community.home-assistant.io/t/custom-component-hacs/121727)
  * [Node Red](https://community.home-assistant.io/t/home-assistant-community-add-on-node-red/55023) for the notification and TTS flow.  

## Install Process  
  *Assumptions: You have Node Red set-up and the Google Calendar integration set-up and working.

  *Install the Sensor Template:  This creates a sensor.calendar_offset which updates with the offset attribute for your calendar.  This is used to trigger offset automations.  Update the entities and descriptions as appropriate for your config.
  ```
  - platform: template
  sensors:
    calendarName_calendar_offset_reached:
      friendly_name: 'Calendar name Calendar Offset'
      entity_id: calendar.school_calendar
      value_template: "{{ state_attr('calendar.school_calendar','offset_reached') }}"  
  ```
  * Add the Node Red flow: SchoolAnnouncements.nodered
    - Update the flow initiation node to your calendar entry
    - Update the Offset Reached and current_state nodes to your offset entity and the calendar entry
    - Updated any announce devices on the far left of the flow and link as the examples are linked.

# Configuration
##Setting up the Google Calendar
  When setting up your calendar it is important to understand how the integration works as this will impact the functioning of this script.
  
  * The integration checks for next event every 15 minutes.  If one event ends and the next one starts within 15 minutes you may not get alerted until after the next event starts and the system checks.  Also consider any offset's in this.  For this reason I use the calendar appointments as a start time, but the end time it typically only a couple minutes after so the refresh to next appointment has time to occur.

  * The entity updates state every minute.  Therefore if a meeting is scheduled for 13:00 your event will typically fire between 13:00 and 13:01.  For announcing class start time I use 12:59 as the start time.

  * Filter which events get spoken.  I used #alexa as the filter so add it to your body
  ```
  google_calendars.yaml
  - cal_id: {someGooblyGook}@group.calendar.google.com
  entities:
  - device_id: school_calendar
    ignore_availability: true
    name: School Calendar
    track: true
    search: '#alexa'
    offset: '!!'
    max_results: 10
  
  in the body of the event in your Google Calendar

  #alexa
  ```
  *Adding additional text after the subject can be done by adding Offset or Time tags in the body of the event.  For example:
  ```
  #alexa
Offset: Don't foget to brush your teeth and be ready!
Time: Have a wonderful day!
  ```

