# Change native tabs to browser tabs

As a User, I want the Content Wizard to open in a new browser tab/window instead of XP tab

## Estimate

6 days (4 days on development + 2 days on tests) 

## Requirements

* Change the navigation to open a new browser tab with the Content Wizard
* Verify that events triggered by the Content Wizard in the new window are still caught by the Content Grid in the original window 
* (To be confirmed) Change title of the browser window from "Content Studio - Enonic XP" to display name of the content opened in the Wizard, for example "Features"
* (To be confirmed) For content that doesn't reside in the root show title as "<Root content name> - <Open content name>", for example "Features - My Content".
* (To be confirmed) Remove "Content Studio" link in the top left corner so that user cannot navigate away from the Wizard
* (To be confirmed) Remove "X" icon from the XP tab so that user closes the Wizard by closing the browser window
* (To be confirmed - if previous requirement is met) Change event listeners from "X" icon to on window close

## Dependencies

None

## Acceptance Criteria

* All requirements are met
* Tests are added for every case listed under requirements
