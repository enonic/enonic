# Enonic CLI

* As a user, I want to be able to manage my installations, homes and projects from a command-line interface

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
  
## File structure

* ~/enonic-cli
  * distributions
    * 6.15.0
    * 7.0.0-SNAPSHOT
  * homes(sandboxes)
    * default
    * customer-a
      * .enonic: xp.version=6.15.1
    * customer-b
  * projects
    * myapp-a
      * .enonic-cli: xp.home=customerA
    * office-league


## CLI options

### XP commands

`enonic-cli xp start [version]`   # Start XP. Download if necessary  
`enonic-cli xp stop` # Stop XP  
`enonic-cli xp set` # Set default xp version  
`enonic-cli xp list` # List all xp installations (and point out the default one)  

### Project commands

`enonic-cli project new`   # Init-app +Wizard  
`enonic-cli project delete`   # Delete an application directory  
`enonic-cli project clean`   # Gradle clean   
`enonic-cli project build`   # Gradle build  
`enonic-cli project install`   # Gradle install  
`enonic-cli project deploy`   # Gradle deploy  
`enonic-cli project set`   # cd to the project directory  
`enonic-cli project list`   # List all projects  
`enonic-cli project add [part|service|page]`   # Add part in project app. +Wizard  

### Home commands

`enonic-cli home new`   # Create a new xp_home (empty folder)  
`enonic-cli home delete`   # Delete an xp_home directory  
`enonic-cli home set`   # Set the current xp_home context   
`enonic-cli home list`   # List the existing xp_home directories


# To be discussed

* How to install Java? Include with the CLI, include with distro, download by the CLI?
