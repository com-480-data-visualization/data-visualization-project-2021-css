# Project of Data Visualization (COM-480)

| Student's name | SCIPER |
| -------------- | ------ |
| **C**adillon Alexandre| 288684|
| **S**habaan Abed Alrahman | 237731|
| **S**abaa Karim | 269647 |

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

|       | player_name        |   overall_rating |
|------:|:-------------------|-----------------:|
|  6169 | Lionel Messi       |               94 |
|  1992 | Cristiano Ronaldo  |               93 |
|  6369 | Luis Suarez        |               90 |
|  6546 | Manuel Neuer       |               90 |
|  7855 | Neymar             |               90 |
| 11041 | Zlatan Ibrahimovic |               89 |
|   948 | Arjen Robben       |               89 |
|  9025 | Robert Lewandowski |               88 |
| 10172 | Thiago Silva       |               88 |
|  9659 | Sergio Aguero      |               88 |

Doing a preprocessing of the league, team, and match data, we are able to infer how many matches each team won, and so we can guess the winner of each league each season as the winner of most matches, this guess checks out against the ground truth.

|    |   league_id | season    |   team_api_id | team_long_name   |   wins |
|---:|------------:|:----------|--------------:|:-----------------|-------:|
|  1 |           1 | 2009/2010 |          8635 | RSC Anderlecht   |     22 |
| 77 |       21518 | 2014/2015 |          8633 | Real Madrid CF   |     30 |
| 23 |        7809 | 2008/2009 |          8721 | VfL Wolfsburg    |     21 |
|  3 |           1 | 2011/2012 |          8635 | RSC Anderlecht   |     20 |
| 76 |       21518 | 2013/2014 |          9906 | Atlético Madrid  |     28 |

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

### Data && motivation

The main focus of our project is to test  the **too-much-talent effect** in European football.  The data that we use contains a large set of match results and other meaningful information across several European leagues. We intend to use this data to build several measures of team performance. Data from the popular **FIFA** series of video games is also available and will allow us to measure individual player attributes which we can then aggregate to measure team talent.

The visualisation will be focused around comparing the designed metrics under user-specified filters (team, country, season ...). The main tool will be a large interactive scatter plot where the user will be able to contrast the theory. We intend to give readers a diverse selection of statistics so that they can obtain rich insights into this phenomenon.

We may also include other visualisation tools more centered on teams, leagues or players, that will please the readers’ curiosity but that are not as focused around the too-much-talent-effect. Some examples of this could be:

* team performance over time
* player talent over time
* compare leagues based on player talent



Depending on the source (all leagues don’t have the same amount of data collected), the data set can be very rich and contain other interesting information such as goal scorers, penalty cards and player substitution which are not always directly related to a team’s success but could lead to interesting visualisation as well.

### Website && ideas

We intend to have a main menu in which the user can select what kind of statistics he wants to test and visualise. This menu would contain several categories such as players, teams, leagues and the-too-much-talent effect.

The first three would be more “raw plots” without any interpretation behind, but for the fourth one, we would like include some interpretation clues to guide the reader and explain the main points made in the article.

As said, we intend to use an interactive scatter plot to make connections between team performance and talent in our too-much-talent category. However, for the other three, visualisation can very well take other forms. For detailed player data, we could use star plots. To visualise a team’s match ups, we could use a circular flow chart. In the league  category, we thought of maybe including a map so the user can select the country’s league he wants to visualise.

[Our website skeleton](https://com-480-data-visualization.github.io/data-visualization-project-2021-css/)


## Milestone 3 (4th June, 5pm)

**80% of the final grade**

[Video Link](https://drive.google.com/file/d/1yOq0sfBSkZPdTYThvAVMNxnHH4hE45ah/view?usp=sharing)

[Report](./data_viz_report.pdf)

## Late policy

- < 24h: 80% of the grade for the milestone
- < 48h: 70% of the grade for the milestone

