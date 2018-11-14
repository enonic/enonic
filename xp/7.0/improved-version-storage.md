# Improved storage

## Prelimary meetings
* [2018-09-27 - Storage improvements meetings - Brainstorming](http://wiki.enonic.com/display/dev/2018-09-27+-+Storage+improvements+meetings+-+Brainstorming)
* [2018-09-27 - Storage improvements meetings](http://wiki.enonic.com/display/dev/2018-09-27+-+Storage+improvements+meetings)
* [2018-11-05 - Storage improvements meetings](http://wiki.enonic.com/display/dev/2018-11-05+-+Storage+improvement)

## Epic1: Blobstore - Segmentation by repository

* The blobstore should be segmented by repository
* Vacuum should have an additional task (executed first), removing blob for deleted (index deleted) repositories

### Requirements

* Blobstore Segments should have the possibilities to have multiple levels.
* In upper levels, the segments should be a couple of level: repository ID and blob type.
* Blob records in file blobstore should have the following path [repositoryId]/[blobType]/[blobKey.substring(0,2)]/[blobKey.substring(2,4)]/[blobKey]
* New vacuum task (executed first), removing blob segments for deleted (index deleted) repositories

## Epic2: UUID Version ID
* Version should be identified by a UUID independent from the blobKey

### Requirements
* Version ID is a UUID (similar to NodeId)
* In ES index storage, the type version has the following properties: "versionid", "blobkey", "nodepath", "nodeid", "timestamp"
* In ES index storage, the type branch has the following properties: "versionid", "blobkey", "path", "nodeid", "timestamp", "branch", "state"

## Epic3: Extract IndexConfig (Apply to Permissions also?)
* The IndexConfig should be stored outside of the node blob.
* Vacuum should be updated to handle this new segment

### Requirements
* New default required blob segment: idxcfg
* In ES index storage, the type version has the following properties: "versionid", "blobkey", "indexconfigkey", "nodepath", "nodeid", "timestamp"
* In ES index storage, the type branch has the following properties: "versionid", "blobkey", "indexconfigkey", "path", "nodeid", "timestamp", "branch", "state"
* "indexconfigkey" is a blob key: a hash of its content
* Task deleting idxcfg not used

## Epic4: Move as MetaData update
* Node blobs should not contain the timestamp.
* Rename/move will only update versionID, timestamp and path in indexes (no blob modification)

