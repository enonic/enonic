# Enonic CLI

* As a user, I want to be able to manage my installations, homes and projects from a command-line interface

## Link Project/Sandbox/EnonicXP

* Sandboxes contain an XP home and have a reference to a specific Enonic XP distribution
* Project (apps/libs) created with the CLI will have a reference to a sandbox
* These references will be stored in a file '.enonic-cli' at the root of the Home/Sandbox

## Code
* Enonic CLI code will be implemented in Go
* Enonic CLI will be generated for the following platform: Linux/x64, macOS/x64 and Windows/x64	
* Enonic CLI has an independant versioning from Enonic XP. (Note: It should not be possible for Enonic CLI to manage a major version greater than the current handled version since we cannot guarantee that the API has remained unchanged).

## Download

* Enonic CLI should be available in download from the Enonic Website
* Enonic CLI should be available using: brew, apt-get, ... //TBD
  
## File structure

* Enonic CLI, will create a dot folder in the user folder to store the XP distributions, sandboxes and projects.
* ~/.enonic-cli
  * jdks
    * jdk1.8.0_181.jdk (for 6.Y.Z versions)
  * distributions
    * 6.15.2
    * 7.0.0-SNAPSHOT
  * sandboxes
    * .enonic-cli: running = customer-b
    * default
      * .enonic-cli: xp.version=6.15.1
      * home
      * blob
    * customer-a
      * .enonic-cli: xp.version=6.15.1
      * home
      * blob
    * customer-b
      * .enonic-cli: xp.version=6.15.2
      * home
      * blob
  * projects
    * myapp-a
      * .enonic-cli: xp.sandbox=customer-a
    * office-league


## CLI options

### Default values

* Default project: Current directory
* Default sandbox: Sandbox associated to the current project

### Sandbox commands

* `enonic sandbox`   # List available sandbox commands
* `enonic sandbox help [command]`   # Display help page for a specific sandbox command
* `enonic sandbox ls`   # List all sandboxes in the CLI folder (and point out the running one and the one associated to the current project)
* `enonic sandbox set [sandboxName]`   # Set the sandbox associated to the current project
* `enonic sandbox start [sandboxName]`   # Start the sandbox (enonic distro pointing to this sandbox home). Create if not existing
* `enonic sandbox stop` # Stop XP  
* `enonic sandbox new`   # Wizard: Create a new sandbox (Download XP distro if necessary, copy the home from the XP distro). Propose 
* `enonic sandbox delete [sandboxName]`   # Delete a sandbox

### Project commands

* `enonic project`      # List available project commands
* `enonic project help [command]`   # Display help page for a specific project command
* `enonic project ls`   # List all projects in the CLI folder (and point out the current one)
* `enonic project set [projectName]`  # Chdir to the project directory   
* `enonic project new`  # Wizard: Init-app + Chdir + Create sandbox if necessary
* `enonic project clean [projectName]`  # Gradle clean   
* `enonic project build [projectName]`  # Gradle build  
* `enonic project deploy [projectName]` # Gradle deploy  
* `enonic project publish [projectName]`# Gradle publishToMavenLocal or publish
* `enonic project delete [projectName]` # Delete the application directory
* `enonic project add (part|service|page|...) [projectName]`      # Wizard: Add part/service/page/... in the project
* `enonic project remove (part|service|page|...) [projectName]`      # Remove part/service/page/... from the project

### Toolbox commands

* `enonic toolbox`      # List available toolbox commands
* `enonic toolbox help [command]`   # Display help page for a specific toolbox command
* `enonic toolbox delete-snapshots`   # Deletes snapshots, either before a given timestamp or by name.
* `enonic toolbox dump`               # Export data from every repository.
* `enonic toolbox export`             # Export data for a specified path.
* `enonic toolbox import`             # Import data from a named export.
* `enonic toolbox install-app`        # Install an application from URL or file
* `enonic toolbox list-snapshots`     # Returns a list of existing snapshots with name and status.
* `enonic toolbox load`               # Import data from a dump.
* `enonic toolbox reindex`            # Reindex content in search indices for the given repository and branches.
* `enonic toolbox reprocess`          # Reprocesses content in the repository.
* `enonic toolbox restore`            # Restores a snapshot of a previous state of the repository.
* `enonic toolbox set-read-only`      # Toggle read-only mode for server or single repository
* `enonic toolbox set-replicas`       # Set the number of replicas in the cluster.
* `enonic toolbox snapshot`           # Stores a snapshot of the current state of the repository.
* `enonic toolbox upgrade`            # Upgrade a dump.
* `enonic toolbox vacuum`             # Removes unused blobs and binaries from blobstore

## Use cases
* First time user create and deploy locally new app
  * `enonic project new`
  * `enonic sandbox start`
  * `enonic project deploy`
* Deploying an app to a different sandbox
  * `enonic sandbox set customer-b`
  * `enonic project deploy`
* Testing a project for a new version of enonic xp
  * `enonic sandbox new`
  * `enonic sandbox set new-sandbox`
  * `enonic sandbox start`
  * `enonic project deploy`
