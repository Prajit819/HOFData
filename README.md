## Baseball Hall of Fame Predictions

## Background

This project was designed to use machine learning against Major League Baseball (MLB) data in order to predict the possibility of being nominated for the Hall of Fame.


## Process

KEYS:
    HOF: players nominated or inducted in the Hall of Fame
    non-HOF: players not nominated or inducted in the Hall of Fame

* The data set was accessed through the Sean Lahman Baseball Database: http://www.seanlahman.com/baseball-archive/statistics/
    * This data set was accessed through MySQL. The dataset covered baseball seasons from 1871 through 2016.
    * Tables primarily used were:
        * Master
        * Batting
        * Pitching
        * Fielding
        * Hall of Fame
* According to project objectives the target data was based on players that had either been inducted or nominated to the Hall of Fame.
    * Removed umpires and managers
    * Seperated Pitchers from Fielders (some players were cross overs)
* For a machine learning approach the data required also consisted of all other players who were not either inducted or nomitated for the Hall of Fame.
    * The Lahman database is structured by season stats for each player. Therefore, career stats had to be calculated.
    * The stat, Wins Above Replacement (WAR) was also included in to the data set by scraping www.baseball-reference.com for each player.
        * WAR was used for fielders when calculating offensive status. WAR for pitchers proved to not be an important factor for various reasons.

## Calculating Batters

* Initial data accumulated consisted of 12,035 non-HOF and 680 HOF players.
* Prior to running a Random Forest (RF) algorithim the data was filtered by:
    * Slugging (SLG) '< 0.700' 
    * Batting Average (BA) '< 0.400'
    * Seasons played '> 4' and ' < 28'
* Applied filters resulted in a more refined data set of 4,585 non-HOF vs. 677 HOF (74/26)
* Data fields applied to the RF were BA, On-Base Percentage (OBP), SLG, WAR
* Final F1 score averaged to 0.91 

## Calculating Pitchers

* Initial data accumulated consisted of 8,852 non-HOF and 449 HOF players.
* Prior to running a Random Forest (RF) algorithim the data was filtered by:
    * Games played '> 100'
* Applied filters resulted in a more refined data set of 2,729 non-HOF vs. 386 HOF (75/25)
* Data fields applied to the RF were Earned Run Average (ERA), Wins, Strikeouts, Games Played, Opposing Batting Average (OBP)
    * Negative stats (Losses, Walks, Runs, etc.) were avoided
* Final F1 score average to 0.92

## Data Structuring and Calculation

* The 'data_building.ipynb' notebook accesses the MySQL DB and accumulates the Pitching/Batting data in to respective CSV files
* 'Batting_RandomForest.ipynb' accesses the dataset through the appropriate CSV and runs RF against the data
* 'Pitching_RandomForest.ipynb' accesses the dataset through the appropriate CSV and runs RF against the data
* 'Player War.ipynb' structures/scrapes for WAR stats against players for the above CSV files used in the RF process
