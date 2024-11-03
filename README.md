# NBA Winning Percentage Prediction

This project uses a linear regression model to try and predict a Nba team's
winning percentage for a given season. Some of the variables used are 
nba team statistics such as shot attempts, rebounds, points per game.

## Dataset

The dataset used for this project is sourced from Kaggle:
- [NBA Team Stats (2000 to 2023)](https://www.kaggle.com/datasets/mharvnek/nba-team-stats-00-to-18?select=nba_team_stats_00_to_23.csv)

Right now the linear regression model has been built. I may add other models and data analysis before Milestone 4.

## Input Variables

The following variables are used in the model:

- `team`
- `win_percentage`
- `points per game`
- `2-pt field goals attempted per game`
- `2-pt field goals made per game`
- `three pointers made per game`
- `three pointers attempted per game`
- `free throws made per game`
- `free throws attempted per game`
- `offensive rebounds per game`
- `defensive rebounds per game`
- `assists per game`
- `turnovers per game`
- `steals per game`
- `blocks per game`
- `blocked attempts per game`
- `personal fouls per game`
- `season`

### Categorical Variables
- `team`
- `season(added in 2nd model)`

## Seasons Selected

Using a random number to start, I used stratified random sampling to sample in 4-year intervals to reduce bias that the best teams cause. Note that I accidently skipped a year up to 2011-2012. I may go back and fix this. The seasons chosen are:
- 2002-2003
- 2006-2007
- 2011-2012
- 2015-2016
- 2019-2020
- 2023-2024


## Data Transformation

- Transformed the points, field_goals_made, field_goals_attempted, three_pointers_made, three_pointers_attempted, free_throws_made, free_throws_attempted, offensive_rebounds, defensive_rebounds, assists, turnovers, steals, blocks, blocks_attempted, personal_fouls, personal_fouls_drawn, plus_minus columns into averages by dividing by the total number of games played for that team in the season. 
- Removed the field_goal_percentage, three_pointers_percentage, free_throw_percentage since they are derived averages for the total success attempts and total attempts.
- Removed derived averages such as `field_goal_percentage`, `three_pointers_percentage`, and `free_throw_percentage` since they depend on attempts/successful makes.
- Created `two_pointers_made` and `two_pointers_attempted` by subtracting `three_pointers_made` from `field_goals_made` and `three_pointers_attempted` respectively. This adjustment accounts for the aggregate nature of field goals.
- Removed `personal_fouls_drawn` due to missing data from earlier seasons.
- Removed `games_played` since it rarely differs from 82.
- Removed `plus/minus` as it directly determines the winner of the game.

## Team Relocation Handling

Resolved the issue of teams moving cities by maintaining a team entity related to a city. The following combinations were made:
- Seattle/OKC
- NJN/Brooklyn (permanent relocation)

New Orleans and Charlotte are kept as single entities. The meaning behind this variable is more with the City than the franchise/ownership.

## City to Integer Mapping

A categorical variable mapping individual teams to integer values is as follows:

| City                  | Integer |
|-----------------------|---------|
| Boston                | 1       |
| Denver                | 2       |
| Seattle/OKC           | 3       |
| Minnesota             | 4       |
| LAC                   | 5       |
| Dallas                | 6       |
| NY                    | 7       |
| Milwaukee             | 8       |
| New Orleans           | 9       |
| Phoenix               | 10      |
| Cleveland             | 11      |
| Indiana               | 12      |
| LAL                   | 13      |
| Orlando               | 14      |
| Philadelphia          | 15      |
| Golden State          | 16      |
| Miami Heat            | 17      |
| Sacramento            | 18      |
| Houston               | 19      |
| Chicago Bulls         | 20      |
| Atlanta Hawks         | 21      |
| Brooklyn              | 22      |
| Utah Jazz             | 23      |
| Memphis               | 24      |
| Toronto Raptors       | 25      |
| San Antonio           | 26      |
| Charlotte             | 27      |
| Portland              | 28      |
| Washington Wizards    | 29      |
| Detroit Pistons       | 30      |

## Year Column Transformation

The year column has been changed to integer values corresponding to the year 2000 plus the number. For example, 2002-03 becomes 3. This column should technically be treated as a categorical variable, and I created a second model to address this.