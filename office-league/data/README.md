# Data

## Content types
* Landing page

## Data (node)
* League
  * Name: String
  * Sport: String //Enum: "foos", "tabletennis"
  * Image: Binary
  * Description: String
  * Config: PropertySet
  * Admins: PlayerId[]
  * PlayersStats
    * PlayerId
    * Stats
      * Rating
      * Ranking ???
      * PreviousRating ???
      * PreviousRanking ???
  * Teams
    * TeamId
    * Stats
      * Rating
      * Ranking ???
      * PreviousRating ???
      * PreviousRanking ???

* Player
  * Name: String
  * Nickname: String
  * Image: Binary
  * Nationality: String //Enum
  * Handedness: String //Enum: Right, left, ambidextrous
  * Description: String
* Team
  * Name: String
  * Image: Binary
  * Description
  * Players: PlayerId[]
* Game
  * LeagueId: 
  * Time: Date/Time  
  * Goals
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
  * Likes: PlayerId[]
  
  
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



