# Foosball app

This document describes the Foosball app features. Items can be linked to issues or feature documents.

## Goal

The goal for the Foosball app is to create a full-blown Progressive Web App from scratch. 
We would like to explore every relevant aspect of PWA from front-end to back-end.

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

## Features

:soccer: - PWA feature

* Home page 
 + Marketing the "Foosball" service, rules, etc
 + Add to home screen :soccer:
* Create/edit players
* Create/edit teams
* Support organizations (scope for players and teams)
* Record a game
 + Select by team/player
 + Select players (Invites?)
 + Enter goals
 + Pause/Undo/Redo
 + Effects (music / sound on goal strikes)?
 + Offline mode :soccer:
 + Sync game data when back online :soccer: 
* Game summary page
* Player profile
 + Linked to a user
* Team profile
* Create tournaments
 + Cup, league, etc
 + Select players and create cup
 + Generate seeds based on ranking
* Organization page summary
 + Show ranking changes, latest games, etc
* Notifications for games played from your org :soccer:
* Leaderboard / ranking page
 + Elo ranking system like in Foos 1.0, or similar
* Organization Administrator page 
 + Possibility for create/delete players, teams, games
* Live games and tournament
 + Page that shows game being played
 + Use WebSockets to update game details
* Comments on games
 + Both for during game (like a chat) and after (like a blog comments)
* Share (game) on social media
* Badges
 + Achievements, e.g. 10 wins in a row
* Invite players
 + Send notifications to players invited (select people or to org) :soccer:


