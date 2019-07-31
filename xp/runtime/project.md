# Content Projects

The goal is to allow to have content data split into different independant content projects (CMS repositories).

These CMS repositories are repositories prefixed by "com.enonic.cms."
The project "default" is always present ("com.enonic.cms.default").

## Data
Content Project
- name
- displayName
- description
- icon

Initialization:
- "cms-repo" has always been renamed to "com.enonic.cms.default" in 7.0
- We will need an additional initialization step to create the default project metadata if needed.

Content API + Content lib:
- We will need to add new functions to list/get/create/delete content project.
  - New library? or adding to content library?
    - I suggest a new library, especially because of the next point.
- At this level no breaking change. You continue to use the contextLib if you need to change between repositories (as you do today when wanting to change branches).
  - An alternative would be to have a parameter 'project'. (IMO will be confusing and conflicting with context lib)
  - A better alternative would be to have a method 'run' in a project library, working like the context lib, but with concepts of project (and layers in the future).


Admin Rest
- For backward compatibility, 

