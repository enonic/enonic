# Show/suggest alt text and enable editing (Insert image)

As a Content Manager, I want to be able to set alternative text for an image when I insert it into HTML Area.

As of now, we always use image's display name as alternative text but it's not editable.

## Estimate

1 day

## Requirements

* Add a new field "Alternative text" to the "Insert Image" dialog, under "Caption"
* The field should not be visible until an image is selected or uploaded
* When user selects or uploads an image in the "Insert image" dialog, put image name into the "Alt text" field
* The field must be editable
* The field should not be required (empty value is allowed)
* Put contents of the field into "alt" attribute of the "img" tag
* Update "alt" attribute of the "img" tag when changing an existing image

## Dependencies

None

## Acceptance Criteria

* All requirements are met
