# Vacuum 7

As an ops, I want to be able to clean up unnecessary storage (unused blobs/binaries/versions=...)

# Requirement

* Endpoint available on the management port, under /system/vacuum
* The following should be vacuumed
  * 1 - Unused segments (repositories)
  * 2 - Unused node versions
    * 2.1 - Deleted from branch
    * 2.2 - 
  * Unused blobs
    * 3 - Unused node blobs
    * 4 - Unused binaries
* As in Vacuum 6, there should be an age threshold (Was set to 1hour)
  * Check that the segment/blob/nodeversion were deleted/created more than X time ago
* Configurable/Parametrizable
  * Threshold
  * Tasks to execute
  
# Propositions

* Allow to gracefully stop the vacuum

