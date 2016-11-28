# Time-based publishing

* As a content studio user, I should be able to publish a content that will be considered published from a defined time until an defined expired time.
* As a content studio user, I should be able to see that a content is pending_published or expired in the content tree view and toolbar status.
* As a content studio user, I should be able to edit the attributes "publish.from" and "publish.to" of a content from the Edit wizard page.
* As a developer, using content api on the master branch, I should retrieve by default only content non pending_published/expired.

http://wiki.enonic.com/display/product/Enonic+XP+-+Time-based+publishing+user+story

## Estimate

2/3 weeks

## Requirements

* Contents have an attribute "publish.to". It should be included in the XML export/import.
* Content Studio: Publish Wizard: I can now "schedule" a publish. This "scheduled" publish will, for the content and required contents, modify the attributes "publish.from" and "publish.to", save and then publish. A validation publish-from < publish-to should be performed. [Screenshot1](http://wiki.enonic.com/download/attachments/19497405/Screen+Shot+2016-11-01+at+16.58.23.png?version=1&modificationDate=1478016094099)[Screenshot2](http://wiki.enonic.com/download/attachments/19497405/Screen+Shot+2016-11-01+at+16.58.17.png?version=1&modificationDate=1478016125072)
* Content Studio: Content Tree & Toolbar: I can now see the substates "Pending"(Orange)/"Expired"(Red) of pending_delete/expired contents: [Screenshot](http://wiki.enonic.com/download/attachments/19497405/Screen+Shot+2016-11-01+at+16.25.38.png?version=1&modificationDate=1478013959116)
* Content API
    * Retrieval functions return, by default and on master branch, only the contents currently published (publish.from is NULL OR public.from  <= now()) AND (publish.to is null OR publish.to > now())
        * Retrieval functions: getById, getNearestSite, getByIds, getByPath, getPermissionsById, getByPaths, findByParent, findIdsByParent, find, getBinary, getBinaryKey, contentExists
    * Function "create" should handle publish info
    * Function "publish" should handle "scheduled" publishing. A validation publish-from < publish-to should be performed.
    * Function "duplication" should reset publish info for duplicated content
    * Function "unpublishContent" should reset publish info
    * __Question1: What about the other ones: delete, deleteWithoutFetch, resolvePublishDependencies, move, setChildOrder, reorderChildren, applyPermissions, compare, getVersions, getActiveVersions, setActiveContentVersion, reprocess__
        * Example: Should delete/deleteWithoutFetch on an expired content work ?
* Content JS Library
    * Adapt get/getChildren/getSite/query to return publish info
    * Adapt modify to be able to modify publish info
    * Adapt publish to perform time-based publish.


## Acceptance Criteria

* All requirements are met
* Unit tests are sufficient
