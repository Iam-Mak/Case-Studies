# Case Study 4 : When Was the Golden Age of Video Games?

<p align="center"> <img width="387" alt="image"  src="https://user-images.githubusercontent.com/92245436/192102065-97943db5-aebe-41c0-9396-267564ddd9f1.png"> </p>


Video games are big business: the global gaming market is projected to be worth more than **$300 billion** by 2027 according to [Mordor Intelligence](https://www.mordorintelligence.com/industry-reports/global-gaming-market). With so much money at stake, the major game publishers are hugely incentivized to create the next big hit. But are games getting better, or has the golden age of video games already passed?

In this project, I'll explore the top 400 best-selling video games created between 1977 and 2020. I'll compare a dataset on game sales with critic and user reviews to determine whether or not video games have improved as the gaming market has grown.
 <br>


### Objective : Exploration of the top 400 best-selling video games created between 1977 and 2020.

##  Ask 
- What are the best-selling video games.
- What are critics' best favorite years for games.
- Find years, where both players and critics loved the games.
- Find Sales in the best video game years wise.

##  Prepare 
This database contains two tables. I've limited each table to 400 rows for this project, but you can find the complete dataset with over 13,000 games on [Kaggle](https://www.kaggle.com/datasets/holmjason2/videogamedata).

### Table 1
`game_sales`

|column	|type	|meaning|
|------|------|--------|
|game|	varchar|	Name of the video game|
|platform|	varchar|	Gaming platform|
|publisher	|varchar|	Game publisher|
|developer|	varchar|	Game developer|
|games_sold	|float	|Number of copies sold (millions)|
|year|	int|	Release year|

### Table 2
`reviews`
|column	|type|	meaning|
|-------|-----|--------|
|game|	varchar	|Name of the video game|
|critic_score	|float|	Critic score according to Metacritic|
|user_score	|float	|User score according to Metacritic|


#### Is Data ROCCC?
A good data source is **ROCCC** which stands for **Reliable, Original, Comprehensive, Current,** and **Cited**.

- **Reliable -** *High* - Data is reliable 
- **Original -** *High* - Dta is Original
- **Comprehensive** - *High* - We have all needed parameters 
- **Current** - *High* - Data is up to date
- **Cited** - *High* - Source is verified


## Process & Analyze
Let's begin by looking at some of the top selling video games of all time!

`Q` Let's find the ten best-selling video games in `game_sales`.

```
SELECT * FROM game_sales
ORDER BY games_sold DESC
LIMIT 3
```
`Result:`
|game	|platform	|publisher|	developer|	games_sold	|year|
|-----|--------|-----------|---------|---------------|----|
|Wii Sports for Wii	|Wii	|Nintendo|	Nintendo EAD|	82.90|	2006|
|Super Mario Bros. for |NES	|NES	Nintendo	|Nintendo EAD	|40.24|	1985|
|Counter-Strike: Global Offensive for PC|	PC	|Valve	|Valve Corporation	|40.00	|2012|

- the best-selling video games were released between 1985 to 2017. we'll have to use data from the reviews table to gain more insight on the best years for video games.
<hr/>


`Q` Let's determine how many games in the `game_sales` table are missing both a `user_score` and a `critic_score`.

```
SELECT COUNT(g.game)
FROM game_sales as g
LEFT JOIN reviews as r
ON g.game = r.game
WHERE r.critic_score IS NULL 
AND r.user_score IS NULL
```
`Result:`

|count|
|-----|
|31|

- It looks like a little less than ten percent of the games on the `game_sales` table don't have any reviews data. That's a small enough percentage that we can continue our exploration.

<hr/>

`Q` Find the years with the highest average critic_score.
```
SELECT g.year, ROUND(AVG(critic_score),2) as avg_critic_score
FROM game_sales as g
LEFT JOIN reviews as r
ON g.game = r.game
GROUP BY g.year
ORDER BY avg_critic_score DESC
LIMIT 10
```
`Result:`
|year	|avg_critic_score|
|-----|--------------|
|1990|	9.80|
|1992|	9.67|
|1998|	9.32|
|2020|	9.20|
|1993|	9.10|
|1995|	9.07|
|2004|	9.03|
|1982|	9.00|
|2002	|8.99|
|1999	|8.93|

- The range of great years according to critic reviews goes from 1982 until 2020.
- Some of those avg_critic_score values look like suspiciously round numbers for averages. The value for 1982 looks especially fishy. Maybe there weren't a lot of video games in our dataset that were released in certain years.

<hr/>

`Q` Find game critics' ten favorite years, this time with the stipulation that a year must have more than four games released in order to be considered.

```
SELECT g.year, 
ROUND(AVG(critic_score),2) AS avg_critic_score,
COUNT (g.game) AS num_games
FROM game_sales AS g
INNER JOIN reviews AS r
ON g.game = r.game
GROUP BY year
HAVING COUNT(g.game) > 4
ORDER BY avg_critic_score DESC
LIMIT 10;
```
`Result:`
|year	|avg_critic_score|	num_games |
|-----|----------------|------------|
|1998|	9.32|	10|
|2004|	9.03	|11|
|2002|	8.99	|9|
|1999	|8.93|	11|
|2001	|8.82	|13|
|2011	|8.76|	26|
|2016	|8.67	|13|
|2013	|8.66	|18|
|2008	|8.63	|20|
|2012|	8.62|	12|

- The num_games column convinces us that our new list of the critics' top games reflects years that had quite a few well-reviewed games rather than just one or two hits.

<hr/>

`Q` Use set theory to find the years that were on our first critics' favorite list but not the second.
`top_critic_years`

|column|	type|	meaning|
|-----|-------|--------|
|year|	int	|Year of video game release|
|avg_critic_score	|float|	Average of all critic scores for games released in that year|


`top_critic_years_more_than_four_games`

|column	|type	|meaning|
|-------|-----|--------|
|year	|int	|Year of video game release|
|num_games|	int|	Count of the number of video games released in that year|
|avg_critic_score|	float|	Average of all critic scores for games released in that year|

```
SELECT year, avg_critic_score
FROM top_critic_years
EXCEPT
SELECT year, avg_critic_score
FROM top_critic_years_more_than_four_games
ORDER BY avg_critic_score DESC;
```
`Result:`
|year|	avg_critic_score|
|-----|------------------|
|1990|	9.80|
|1992	|9.67|
|2020|	9.20|
|1993|	9.10|
|1995|	9.07|
|1982|	9.00|

- It looks like the early 1990s might merit consideration as the golden age of video games based on critic_score alone, but we'd need to gather more games and reviews data to do further analysis.

<hr/>

`Q` Find years with ten highest avg_user_score values.
```
SELECT g.year, 
ROUND(AVG(user_score),2) AS avg_user_score,
COUNT(g.game) AS num_games
FROM game_sales AS g
INNER JOIN reviews AS r
ON g.game = r.game
GROUP BY year
HAVING COUNT(year) > 4
ORDER BY avg_user_score DESC
LIMIT 10;
```
`Result:`
|year	|avg_user_score|	num_games|
|-----|---------------|----------|
|1997|	9.50	|8|
|1998|	9.40	|10|
|2010|	9.24	|23|
|2009|	9.18	|20|
|2008|	9.03	|20|
|1996|	9.00	|5|
|2005|	8.95	|13|
|2006|	8.95	|16|
|2000|	8.80|	8|
|1999|	8.80	|11|

<hr/>

`Q` Create a list of years that appear on both the top_critic_years_more_than_four_games table and the top_user_years_more_than_four_games table.
`top_critic_years_more_than_four_games`

|column|	type|	meaning|
|------|------|--------|
|year	|int	|Year of video game release|
|num_games	|int	|Count of the number of video games released in that year|
|avg_critic_score|	float|	Average of all critic scores for games released in that year|

`top_user_years_more_than_four_games`
|column	|type	|meaning|
|-------|-----|-------|
year	|int	|Year of video game release|
|num_games|	int	|Count of the number of video games released in that year|
|avg_user_score	|float	|Average of all user scores for games released in that year|

```
SELECT year 
FROM top_critic_years_more_than_four_games
INNER JOIN top_user_years_more_than_four_games
USING (year);
`Result:`
```
|year|
|----|
|1998|
|2002|
|2008|

- We've got three years that both users and critics agreed were in the top ten.

<hr/>

`Q` Add a column showing total games_sold in each year to the table you created in the previous task.

```
SELECT year,
SUM(games_sold) AS total_games_sold
FROM game_sales
WHERE year IN (SELECT year 
FROM top_critic_years_more_than_four_games
INNER JOIN top_user_years_more_than_four_games
USING (year))
GROUP BY year
ORDER BY total_games_sold DESC;
```
`Result:`
|year	|total_games_sold|
|-----|--------------|
|2008	|175.07|
|1998	|101.52|
|2002	|58.67|
<hr/>

## Findings
- Best Years for games according to critics score are 1990,1992 and 1998
- Best years for games according to both critics and players are 2008,1998 and 2002.
- Total Games sold in best years are  175.07, 101.52, 58.67 millions.
