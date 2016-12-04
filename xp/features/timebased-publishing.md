# Time-based publishing

* As a content studio user, I should be able to publish a content that will be considered published from a defined time until an defined expired time.
* As a content studio user, I should be able to see that a content is pending_published or expired in the content tree view and toolbar status.
* As a content studio user, I should be able to edit the attributes "publish.from" and "publish.to" of a content from the Edit wizard page.
* As a developer, using content api on the master branch, I should retrieve by default only content non pending_published/expired.

http://wiki.enonic.com/display/product/Enonic+XP+-+Time-based+publishing+user+story

## Estimate

2 weeks

## Requirements

* Contents have an attribute "publish.to". It should be included in the XML export/import.
* Content Studio: Edit wizard page: There are two datetime picker fields in the settings part mapped to the attributes 'publish.from' and 'publish.to'.
* Content Studio: Publish Wizard: We can now "schedule" a publish. This "scheduled" publish will set the dates for all contents where values have not already been configured and then publish them. A validation publish-from < publish-to should be performed. [Screenshot1](http://wiki.enonic.com/download/attachments/19497405/Screen+Shot+2016-11-01+at+16.58.23.png?version=1&modificationDate=1478016094099)[Screenshot2](http://wiki.enonic.com/download/attachments/19497405/Screen+Shot+2016-11-01+at+16.58.17.png?version=1&modificationDate=1478016125072)
* Content Studio: Content Tree & Toolbar: I can now see the substates "Pending"(Orange)/"Expired"(Red) of pending_delete/expired contents: [Screenshot](http://wiki.enonic.com/download/attachments/19497405/Screen+Shot+2016-11-01+at+16.25.38.png?version=1&modificationDate=1478013959116)
* Content API
    * Retrieval functions return, by default and on master branch, only the contents currently published (publish.from is NULL OR public.from  <= now()) AND (publish.to is null OR publish.to > now())
        * Retrieval functions: getById, getNearestSite, getByIds, getByPath, getPermissionsById, getByPaths, findByParent, findIdsByParent, find, getBinary, getBinaryKey, contentExists
    * Function "create" should handle publish info. A validation publish-from < publish-to should be performed.
    * Function "modify" should handle publish info. A validation publish-from < publish-to should be performed.
    * Function "publish" should handle "scheduled" publishing. A validation publish-from < publish-to should be performed. The publish info values will be set for all content where values have not already been configured.
    * Function "duplication" should reset publish info for duplicated content
    * Function "unpublishContent" will remove the publish info. __Question: Is that correct?__
* Content JS Library
    * Adapt get/getChildren/getSite/query to return publish info
    * Adapt modify to be able to modify publish info
    * Adapt publish to perform time-based publish.
* Context JS Library
    * Adapt run and get to be able to set attributes


## Acceptance Criteria

* All requirements are met
* Unit tests are sufficient
