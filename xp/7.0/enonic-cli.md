# Enonic CLI

* As a user, I want to be able to manage my installations, homes and projects from a command-line interface

## Link Project/Sandbox/EnonicXP

* Sandboxes contain an XP home and have a reference to a specific Enonic XP version
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

* Enonic CLI, will create a hidden folder in the user folder to store the XP distributions, homes and projects.
* ~/.enonic-cli
  * distributions
    * 6.15.0
    * 7.0.0-SNAPSHOT
  * sandboxes
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

### XP commands

* `enonic xp` # List XP commands
* `enonic xp ls` # List all distributions in the CLI folder (and point out the running one)

### Sandbox commands

* `enonic sandbox`   # List Sandbox commands
* `enonic sandbox ls`   # List all sandboxes in the CLI folder (and point out the running one and the default one)
* `enonic sandbox start [sandboxName]`   # Start the sandbox.
* `enonic sandbox stop` # Stop XP  
* `enonic sandbox new`   # Wizard: Create a new sandbox (Download XP distro if necessary, copy the home from the XP distro)
* `enonic sandbox delete [sandboxName]`   # Delete a sandbox
* `enonic sandbox set [sandboxName]`   # Set the default sandbox for the current project

### Project commands

* `enonic project`      # List Project commands
* `enonic project ls`   # List all projects in the CLI folder
* `enonic project new`  # Wizard: Init-app + Chdir + Create sandbox if necessary
* `enonic project run [projectName]`  # = `enonic project deploy [projectName]` + `enonic sandbox start`
* `enonic project clean [projectName]`  # Gradle clean   
* `enonic project build [projectName]`  # Gradle build  
* `enonic project install [projectName]`# Gradle build + /api install 
* `enonic project deploy [projectName]` # Gradle deploy  
* `enonic project set [projectName]`  # Chdir to the project directory   
* `enonic project delete [projectName]` # Delete the application directory
* `enonic project add (part|service|page|...) [projectName]`      # Wizard: Add part/service/page/... in the project
* `enonic project remove (part|service|page|...) [projectName]`      # Remove part/service/page/... from the project

### Default values

* projectName: Current directory
* sandboxName: 
  * Running sandbox
  * If no running sandbox, sandbox associated to the current project

## Example of use
* Install Enonic CLI
  * brew install enonic-cli
  * apt-get install enonic-cli
  * //Or download manually
* Create a new app
  * enonic-cli project new
* Build, deploy the application
  * enonic-cli project run


## Use cases
* First time user create and deploy locally new app
  * enonic-cli project new 
  * enonic-cli project run
* Deploying an app to different homes
* Switching between homes and projects
* Testing a project for a new version of enonic xp
* OPT: Run a cluster locally
* Run multiple instances of Enonic XP
* Install app from market
