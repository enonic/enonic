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
    * Teams 
      
* Player
  * Name: String
  * Image: Binary
  * 
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

/leagues/enonic-foos/games
/leagues/enonic-foos/comments


