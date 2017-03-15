# Features 


## Features
 
 
### Core

:soccer: - PWA features
    
- [x] Home page 
  - [x] Presentation of the foosball app
  - [ ] Add to home screen :soccer:
- [ ] Marketing page 
- [ ] Create/edit players
- [ ] Create/edit teams
- [x] Support league (scope for games)
* Record a game
  - [x] Select players
  - [x] Enter goals (Self goals?)
  - [x] Offline mode
  - [ ] Sync game data when back online :soccer: 
  - [ ] Team creation if team does not exist
  - [ ] Rating computation/adaptation
- [ ] Game page
- [x] Player profile
  - [x] Linked to a user
- [x] Team profile
- [x] League page summary
  - [x] Show ranking changes, latest games, etc
- [x] Leaderboard / ranking page (by league)
  - [x] Elo ranking system like in Foos 1.0, or similar
- [x] Join a league
  - [x] For a player, this can be done from the league presentation (ex: a Join button) or through their profile.
  - [ ] For a team, it is dynamically associated if the 2 players are in the league
    * Can happen when a player joins/leave a league, a team is created/updated/deleted.
- [x] Localization research

### Version 1.1
* Live games and tournaments
  * Page that shows game being played
  * Use WebSockets to update game details
- [ ] Notifications (On game played in your league, send notification with a link to live game page)
  - [ ] Push notification server
  - [ ] Push notification client :soccer:
* Comments on games
  * Both for during game (like a chat) and after (like a blog comment)

### Version 2
* Invite players to game
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
* Seach/filter of league

### Version 3
* CMS Integration
  * Blog posts
  * About/Contact
* Multiple languages

### Version 4
* Sensors (Connected by bluetooth) to record the score
* Camera (Goal replays)

## Technical requirements
* The data should be retrieve from the back-end using GraphQL
* The data (except the landing pages) should be stored as node directly
* PWA
  * Caching only after login
  * All pages rendered by angular
    * Admin preview?
    * Search engines
    * Deep-linking
  * Routing should be similar on server and client (ie 404 & 403)
  * Every other page should return the angular page
  * Add to homescreen = /
  * Languages

