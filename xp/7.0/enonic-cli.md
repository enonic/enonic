# Enonic CLI

* As a user, I want to be able to manage my installations, homes and projects from a command-line interface

## Link Project/Home/EnonicXP

* XP Home created with the CLI will have a reference to a Enonic XP version
* XP Project (apps/libs) created with the CLI will have a reference to a XP Home
* These references will be stored in a file '.enonic-cli' at the root of the Home/Project

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
    * .enonic-cli (Stores the current running XP distributions
    * 6.15.0
    * 7.0.0-SNAPSHOT
  * homes(sandboxes)
    * default
    * customer-a
      * .enonic-cli: xp.version=6.15.1
    * customer-b
  * projects
    * .enonic-cli (Stores the current project context)
    * myapp-a
      * .enonic-cli: xp.home=customerA
    * office-league


## CLI options

### XP commands

* `enonic-cli xp` # List XP commands
* `enonic-cli xp ls` # List all distributions in the CLI folder (and point out the running one)  
* `enonic-cli xp start [version=latest_release]`   # Start XP. Download if necessary  
* `enonic-cli xp stop` # Stop XP 

### Home commands

* `enonic-cli home`   # List Home commands
* `enonic-cli home ls`   # List all homes in the CLI folder
* `enonic-cli home new`   # Create a new home (copy the home from the XP version)
* `enonic-cli home delete`   # Delete an home
* `enonic-cli home set`   # Set the default home context for the current project

### Project commands

* `enonic-cli project`      # List Project commands
* `enonic-cli project ls`   # List all projects in the CLI folder
* `enonic-cli project new`  # Wizard: Init-app
  * Execute what is today Init-app
  * Cd to the project directory
* `enonic-cli project clean [name=current_repository]`  # Gradle clean   
* `enonic-cli project build [name=current_repository]`  # Gradle build  
* `enonic-cli project install [name=current_repository]`# Gradle install  
* `enonic-cli project deploy [name=current_repository]` # Gradle deploy  
* `enonic-cli project set`                              # cd to the project directory   
* `enonic-cli project delete [name=current_repository]` # Delete the application directory
* `enonic-cli project add (part|service|page|...)`      # Wizard: Add part/service/page/... in the project

### Default values

* The default project is
** The current directory
** If the current directory is not a CLI project, 


## Use cases
* First time user create and deploy locally new app
  * enonic-cli project new //Creates a directory, Cd, Init-app
  * enonic-cli project deploy //Check if XP and home (downloads if missing and start), Gradle deploy
* Deploying an app to different homes
* Switching between homes and projects
* Testing a project for a new version of enonic xp
* OPT: Run a cluster locally
* Run multiple instances of Enonic XP
* Install app from market

## Example of use
* Install Enonic CLI
  * brew install enonic-cli
  * apt-get install enonic-cli
  * //Or download manually
* Start Enonic XP (download if necessary)
  * enonic-cli xp start 6.15
* Create a new app
  * enonic-cli project new
* Build & deploy the application
  * enonic-cli project deploy
