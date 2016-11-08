# Repo Service API

As a developer, I want to be able to create and manage my own storage so I can store and manage data that are not Content.

## Estimate

X days/weeks

## Requirements

* I want to be able to create and manage other storages/repositories than the buildIn cms-repo and system-repo. 
* It should be possible to create different branches in repositories, but not necessary. 
* An API to easily create and manage data (nodes) in the repositories should also be available
* The API should fluently handle advanced data-types like geo-point and binaries
* I should be able to create data with a minimum of properties, e.g I should not have to give my node a name.

## Acceptance Criteria

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
