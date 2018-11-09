# Enonic CLI

* As a user, I want to be able to manage my installations, homes and projects from a command-line interface

## Link Project/Sandbox/EnonicXP

* Sandbox contain an XP home and have a reference to a specific Enonic XP distribution
* Project (apps/libs) created with the CLI will have a reference to a sandbox
* These references will be stored in a file '.enonic' at the root of the Project/Sandbox

## Code
* Enonic CLI code will be implemented in Go
* Enonic CLI will be generated for the following platform: Linux/x64, macOS/x64 and Windows/x64	
* Enonic CLI has an independant versioning from Enonic XP. (Note: It should not be possible for Enonic CLI to manage a major version greater than the current handled version since we cannot guarantee that the API has remained unchanged).

## Download

* Enonic CLI should be available in download from the Enonic Website
* Enonic CLI should be available using: brew, apt-get, ... //TBD
  
## File structure

* Enonic CLI, will create a dot folder in the user folder to store the XP distributions, sandboxes and projects.
* ~/.enonic
  * distributions
    * 7.0.0-macos
    * 7.1.0-SNAPSHOT-macos
  * sandboxes
    * default
      * .enonic: distro=7.0.0-macos . running=true  
      * home
      * blob
    * customer-a
      * .enonic: distro=7.0.0-macos running=false
      * home
      * blob
    * customer-b
      * .enonic: distro=7.1.0-macos running=false
      * home
      * blob
* gitfolder
  * myapp-a
    * .enonic: sandbox=customer-a
  * office-league


## CLI options

### Default values

* Default sandbox: Sandbox associated to the current project

### Sandbox commands

* `enonic sandbox`   # List available sandbox commands
* `enonic sandbox help [command]`   # Display help page for a specific sandbox command
* `enonic sandbox ls`   # List all sandboxes in the CLI folder (and point out the running one and the one associated to the current project)
* `enonic sandbox start [sandboxName]`   # Start the sandbox (enonic distro pointing to this sandbox home). Create if not existing
* `enonic sandbox stop [sandboxName]` # Stop XP  
* `enonic sandbox new`   # Wizard: Create a new sandbox (Download XP distro if necessary, copy the home from the XP distro). Propose to set it for the current project
* `enonic sandbox delete [sandboxName]`   # Delete a sandbox

### Project commands

* `enonic project`      # List available project commands
* `enonic project help [command]`   # Display help page for a specific project command
* `enonic project sandbox [sandboxName]`   # Set the default sandbox associated to the current project
* `enonic project new`  # Wizard: Init-app
* `enonic project clean `  # Gradle clean   
* `enonic project build`  # Gradle build  
* `enonic project deploy` # Create sandbox if necessary + Gradle deploy
* `enonic project publish`# Gradle publishToMavenLocal or publish
* `enonic project add (part|service|page|...)`      # Wizard: Add part/service/page/... in the project
* `enonic project remove (part|service|page|...)`      # Remove part/service/page/... from the project

### Misc commands

* `enonic attach -s [sandboxName]` OR `enonic attach -u [sandboxUrl]` #Sets the target for Management Commands


### Management Commands

* `enonic snapshot ls`           # Returns a list of existing snapshots with name and status.
* `enonic snapshot new`          # Stores a snapshot of the current state of the repository.
* `enonic snapshot restore`          # Restores a snapshot of a previous state of the repository.
* `enonic snapshot delete`       # Deletes snapshots, either before a given timestamp or by name.

* `enonic dump new`                # Export data from every repository.
* `enonic dump upgrade`            # Upgrade a dump.
* `enonic dump load`               # Import data from a dump.

* `enonic export new`              # Export data for a specified path.
* `enonic export load`             # Import data from a named export.

* `enonic app install`  # Install an application from URL or file
    
* `enonic repo reindex`            # Reindex content in search indices for the given repository and branches.
* `enonic repo read-only`      # Toggle read-only mode for sandbox or single repository

* `enonic cms reprocess`          # Reprocesses content in the repository.

* `enonic cluster replicas`       # Set the number of replicas in the cluster.

* `enonic vacuum`             # Removes unused blobs and binaries from blobstore


## Use cases
* First time user create and deploy locally new app
  * `enonic project new`
  * `enonic project deploy`
* Deploying an app to a different sandbox
  * `enonic project deploy -s customer-b`
* Testing a project for a new version of enonic xp
  * `enonic sandbox new` //Wizard will propose to associate the new sandbox to the current project
  * `enonic project deploy`
* Taking a snapshot of a sandbox
  * `enonic attach -s [sandboxName]` OR `enonic attach -u [sandboxUrl]`
  * `enonic snapshot`
