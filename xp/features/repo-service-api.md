# Repo Service API

As a developer, I want to be able to create and manage my own storage so I can store and manage data that are not "Content".

## Estimate

6 weeks

## Requirements

* I should be able to create and manage other storages/repositories than the built-in cms-repo and system-repo. 
* It should be possible to create different branches in repositories, but not necessary. 
* A Java/Javascript-API to easily create and manage data (nodes) in the repositories should be available
* API: I should be able to create data with a minimum of properties, e.g I should not have to give my node a name.
* API: I should be able to do queries with aggregations on the nodes
* API: I should be able to fluently handle advanced data-types like geo-point and binaries

## Acceptance Criteria

* All new functionality should have minimum 80% code coverage
* The Javascript-API documentation should be available
* New Javascript-API should be tested in the features-app
* Existing data from previous versions should work
* Applications built on the old versions should work without having to rebuild the application with the new API
* An application using the new API's should be created and used to test user experience

### The following API's should be available:
* Java repo-API
 - createRepository
 - createBranch
 - list
 - exists(repositoryId)
 - get(repositoryId)
 - deleteRepository
 
* Javascript repo-API
 - createRepository
 - createBranch
 - list
 - exists(repositoryId) 
 - get(repositoryId)
 - deleteRepository
 
* Javascript node-API
 - create
 - modify
 - diff
 - push
 - get
 - delete
 - move
 - query


## Breakdown
