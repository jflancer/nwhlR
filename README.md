# nwhlR

`nwhlR` is an R package for working with NWHL play-by-play data. This 
package can be used to scrape play by play data from the NWHL website, and
additionally compile the data into player and team summaries.

## Installation

First install the package `devtools` if you haven't already
``` r
#install.packages("devtools")
devtools::install_github("jflancer/nwhlR")
```

## Functionality

This package consists of 5 main functions. 

**To scrape for game ids:**
- `get_id_date` gets all game ids for a specified date
- `get_id_schedule` gets all game ids for a specified season and team(s)

Additionally, game ids can be found in the url when browsing games, for example ```https://www.nwhl.zone/game/show/14668259?subseason=327151&referrer=2758855```.

When viewing the webpages, the unique game id is the first string of digits, in this case ```14668259```

**To scrape for play by play**
- `get_play_by_play` gets the play by play data given one or multiple game ids

**To compile play by play**
- `get_player_summary` converts the play by play data into a game summary for each player
- `get_team_summary` converts the play by play data into a team summary for both teams


### Use

The easiest way to use this package is to follow the format
``` r
# Get the game ids using one of two functions or this could be manual
game_ids <- get_id_date(Season = "20182019", Year = "2018", Month = "12", Day = "09")
# game_ids <- get_id_schedule(Season = "20182019", teams = "BUF")
pbp_data <- get_play_by_play(game_ids)
player_stats <- get_player_summary(pbp_data)
team_stats <- get_team_summary(pbp_data)

```

### `get_id_date`
This function takes in several parameters and will return a vector of game ids for a given date
* Season | an 8 digit season, ex. "20182019"
* Year | a four digit year parameter yyyy, ex. "2018"
* Month | The specified month, must be using format mm, ex. April = "04"
* Day | The specified date, must be using format dd, ex. the eighth = "08"

### `get_id_schedule`
This function returns all game ids for given teams in a given season. Default is set to 20182019, and all teams.
* Season | an 8 digit season, ex. "20182019"
* Teams | the team abbreviations used by the NWHL- as follows "BOS", "BUF", "CTW", "MET", "MIN"

### `get_play_by_play`
This function will return a tidy play-by-play file given a single, or multiple game ids
* game_ids | vector of game ids in either character or numeric format

### `get_player_summary`
This function will give you player stats for all games specified in the play-by-play.
* pbp_df | dataframe consisting of play by play data from get_play_by_play

### `get_team_summary`
This function will give you team stats for all games specified in the play-by-play
* pbp_df | dataframe consisting of play by play data from get_play_by_play


