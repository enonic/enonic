# Repo Service API

As a developer, I want to be able to create and manage my own storage so I can work with data that are not Content.

## Estimate

X days/weeks

## Requirements

* I want to be able to create and manage other storages than the buildIn cms-repo and system-repo. 
* It should be possible to create different branches in this storage, but not necessary. 
* An API to easily create and manage data in the repositories should also be available
* The API should fluently handle advanced data-types like geo-point and binaries
* I should be able to create data with a minimum of properties set, e.g I should not have to give my data a name.

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
