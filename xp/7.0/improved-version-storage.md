# Improved version storage

* As a user I want the space taken by the blobstore to be more efficient

## Requirements

* IndexConfig is extracted from version files to a specific files.
  * IndexConfig files are identified by their MD5 hash
  * IndexConfig files are a new segment of blob store (in addition to node and binary)
  * Version files reference IndexConfig files by their ID stored inside the version file.
* Blobstore segment should contain repository
  

## Dependencies

None


  
