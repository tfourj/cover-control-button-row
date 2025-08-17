# cover-control-button-row
button row for controlling open/close covers in Home Assistant. This plugin will also accept a "cover group" as the entity_id.

This element is completely theme-able to provide a match to the other control rows to provide a consistent look for the different elements in your Lovelace frontend

Installation:

The easiest way to install this is to use the Home Assistant Community Store (HACS) in Home Assistant.

Follow the instructions there for installation making sure you note the "url:" section for the resources addition.


Conversely, if you don't use HACS you can install it manually by performing the following:

Copy the cover-control-button-row.js file to the appropriate folder in your Home Assistant Configuration directory (/config/www/).

Place the following in your "resources" section in your lovelace configuration (updating the localation to where you placed the above file):

  ```
    - url: /local/cover-control-button-row.js
      type: module
  ```
    
Then to use this in a card place the following in your entity card:

<b>Options:</b>

| Name | Type | Required | Default | Description |
| --- | --- | --- | --- | --- |
| type | String | Yes | none | custom:cover-position-entity-row |
| entity | String | Yes | none | Any positional cover entity_id (including "cover group" entities) |
| name | String | No | none | A custom name for the entity in the row |
| customTheme | Boolean | No | false | Set to true to use a custom theme |
| reverseButtons | Boolean | No | false | Set to true to reverse the button order |
| hideStopButton | Boolean | No | false | Set to true to hide the Stop button for covers thast don't support it. |
| allowDisablingButtons | Boolean | No | true | Set to false to prevent buttons being disabled |
| width | String | No | 41px | A custom width for the buttons |
| height | String | No | 30px | A custom height for the buttons |
| isOpenColor | String | No | '#f44c09' | Sets the color of the 'open' button if cover is fully open |
| isClosedColor | String | No | '#43A047' | Sets the color of the 'closed' button if cover is closed |
| stopButtonColor | String | No | '#c94444' | Sets the color of the 'open' button if cover is fully open |
| buttonInactiveColor | String | No | '#759aaa' | Sets the color of the the buttons if that selection is not "active" |
| customOpenText | String | No | 'OPN' | Sets the text of the "open" control button |
| customStopText | String | No | 'STP' | Sets the text of the "stop" control button |
| customCloseText | String | No | 'CLS' | Sets the text of the "close" control button |
| customOpenConfirmationText | String | No | null | If set, shows a Yes/No confirmation dialog before opening the cover |
| customStopConfirmationText | String | No | null | If set, shows a Yes/No confirmation dialog before stopping the cover |
| customCloseConfirmationText | String | No | null | If set, shows a Yes/No confirmation dialog before closing the cover |
| triggertimer | String | No | null | Triggers specific timers for specific users. Format: "username/timer.entity_id" or multiple: "user1/timer.timer1;user2/timer.timer2" |
| state_color | Boolean | No | false | Sets the icon color of the entity to reflect the current state |
| preventdefaultpointer | Boolean | No | false | Set to true to prevent clicking on the row pointer from opening the cover control dialog |


The values for the colors can be any valid color string in "HEX", "RGB" or by color name.

If the cover position is changed via any other means (slider, service call, etc) the buttons will indicate positions correctly.

This plugin can also be used with a group of positionable covers by creating a "cover group". Then each cover in the group will be simultaneously controlled by the plugin.

<b>Configuration Examples:</b>
    
  ```
    cards:
      - type: entities
        title: cover theme test
        show_header_toggle: false
        state_color: true
        entities:
          - type: custom:cover-control-button-row
            name: Garage Door
            entity: cover.garage_door
            reverseButtons: true
            hideStopButton: true
            ## used to select your own customizable theme
            customTheme: true
            stopButtonColor: 'orange'
            buttonInactiveColor: 'gray'
            isOpenColor: 'pink'
            isClosedColor: 'magenta'
            ## used to select custom text for the buttons
            customOpenText: 'OPEN'
            customStopText: 'STOP'
            customCloseText: 'CLOSE'
            width: '15px'
            height: '15px'
  ```

<b>Configuration Example with Confirmation Dialogs:</b>
    
  ```
    cards:
      - type: entities
        title: Garage Door with Confirmations
        show_header_toggle: false
        entities:
          - type: custom:cover-control-button-row
            name: Garage Door
            entity: cover.garage_door
            ## Add confirmation prompts for safety
            customOpenConfirmationText: 'Are you sure you want to open the garage door?'
            customCloseConfirmationText: 'Are you sure you want to close the garage door?'
            customStopConfirmationText: 'Are you sure you want to stop the garage door?'
            customOpenText: 'OPEN'
            customStopText: 'STOP'
            customCloseText: 'CLOSE'
  ```

<b>Configuration Example with Timer Triggers:</b>
    
  ```
    cards:
      - type: entities
        title: Garage Door with User-Specific Timers
        show_header_toggle: false
        entities:
          - type: custom:cover-control-button-row
            name: Garage Door
            entity: cover.garage_door
            ## Timer configuration - triggers different timers for different users
            ## Single user: triggertimer: "john/timer.garage_access"
            ## Multiple users: triggertimer: "john/timer.john_garage;mary/timer.mary_garage;admin/timer.admin_access"
            triggertimer: "john/timer.garage_timer;mary/timer.security_timer"
            customOpenText: 'OPEN'
            customStopText: 'STOP'
            customCloseText: 'CLOSE'
            ## Optional: Add confirmations - timer only starts if user confirms
            customOpenConfirmationText: 'Open garage door?'
            customCloseConfirmationText: 'Close garage door?'
  ```

This is with the default Lovelace frontend theme set:

![Default](cover_default.gif)

This is with the "Slate" frontend theme set:

![Slate](cover_default_slate.gif)

This is with a custom theme and custom text:

![Custom Theme and Text](cover_themed_text_slate.gif)

