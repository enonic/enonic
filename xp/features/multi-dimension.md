# Multi-dimension contents

As a developer, I want to be able to create multiple version of my node/content in multiple dimensions (language,country,...)
As a developer, I want to be able to push a content tree to a target dimension

# Requirements
* I must be able to separate versions of nodes/contents between dimensions
* I must be able to publish a content tree to a target dimension
* I should be able to know the version the variant was dimensionPushed from


# Breakdown

## Node meta data
* Create two new metadata fields "dimension" and "variantOf"
  * These two fields need to be in both ES type "version" and "branch" (To be changed in 8.0)
  * Check that it is serialized, dumped/loaded, exported/imported, kept when updated, ...

## NodeService.createVariant
* 1 - Get current versionId
* 2 - Update metadata with dimension=Dimension and variantOf=currentVersionId
  * Do something like SetNodeStateCommand. But beware: updateMetadataOnly is only updating branch, while we want to update version also. Refactor this.

## ContentService.pushToDimension
* Variation of publish
* 1 - Create branch if necessary
* 2 - result = PushToDimensionCommand //Slightly different from PublishContentCommand. Should commit differently. Different behaviour for PENDING_DELETE. Should return also the versionId for the results
* 3 - For each result, nodeService.createVariant

# Warning

* Special case of PENDING_DELETE
