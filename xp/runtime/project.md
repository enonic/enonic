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

## Initialization

- "cms-repo" has always been renamed to "com.enonic.cms.default" in 7.0
- We will need an additional initialization step to create the default project metadata if needed.

## Content API + Content lib

### Create/Retrieve/Update/Delete

- We will need to add new functions to list/get/create/modify/delete content projects.
  - New library? or adding to content library?
    - Prefered solution: A new library, especially because of the next point.
- No breaking change. You can continue to use the contextLib if you need to change between repositories (as you do today when wanting to change branches).
  - Proposition: Have a method 'run' in a project library, working like the context lib, but with concepts of project (and layers in the future).

### Admin Rest
- For backward compatibility, we will keep all the /admin/rest/content/* endpoint
  - /admin/rest/content
  - /admin/rest/content/page
  - /admin/rest/content/page/template
  - /admin/rest/content/page/fragment
  - /admin/rest/content/icon
  - /admin/rest/content/media
  - /admin/rest/content/image
- And make them listen additionaly to respectively:
  - /admin/rest/cms/[project]/[layer]
  - /admin/rest/cms/[project]/[layer]/page
  - /admin/rest/cms/[project]/[layer]/page/template
  - /admin/rest/cms/[project]/[layer]/page/fragment
  - /admin/rest/cms/[project]/[layer]/icon
  - /admin/rest/cms/[project]/[layer]/media
  - /admin/rest/cms/[project]/[layer]/image
- We will create a JAX-RS filter (As done in ContentLayer proto epic)
  - It will listen to /admin/rest/cms/[project]/[layer] and set the context to use the corresponding repository (We ignore layer for now)
  

