# Screen Layouts

## Pages

* Menu (Navigation bar on the side)
  * Log-in or Log-out
  * Navigate to
    * Foos/TableTennis leagues list
    * Profile
    * Home/Newsfeed (v2)
* Home page
  * Sign up / Log-in
  * Continue without login -> All/Your leagues list (if logged in or not)
* Your leagues list (logged in)
  * Displays list of leagues you are a part of
  * Join a league button  -> All leagues list
  * Create a league button
* All leagues list 
  * Displays list of all leagues
  * Create league
* League profile
  * Players list summary (ranked) -> Players list
  * Teams list summary (ranked) -> Teams list
  * Latest games list summary -> Games list
  * Rules (Generated text from the league config)
  * Join button
  * Edit button (if owner)
* League creation/edit
  *  Inputs
    * Name
    * Picture
    * Sport
    * Description
    * Config (appears on sport selection, default values)
    * Create/Save button -> League profile
    * Delete button -> Leagues list (v2: Notification)
* Players list (for a League)
  * Ranked list of players -> Player profile
  * Graph
  * Add player to league button (v2)
* Teams list (for a League)
  * Ranked list of teams -> Team profile
  * Graph
  * Add team to league button (v2)
* Player profile
  * Picture
  * Basic data: Name, Left/Right handed, Nationality, (Configurable attributes?), ...
  * Games
  * Statistics (v2)
  * Teams
    * Create a new team
  * Leagues (show your rank in that league)
  * Edit button
  * Badges (v2)
* Player creation/edit
  *  Inputs
    * Name
    * Nickname
    * Picture
    * Nationality: String //Enum
    * Handedness: String //Enum: Right, left, ambidextrous
    * Description
    * Create/Save button -> Player profile (v2: Notification)
    * Delete button -> Player list (v2: Notification)
* Team profile
  * Picture
  * Basic data: Name, ...
  * Players
  * Games
  * Statistics (v2)
  * Leagues (show your rank in that league)
  * Edit button
  * Badges (v2
* Team creation/edit
  *  Inputs
    * Name
    * Picture
    * Description
    * Create/Save button -> Player profile (v2: Notification)
    * Delete button -> Player list (v2: Notification)
* Newsfeed (v2)
  * Displayed instead of the home page if the user is logged in
  
    
  
## Page hierarchy

Page | Path
---- | ----
Home or Newsfeed | /
Your leagues | /leagues(?player=playerId) (?)
Enonic Foos league | /leagues/enonic-league
Enonic Foos league edit | /leagues/enonic-league/edit
Enonic Foos league teams | /leagues/enonic-league/teams
Enonic Foos league players | /leagues/enonic-league/players
ARO profile | /players/aro
Elastic backend profile | /teams/elastic
