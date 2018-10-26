# Improved storage

## Prelimary meetings
* [2018-09-27 - Storage improvements meetings - Brainstorming](http://wiki.enonic.com/display/dev/2018-09-27+-+Storage+improvements+meetings+-+Brainstorming)
* [2018-09-27 - Storage improvements meetings](http://wiki.enonic.com/display/dev/2018-09-27+-+Storage+improvements+meetings)

## Epic1: Divide blobstore by repository

* The blobstore should be divided by repository
* As a controller developer, I should be able to delete entirely (index+blob) a repository

### Requirements

* Blobstore implementations should have their method getRecord/addRecord/removeRecord/list have an additional RepositoryId parameter
* Blobstore implementations should have a new method deleteRepository(RepositoryId)
* Record in file blobstore should have the following path [repositoryId]/[segment]/[blobKey.substring(0,2)]/[blobKey.substring(2,4)]/[blobKey]
