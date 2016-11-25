# Scheduled publishing

* As a content studio, I should be able to publish content starting from a time until an expired time.
* As a content studio, I should be able to see that a content is pending_published or expired in the content tree view and toolbar status.
* As a developer, using content api on the master branch, I should retrieve by default only content non pending_published/expired.

http://wiki.enonic.com/display/product/Enonic+XP+-+Time-based+publishing+user+story

## Estimate

2 weeks

## Requirements

* Contents have an attribute "publish.until". It should be included in the XML export/import.
* Content Studio: Publish Wizard: I can now Schedule a publish. This schedule publish will, for the content and required contents, modify the attributes "publish.from" and "publish.until", save and then publish. [Screenshot1](http://wiki.enonic.com/download/attachments/19497405/Screen+Shot+2016-11-01+at+16.58.23.png?version=1&modificationDate=1478016094099)[Screenshot2](http://wiki.enonic.com/download/attachments/19497405/Screen+Shot+2016-11-01+at+16.58.17.png?version=1&modificationDate=1478016125072)
* Content Studio: Content Tree & Toolbar: I can now see the substates "Pending"(Orange)/"Expired"(Red) of contents pending_publish: [Screenshot](http://wiki.enonic.com/download/attachments/19497405/Screen+Shot+2016-11-01+at+16.25.38.png?version=1&modificationDate=1478013959116)
* The following ContentService functions, on master branch, return by default only the contents currently published (publish.from is NULL OR public.from  <= now()) AND (publish.until is null OR publish.until > now())
    * TBD

* The following JS Content library functions, on master branch, return only the contents currently published (publish.from is NULL OR public.from  <= now()) AND (publish.until is null OR publish.until > now())
    * get, getAttachments, getAttachmentStream, getChildren, getPermissions, getSite, getSiteConfig
    * !!!! What about the other ones: create, createMedia, delete, modify, move, publish, query, setPermissions, unpublish !!!!
        * For example: Should a contentLib.delete on a expired content work? I guess not. Otherwise it means that we get null on get() but that delete() deletes something.
        * Example2: Should I be able to create a content on master with the publish information set?
       * Example3: Should we adapt the publish functions


## Acceptance Criteria

* All requirements are met
* Unit tests are sufficient
