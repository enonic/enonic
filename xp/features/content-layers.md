# Content Layers

Unlike the prototype:
- Branch inheritance will be a content level concept.
- There will be multi-inheritance (Not implemented in this version, but we should try to keep it in mind)

## Decisions
- We will store the inheritance/layers information
  - In the "com.enonic.cms" part of the repository data
  - In each node through "tags" (In this case we will store the original branch)
- ContentLayer
  - name: ContentLayerName
  - parentNames: List<ContentLayerName>
  - displayName: String
  - description: String
  - language: Locale
  - icon: Attachment
- ContentLayerName format: [A-Za-z0-9\-_]+

## Steps
- Project Settings
- LayeredNodeService
  - uses NodeService and ProjectService
  - is used by ContentService
- VersionTags
  - Add the concept of tags. Will be stored in branch and version ES documents
  - Should be returned on NodeComparison
- For each node operation, apply necessary additional treatment (Special push)
