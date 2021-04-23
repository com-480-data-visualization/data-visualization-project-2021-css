# Project of Data Visualization (COM-480)

| Student's name | SCIPER |
| -------------- | ------ |
| Alexandre Cadillon| 288684|
|Abed Alrahman Shabaan | 237731|
| Sabaa Karim | 269647 |

[Milestone 1](#milestone-1) • [Milestone 2](#milestone-2) • [Milestone 3](#milestone-3)

## Milestone 1 (23rd April, 5pm)

**10% of the final grade**

This is a preliminary milestone to let you set up goals for your final project and assess the feasibility of your ideas.
Please, fill the following sections about your project.

*(max. 2000 characters per section)*

### Dataset

We decided to use a dataset from [Kaggle](https://www.kaggle.com/) as suggested. The dataset is called [European Soccer Database](https://www.kaggle.com/hugomathien/soccer). It contains data about teams, players and matches from 11 European leagues. There are +10,000 players and +25,000 matches from 2008 to 2016.

Match data contains team names, the date and the result. Additionally, team line ups, detailed match events (goal types, possession, corner, cross, fouls, cards etc…) and multiple betting odds are available for most games.

Players and teams attributes are sourced from EA Sports's FIFA video game series. 

The dataset is fairly clean but there is some work to be done in the matches table. When available, match events need to be parsed to identify meaningful stats like goals or cards, and link them to particular players.


### Problematic


Our inspiration comes from the [Too-Much-Talent Effect](https://journals.sagepub.com/doi/10.1177/0956797614537280), a study published in Psychological Science Journal.

Whether they are trying to build a sports team or a team of engineers, most people will choose talent as their top criteria in recruiting. Is selecting individuals only based on talent the most effective way? That's what the study was about. They looked into the relationship between team member's individual talents and overall team performance. They studied around 400 football matches from the 2010 and 2014 world cup. Surveys have shown that 37% of people believe that it's a linear relationship, the more stars in a team there is, the more successful it becomes. This study shows that individual talent helps improve the team's performance up to a certain point, after which it may start having a negative effect.

We would like to study this topic through our dataset and to produce an interactive visualization tool that will allow us to generate insights on this topic. It may make more people aware of this effect and even help some of that 37% change their minds.

### Exploratory Data Analysis

Preprocessing of the player data shows that we have a total of 11060 players in the dataset, for each of them we have multiple `attributes` entries, those come from the FIFA video game data. We will use the overall score from that table as the rating of each player.
We have one entry per player per season for the first years, but then we start to have multiple entries per player, which means we will have to average those.

![Entry date distribution](dates.png)

Taking for example the very last year in the dataset (2016) we get the following top 10 list

![stars list](stars.png)

Doing a preprocessing of the league, team, and match data, we are able to infer how many matches each team won, and so we can guess the winner of each league each season as the winner of most matches, this guess checks out against the ground truth.

![winner list](winners.png)

We can also compute meaningful statistics for every season of every league. Here is the Swiss league:

|    | country_name   | league_name              | season    |   number_of_stages |   number_of_teams |   avg_home_team_scors |   avg_away_team_goals |   avg_goal_dif |   avg_goals |   total_goals |
|---:|:---------------|:-------------------------|:----------|-------------------:|------------------:|----------------------:|----------------------:|---------------:|------------:|--------------:|
| 79 | Switzerland    | Switzerland Super League | 2015/2016 |                 36 |                10 |               1.78333 |               1.36111 |       0.422222 |     3.14444 |           566 |
| 80 | Switzerland    | Switzerland Super League | 2014/2015 |                 36 |                10 |               1.60556 |               1.26667 |       0.338889 |     2.87222 |           517 |
| 81 | Switzerland    | Switzerland Super League | 2013/2014 |                 36 |                10 |               1.61111 |               1.27778 |       0.333333 |     2.88889 |           520 |
| 82 | Switzerland    | Switzerland Super League | 2012/2013 |                 36 |                10 |               1.51111 |               1.05556 |       0.455556 |     2.56667 |           462 |
| 83 | Switzerland    | Switzerland Super League | 2011/2012 |                 36 |                10 |               1.45062 |               1.17284 |       0.277778 |     2.62346 |           425 |
| 84 | Switzerland    | Switzerland Super League | 2010/2011 |                 36 |                10 |               1.57222 |               1.41111 |       0.161111 |     2.98333 |           537 |
| 85 | Switzerland    | Switzerland Super League | 2009/2010 |                 36 |                10 |               1.99444 |               1.33333 |       0.661111 |     3.32778 |           599 |
| 86 | Switzerland    | Switzerland Super League | 2008/2009 |                 36 |                10 |               1.75556 |               1.24444 |       0.511111 |     3       |           540 |


Or summarize matchups between teams. Here are some matchups for Real Madrid at home.

|      | country_name   | league_name     | home_team      | away_team               |   games |   seasons |   home_team_goals |   away_team_goal |   home_wins |   draws |   laway_wins |
|-----:|:---------------|:----------------|:---------------|:------------------------|--------:|----------:|------------------:|-----------------:|------------:|--------:|-------------:|
| 4852 | Spain          | Spain LIGA BBVA | Real Madrid CF | Athletic Club de Bilbao |       8 |         8 |                34 |                9 |           8 |       0 |            0 |
| 4859 | Spain          | Spain LIGA BBVA | Real Madrid CF | FC Barcelona            |       8 |         8 |                12 |               22 |           2 |       1 |            5 |
| 4881 | Spain          | Spain LIGA BBVA | Real Madrid CF | Valencia CF             |       8 |         8 |                13 |                7 |           4 |       4 |            0 |
| 4878 | Spain          | Spain LIGA BBVA | Real Madrid CF | Sevilla FC              |       8 |         8 |                27 |               11 |           7 |       0 |            1 |
| 4853 | Spain          | Spain LIGA BBVA | Real Madrid CF | Atlético Madrid         |       8 |         8 |                13 |                8 |           4 |       1 |            3 |
| 4864 | Spain          | Spain LIGA BBVA | Real Madrid CF | Málaga CF               |       8 |         8 |                25 |                7 |           6 |       2 |            0 |
| 4860 | Spain          | Spain LIGA BBVA | Real Madrid CF | Getafe CF               |       8 |         8 |                32 |                9 |           8 |       0 |            0 |
| 4868 | Spain          | Spain LIGA BBVA | Real Madrid CF | RCD Espanyol            |       8 |         8 |                27 |                5 |           6 |       2 |            0 |
| 4882 | Spain          | Spain LIGA BBVA | Real Madrid CF | Villarreal CF           |       7 |         7 |                22 |                7 |           6 |       1 |            0 |
| 4863 | Spain          | Spain LIGA BBVA | Real Madrid CF | Levante UD              |       6 |         6 |                19 |                3 |           6 |       0 |            0 |



### Related work

[The Too-Much-Talent Effect: Team Interdependence Determines When More Talent Is Too Much or Not Enough](https://journals.sagepub.com/doi/10.1177/0956797614537280): Roderick I. Swaab, Michael Schaerer, Eric M. Anicich, Richard Ronay, Adam D. Galinsky

## Milestone 2 (7th May, 5pm)

**10% of the final grade**


## Milestone 3 (4th June, 5pm)

**80% of the final grade**


## Late policy

- < 24h: 80% of the grade for the milestone
- < 48h: 70% of the grade for the milestone

