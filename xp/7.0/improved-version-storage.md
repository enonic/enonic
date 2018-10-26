# Improved storage

## Prelimary meetings
* [2018-09-27 - Storage improvements meetings - Brainstorming](http://wiki.enonic.com/display/dev/2018-09-27+-+Storage+improvements+meetings+-+Brainstorming)
* [2018-09-27 - Storage improvements meetings](http://wiki.enonic.com/display/dev/2018-09-27+-+Storage+improvements+meetings)

## Epic1: Blobstore segments divided by repository

* The blobstore segments should be divided by repository
* TBD: As a controller developer, I should be able to delete entirely (index+blob) a repository
* Vacuum should have an additional task (executed first), removing blob for deleted (index deleted) repositories

### Requirements

* Blobstore implementations should have
  * Their methods getRecord/addRecord/removeRecord/list have an additional RepositoryId parameter before the segment
  * A new method deleteRepository(RepositoryId)
  * A new method listRepositories()
* CachingBlobStore implementations should have
  * Their method invalidate have an additional RepositoryId parameter before the segment
* Blob records in file blobstore should have the following path [repositoryId]/[segment]/[blobKey.substring(0,2)]/[blobKey.substring(2,4)]/[blobKey]
* TBD: repoLib.delete will have two parameters:
  * repoId //Mandatory
  * includeBlobs //Optional. Defaults to false
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
