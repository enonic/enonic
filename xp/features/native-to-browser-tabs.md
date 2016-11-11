# Open Content Wizard in native browser tab

As a User, I want the Content Wizard to open in a new browser tab/window instead of XP tab

## Estimate

7 days (4 days on development + 3 days on tests) 

## Requirements

* Content Wizard must open in a new browser tab
* Browser tab must have content's display name in its title
* All changes done to the content in the new tab must still be caught by the Content Grid in the original window
* The Black bar on top must be removed
* To the left of the action buttons in the Content Wizard Toolbar should be the Content Studio icon (the tree icon, black on white - see attached image) that will open the Content Grid in a new window
* When I try to close the Wizard tab with unsaved changes, I should get the same confirmation as I do now when I close an XP tab
* User Wizard and Application Wizard must remain intact

## Dependencies

None

## Acceptance Criteria

* All requirements are met
* Tests are added for every case listed under requirements
