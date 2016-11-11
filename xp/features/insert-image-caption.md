# Show/suggest caption from image caption and description (Insert image)

As a Content Manager, I want XP to retrieve caption from image meta-data when I insert an image into HTML Area.

## Estimate

2 days

## Requirements

* When user selects an image in the "Insert image" dialog, extract Description from image meta-data and put it into the "Caption" field
* If "Description" is empty, extract "Caption" from meta-data and use that.
* Extraction of meta-data should work on upload of a new image as well
* The Caption field should not be visible until an image is selected or uploaded
* Caption must be editable
* Caption should not be required (empty value is allowed)

## Dependencies

None

## Acceptance Criteria

* All requirements are met
