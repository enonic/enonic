# HTML Area model

* The contents referenced inside an HTML area should be considered when deleting a referenced content or checking inboud/outbound dependencies.

## Requirements

* A ContentProcessor (portal level) should analyze all HTML areas of a content on create&update and store the references in a new content property: processedReferences

## To be discussed

Discuss "reprocess" when migrating to 7.0

