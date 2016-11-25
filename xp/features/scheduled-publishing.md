# Scheduled publishing

As a content studio, I should be able to publish content starting from a time until an expired time.
As a content studio, I should be able to see that a content is pending_published or expired in the content tree view and toolbar status.
As a developer, using content api on the master branch, I should retrieve by default only content non pending_published/expired.

http://wiki.enonic.com/display/product/Enonic+XP+-+Time-based+publishing+user+story

## Estimate

2 weeks

## Requirements

* Contents have an attribute "publish.until"
* Content Studio: Publish Wizard: I can now Schedule a publish. This schedule publish will modify the attributes , save and then publish for the content and required contents.
* The following ContentCommands, on master branch, return by default only the contents currently published (publish.from is NULL OR public.from  <= now()) AND (publish.until is null OR publish.until > now())
  * TBD

* The following JS Content library functions, on master branch, return only the contents currently published (publish.from is NULL OR public.from  <= now()) AND (publish.until is null OR publish.until > now())
  * TBD


## Acceptance Criteria

* All requirements are met
* Unit tests are sufficient
