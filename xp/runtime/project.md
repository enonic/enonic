# Content Projects

The goal is to allow to have CMS data split into different independant content projects (CMS repositories).

These CMS repositories are repositories prefixed by "com.enonic.cms."
The project "default" is always present ("com.enonic.cms.default").

The project metadata (display name, description icon, ...) will be stored as a node "/project" in the master branch of the repository of the project.

## Data
Content Project
- name
- displayName
- description
- icon

## Initialization

- "cms-repo" has already been renamed to "com.enonic.cms.default" in 7.0 but will need an additional initialization step to create the default project metadata if needed.


## Project service

- Create new service ProjectService with the following methods
  - list
  - get
  - create
  - modify
  - delete

## Content API + Content lib

- Create new library "project"
  - Create functions: "list","get","create","modify","delete"
  - Create function "run" in a project library, working by setting a context like the contextLib.run, but with concepts of project (and layer in the future).
- Remove all places in the content level where the default CMS repo was used directly. Retrieve it from the current context.

## Admin Rest
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
- Add new Admin Resource to "list","get","create","modify","delete" projects
  

