# Data

## Content types
* Landing page

## Data (node)
* League
  * Name: String
  * Sport: String //Enum: "foos", "tabletennis"
  * Image: Binary
  * Config: PropertySet
  * Stats
    * // Additional generated stats
      
* Player
  * Name: String
  * Image: Binary
  * Nationality: String //Enum
  * Handed: String //Enum: Right, left, ambidextrous
  * Description: String
  * // Additional generated stats
* Team
  * Name: String
  * Image: Binary
  * Players: PlayerId[]
* Game
  * Time: Date/Time  
  * Points
    * PlayerId: PlayerId
    * Time: Int
    * Against: Boolean 
  * Blue: PlayerId[1-2]
  * Red: PlayerId[1-2]
  * Stats
    * // Additional generated stats (winners, player score, ranking diff, )
* Comment
  * Author: PlayerId //Opt. Nil if generated
  * Text: String
  * Media: Binary
  
  
  
## Data structure

* /leagues
* /leagues/enonic-foos
* /leagues/enonic-foos/games
* /leagues/enonic-foos/games/game1
* /leagues/enonic-foos/games/game1/comments
* /leagues/enonic-foos/games/game1/comments/comment1
* /leagues/enonic-foos/games/game2
* /leagues/enonic-foos/games/game2/comments
* /teams
* /teams/elastic
* /players
* /players/aro



