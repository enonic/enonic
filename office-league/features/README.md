# Features & Requirements

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
* Sensors (Connected by bluetooth) to record the score
* Camera (Goal replays)
* Ball recognition ? (V3)
* Blog posts
* Pictures for game summary
* Different type of office games/sport (chess, foos, pingpong, football, ...)
* Localization
* Newsfeed (Last games of the leagues) (Will ease up the notifications also) + Tweet/comment from profile


# Technical choices
* GraphQL
* Store as possible as node (not content)
