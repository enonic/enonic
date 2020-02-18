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
- It should be possible to store tags on a node.
- These tags should be stored in storage ES documents



- When creating a content

## To Be Defined




## Decisions
- We will store the inheritance/layers information
  - In the Project Settings
  - In each content/node through "tags" (original branch)

## Steps
- Project Settings
- LayeredNodeService
  - uses NodeService and ProjectService
  - is used by ContentService
- VersionTags
  - Add the concept of tags in Node. Will be stored in branch and version ES documents
  - Should be returned on NodeComparison
- For each node operation, apply necessary additional treatment (Special push)
