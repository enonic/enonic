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

enonic-cli
  xp
    start [version]
      Starts XP. Download if necessary
    stop
      Stops XP
    set
      Set default xp version
    list
      List all xp installations (and point out the default one)
  project
    new
      Init-app +Wizard
    delete
    clean
      Gradle clean
    build
      Gradle Build
    install
      Gradle install
    deploy
      gradle deploy
    set
      cd to the project directory
    list
      list all projects
    add part/service/page
      Wizard
  home
    new
    delete
    set
    list
    new
