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
  * Enter goals (Self goals?)
  * Offline mode :soccer:
  * Sync game data when back online :soccer: 
  * Team creation if team does not exist
* Game summary page
* Player profile
  * Linked to a user
* Team profile
* League page summary
  * Show ranking changes, latest games, etc
* Notifications for games played from your league :soccer:
* Leaderboard / ranking page (by league)
  * Elo ranking system like in Foos 1.0, or similar
* Administration
  * Possibility for create/delete players, teams, games
* Live games and tournaments
  * Page that shows game being played
  * Use WebSockets to update game details
* Comments on games
  * Both for during game (like a chat) and after (like a blog comment)
* Join a league
  * For a player, this can be done from the league presentation (ex: a Join button) or through their profile.
  * For a team, it is dynamically associated if the 2 players are in the league
    * Can happen when a player joins/leave a league, a team is created/updated/deleted.
  

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
* Create tournaments
  * Cup, league, etc
  * Select players and create cup
  * Generate seeds based on ranking

### Version 3
* Localization
* Blog posts/rticles

### Version 4
* Sensors (Connected by bluetooth) to record the score
* Camera (Goal replays)

## Technical requirements
* The data should be retrieve from the back-end using GraphQL
* The data (except the landing pages) should be stored as node directly
