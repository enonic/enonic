# Improved storage

## Prelimary meetings
* [2018-09-27 - Storage improvements meetings - Brainstorming](http://wiki.enonic.com/display/dev/2018-09-27+-+Storage+improvements+meetings+-+Brainstorming)
* [2018-09-27 - Storage improvements meetings](http://wiki.enonic.com/display/dev/2018-09-27+-+Storage+improvements+meetings)

## Epic1: Blobstore - Segmentation by repository

* The blobstore should be segmented by repository
* Vacuum should have an additional task (executed first), removing blob for deleted (index deleted) repositories

### Requirements

* Blobstore Segments should have the possibilities to have multiple levels.
* In upper levels, the segments should be a couple of level: repository ID and blob type.
* Blob records in file blobstore should have the following path [repositoryId]/[blobType]/[blobKey.substring(0,2)]/[blobKey.substring(2,4)]/[blobKey]
* New vacuum task (executed first), removing blob for deleted (index deleted) repositories

## Epic2: Improved node version model

* The IndexConfig should be stored outside of the node blob.
* Version should be identified by a UUID independent from the blobKey
* Node blobs should not contain the timestamp.
* Rename/move will only update versionID, timestamp and path in indexes (no blob modification)
* Vacuum should be update to handle this new segment

### Requirements

* New default required blob segment: index-config
* In ES index storage, the type version has the following properties: "versionid", "nodeblobkey", "indexconfigblobkey", "nodeid", "path", "timestamp"
* In ES index storage, the type branch has the following properties: "versionid", "nodeblobkey", "indexconfigblobkey", "branch", "nodeid", "path", "timestamp", "state"
* Version ID is a UUID (similar to NodeId)
* NodeBlobKey and IndexConfigBlobKey are BlobKeys (hash of their content)
* Node blob do not contain the IndexConfig or timestamp
