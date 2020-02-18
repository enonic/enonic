# Content Layers (Runtime)

## Differences with prototype
- Branch inheritance will be a content level concept.
- There will be multi-inheritance (Not implemented in this version, but we should keep it in mind)
- Will be non-breaking (XP 7.Y) if possible

## Dependency

- Must be done after Content Project

## Requirements

- A content layer as the following information
  - name: ContentLayerName
  - parentNames: List<ContentLayerName>
  - displayName: String
  - description: String
  - language: Locale
  - icon: Attachment
- ContentLayer name format: [A-Za-z0-9\-_]+
- Branch name format: draft-{layerName} OR master-{layerName}
- Layer information is stored in Project Settings
- Node has a new field "tags" (An array/list of string)
- Tags should also be stored in storage ES documents
- Content service will set the layerName in tags
  - The best way would be to have a real additional data tree. Not having this, we will have to mimic it
  - Proposition of value: com.enonic.cms.layer={layerName}

- Deletion of content through Content API should have an additional option/flag to define if the content is supposed to be deleted in child branches (otherwise, it will modify the tags of the node in all direct child branches).

- Wrap node operation with the following
  - If node created -> Push* node to child branches
  - If node updated -> Push* node to child branches
  - If node renamed -> Push* node to child branches
  - If node deleted -> Delete/Modify* node in child branches
  - If node pushed -> Push* node to child branches
  - If node duplicated -> Push* node to child branches
  - If node moved -> Push* node to child branches
  - If node reordered -> Push* node to child branches
  - If node permissions changed -> Push* node to child branches
  - If root permissions changed -> Push* node to child branches
  - If node imported -> Push* node to child branches
  - For all other operations, do nothing more

## To Be Defined
- Tag format


## Steps
- Project Settings
- LayeredNodeService
  - uses NodeService and ProjectService
  - is used by ContentService
- VersionTags
  - Add the concept of tags in Node. Will be stored in branch and version ES documents
  - Should be returned on NodeComparison
- For each node operation, apply necessary additional treatment (Special push)
