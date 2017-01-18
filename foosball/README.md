# Foosball app

This document describes the Foosball app features. Items can be linked to issues or feature documents. Items can also be annotated with the following icons:

## Goal

The goal for the Foosball app is to create a full-blown Progressive Web App from scratch. 
We would like to explore every relevant aspect of PWA from front-end to back-end.

##Features
* Record a game (PWA - offline mode, sync when back online)
 + Select by team/player
 + Select players (Invites?)
 + Enter goals
 + Pause/Undo/Redo
 + Effects (music / sound on goal strikes)?
* Create/edit players
* Create/edit teams
* Support organizations (scope)
* Game summary page
* Player profile (linked to a user)
* Team profile
* Rule page
* Create tournament (cup/league)
 + select players and create cup (generate seeds based on ranking)
* Home page summary (ranking changes, latest games, etc)
* Notifications for games in your org (PWA) 
* Leaderboard / ranking page
* Organization Administrator page (create/delete players, games)
* Live games and tournament
* Comments on games (during game and after)
* Share (game) on social media
* Badges (achievements, e.g. 10 wins in a row)
* Invite players (send notifications) (select people or to org)

## Pages
* Team list / ranking
* Player list / ranking
* Team profile
* Player profile
* Player profile
* Game recording


## Blog post requirements
* Both developers and non-techies must be able to relate to the concept
* Should have an interesting data model, with potentially big volumes
* Needs to provide a relevant offline experience
* Support storing of personal settings or data
* Login support with popular ID providers such as Google and Facebook
* Support User generated content
* Provide transactions of some kind
* Relevant use of push notifications
* Nice URL handling and deep linking support
* Include public facing content, for easy access and search robot indexing
* Support localization
* Re-useable beyond Enonic, potentially as a cloud service
* Interaction with physical devices / IoT if possible

## Blog post features 
* Public pages for marketing the "Foosball" service, rules, etc etc
* Login to register new players
* Teams, players and games would be the core datamodel - with a growing data-set
* Notify players of upcoming games, or changes to their ranking
* Offline support for playing and recording games
* Deep linking into content, player statistics and game info
* User comments on games played
* Challenge other users for a new game