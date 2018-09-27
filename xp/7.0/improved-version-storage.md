# Improved storage

* As a user I want to be able to change index and re-index data if needed (without changing the version of a document)
* Today, many nodes are 90% index, and 10% data - this is inefficient. Can we store data differently?
* Vacuum should be done quickly (delete blob&binaries that are no longer in use)
* Version storage in XP is very "greedy" in that every small change will create a new "nodeversion". 
* Developers do not always want versions, but just the ability to "update" an item (for example if you update a user object every time user logs in)
* An option could be to have a max number of versions for a specific node?? (what about different versions in branches??)
* We are missing an API for nodeversions in node-lib
* Consider how we create indexes/types in ES - is this optimal?
* We don't know if a field is a "principal" (valueType?)

# Other stuff
* It would be nice at one point to have a "bucket" rather than repo, with no tree structure, branches and versions (at least) - this could be used for high-performance volume data ala logging.
- Would require one "blobstore segment" per bucket (for re-indexing)



## Thoughts

* Currently MD5 is used as nodeversion key, this should probably be discontinued?
* Potentially, "versions" can be committed/frozen - but until they are frozen they can be updated. I.e. when doing autosave in content studio, this would be useful. Also, for "application style" data like users, a single node could be udpated as many times as the developer likes without creating new versions that need to be persisted

  
