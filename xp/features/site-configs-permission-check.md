# Site config permission check

As a content studio user and as a developer, I should not be able to modify site configurations through the content API if I do not have one of the following roles: "cms.admin" or “system.admin”.
Warning: This permission check will not be executed if the Node API is accessed directly.

## Estimate

1/2 days

## Requirements

* There should be a RoleRequiredException thrown if a site configuration is added/modified/deleted through the content API and the user does not have one of the following roles: "cms.admin" or “system.admin”.
* In Content Studio, the site configs combobox should not be editable if I do not have the role "cms.admin"

## Acceptance Criteria

* All requirements are met
* Unit tests are sufficient



