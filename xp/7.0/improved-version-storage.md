# Improved storage

## Prelimary meetings
* [2018-09-27 - Storage improvements meetings - Brainstorming](http://wiki.enonic.com/display/dev/2018-09-27+-+Storage+improvements+meetings+-+Brainstorming)
* [2018-09-27 - Storage improvements meetings](http://wiki.enonic.com/display/dev/2018-09-27+-+Storage+improvements+meetings)

## Epic1: Divide blobstore segments by repository

* The blobstore segments should be divided by repository
* As a controller developer, I should be able to delete entirely (index+blob) a repository
* Vacuum should have an additional task (executed first), removing blob for deleted (index deleted) repositories

### Requirements

* Blobstore implementations should have
  * Their method getRecord/addRecord/removeRecord/list have an additional RepositoryId parameter before the segment
  * A new method deleteRepository(RepositoryId)
  * A new method listRepositories()
* Blob records in file blobstore should have the following path [repositoryId]/[segment]/[blobKey.substring(0,2)]/[blobKey.substring(2,4)]/[blobKey]
* New vacuum task (executed first), removing blob for deleted (index deleted) repositories
