# Game Analysis

## Project overview

This data analysis project aims to provide insights about players and their performance in each level of games played. 

### Data sources

Games data : The primary dataset used in the analysis are 'Player details' and 'Level details' which contains a brief description of each players and the levels of games played.

### Tools

SQL ( This was used for querying and extracting data from the tables ).

### Data Preparation
In the initial data preparation stage, the tasks were performed
- Data loading and inspection.

### Exploratory data analysis

EDA involved exploring the games data to answer questions like :
1. Find level and it's corresponding level code wise sum of lives earned excluding level 0.
2. Find the top 3 score based on each dev_id and rank them and rank them in increasing order using row_number.
3. Find the first login datetime for each device id.
4. Find the device id that is first logged in (based on start_date) for each player.

### Data Analysis

``` sql
    with  cte_game  as (
       select [dev_id],[score], [difficulty],
       rank() over (partition by [difficulty] order by [score] as top_5
       from [game_analysis].[dbo].[levels_details2] lv
       join [game_analysis].[dbo].[player_details] pd
       on lv.p_id = pd.p_id )
   select dev_id,score, difficulty
   from cte_game
   where top_5  <= 5
```






