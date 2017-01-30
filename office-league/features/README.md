# Features 


## Features
 
 
### Core

:soccer: - PWA feature

* Home page 
  * Marketing the "Foosball" service, rules, etc
  * Add to home screen :soccer:
* Create/edit players
* Create/edit teams
* Support league (scope for games)
* Record a game
  * Select by team/player
  * Select players (Invites?)
  * Enter goals
  * Offline mode :soccer:
  * Sync game data when back online :soccer: 
* Game summary page
* Player profile
  * Linked to a user
* Team profile
* Create tournaments
  * Cup, league, etc
  * Select players and create cup
  * Generate seeds based on ranking
* Organization page summary
  * Show ranking changes, latest games, etc
* Notifications for games played from your org :soccer:
* Leaderboard / ranking page
  * Elo ranking system like in Foos 1.0, or similar
* Organization Administrator page 
  * Possibility for create/delete players, teams, games
* Live games and tournament
  * Page that shows game being played
  * Use WebSockets to update game details
* Comments on games
  * Both for during game (like a chat) and after (like a blog comments)

### Version 2
* Newsfeed (Last games of the leagues) (Will ease up the notifications also)  * Tweet/comment from profile
* Comments/Post/Article on wall
* Record game improv.
  * Pause/Undo/Redo
  * Effects (music / sound on goal strikes)?
* Badges
  * Achievements, e.g. 10 wins in a row
* Share (game) on social media
* Different type of office games/sport (chess, foos, pingpong, football, ...)
* Generated comments
* Invite players
  * Send notifications to players invited (select people or to org) :soccer:

### Version 3
* Localization

### Version 4
* Sensors (Connected by bluetooth) to record the score
* Camera (Goal replays)

## Technical choices
* The data should be retrieve from the back-end using GraphQL
* The data (except the landing pages of the blog posts) should be stored as node directly
