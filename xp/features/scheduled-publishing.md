# Scheduled publishing

* As a content studio, I should be able to schedule publish a content starting from a time until an expired time.
* As a content studio, I should be able to see that a content is pending_published or expired in the content tree view and toolbar status.
* As a developer, using content api on the master branch, I should retrieve by default only content non pending_published/expired.

http://wiki.enonic.com/display/product/Enonic+XP+-+Time-based+publishing+user+story

## Estimate

2/3 weeks

## Requirements

* Contents have an attribute "publish.until". It should be included in the XML export/import.
* Content Studio: Publish Wizard: I can now Schedule a publish. This schedule publish will, for the content and required contents, modify the attributes "publish.from" and "publish.until", save and then publish. [Screenshot1](http://wiki.enonic.com/download/attachments/19497405/Screen+Shot+2016-11-01+at+16.58.23.png?version=1&modificationDate=1478016094099)[Screenshot2](http://wiki.enonic.com/download/attachments/19497405/Screen+Shot+2016-11-01+at+16.58.17.png?version=1&modificationDate=1478016125072)
* Content Studio: Content Tree & Toolbar: I can now see the substates "Pending"(Orange)/"Expired"(Red) of contents pending_publish: [Screenshot](http://wiki.enonic.com/download/attachments/19497405/Screen+Shot+2016-11-01+at+16.25.38.png?version=1&modificationDate=1478013959116)
* Content API
    * Retrieval functions return, by default and on master branch, only the contents currently published (publish.from is NULL OR public.from  <= now()) AND (publish.until is null OR publish.until > now())
        * Retrieval functions: getById, getNearestSite, getByIds, getByPath, getPermissionsById, getByPaths, findByParent, findIdsByParent, find, getBinary, getBinaryKey, contentExists
    * Function "create" should handle publish info
    * Function "publish" should handle schedule publishing
    * Function "duplication" should reset publish info for duplicated content
    * Function "unpublishContent" should reset publish info
    * __Question1: What about the other ones: delete, deleteWithoutFetch, resolvePublishDependencies, move, setChildOrder, reorderChildren, applyPermissions, compare, getVersions, getActiveVersions, setActiveContentVersion, reprocess__
        * Example: Should delete/deleteWithoutFetch on an expired content work ?
* Content JS Library
    * Adapt get/getChildren/getSite/query to return publish info
    * Adapt modify to be able to modify publish info
    * __Question2: Should we adapt publish to perform scheduled publish from JS?__


## Acceptance Criteria

* All requirements are met
* Unit tests are sufficient
