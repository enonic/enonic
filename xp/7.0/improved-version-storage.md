# Improved version storage

* As a user I want the space taken by the blobstore to be more efficient

## Requirements

* IndexConfig is extracted from version files to a specific files.
  * IndexConfig files are identified by their MD5 hash
  * IndexConfig files are a new segment of blob store (in addition to node and binary)
  * Version files reference IndexConfig files by their ID stored inside the version file.
  
  

## Dependencies

None

## Raw specs to be discussed

* One root folder by repository: /$blobstore/cms-repo/blobs/aa/bb/cc/aabbccxxx
  * Use a generated ID per repo than name
* node will now be stored by Node ID, with versions as subfolder/files (the versions will not be md5 anymore but a random ID) to allow upgrading of version files.
* (Lower prio)Binary counter in the index to keep track of number of nodes using the Binary
* Rewrite Vacuum (Example: Repositories can be deleted in an easier way)
* Rewrite versions table (only need to hold versions that are in branches), and nodes that are/ have not yet been deleted
* Fix "Hack" for detecting changed nodes (related to metadata - ask @runarmyklebust )
* Look at dump/export format


  