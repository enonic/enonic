# Automatic data upgrade

* As a user I want to have my existing data upgraded automaticaly, if necessary, between minor versions (w/o system dumps)

## Requirements

* The data model version must be stored in the data (repository system-repo).
* A mechanism similar to initialization should check the data model version
  * Upgrade the data if possible
  * Block the startup of the platform until it is finished
  * Stop the startup if the existing version is subsequent to the expected version (no rollback)

## Dependencies

None

## To be discussed

* Where to store the data model version?
  * Proposition: As two properties in a new node at the root of system-repo

## Details

### Versioning

* [See versioning in data migration](./data-migration.md)
