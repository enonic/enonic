# HTML Area model

* The contents referenced inside an HTML area should be considered when deleting a referenced content or checking inboud/outbound dependencies.

## Requirements

* The input type "HtmlArea" is now a property set.
  * It contains a property "value" of type string.
  * It contains a property "references" of type reference.
* The HTML stripping is done on the property "value"
* Data migration should include the migration of HTML areas for both index config and data

## Dependencies

Data Migration should be partially done

