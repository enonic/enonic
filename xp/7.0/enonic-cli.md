# Enonic CLI

* As a user, I want to be able to manage my installations, homes and projects from a single command

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
  * homes
    * default
    * customer-a
    * customer-b
  * projects
    * myapp-a
    * office-league
  * java
    * jdk-1.8
    * jdk-1.11
  * context.properties


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
