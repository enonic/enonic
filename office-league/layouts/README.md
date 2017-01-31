# Screen Layouts

## Pages

* Menu (Navigation bar on the side)
  * Log-in or Log-out
  * Navigate to
    * Foos/TableTennis leagues list
    * Profile
    * Home/Newsfeed (v2)
* Home page
  * Log-in
  * Browse league
  * Presentation/Marketing of the product
* Leagues list (for a sport)
* League presentation
  * Players list 
  * Teams list 
  * Games list 
  * Rules
* League creation/edit (dialog)
* Players list (for a League)
  * Ranked list of players
* Teams list (for a League)
  * Ranked list of teams
* Player profile
  * Picture
  * Basic data: Name, Left/Right handed, Nationality, (Configurable attributes?), ...
  * Games
  * Statistics
  * Teams
    * Create a new team
  * Leagues
  * Badges (v2)
* Player creation/edit (dialog)
* Team profile
  * Picture
  * Basic data: Name, Left/Right handed, (Configurable attributes?), ...
  * Players
  * Games
  * Statistics
  * Leagues
  * Badges (v2)
* Team creation/edit (dialog)
* Newsfeed (v2)
  * Displayed instead of the home page if the user is logged in
  



    
  
## Page hierarchy

Page | Path
---- | ----
Home or Newsfeed | /
Foos leagues | /leagues?sport=foos
Table tennis leagues | /leagues?sport=tabletennis
Enonic Foos league | /leagues/enonic-foos
Enonic Foos league teams | /leagues/enonic-foos/teams
Enonic Foos league players | /leagues/enonic-foos/players
ARO profile | /players/aro
Elastic backend profile | /teams/elastic
