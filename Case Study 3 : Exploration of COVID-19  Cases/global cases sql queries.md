###  Total coronavirus cases continent wise
```
SELECT
  continent,
  SUM(total_deaths) total_case
FROM
  `covid-19-341809.global_covid_19.covid_cases`
WHERE
  continent IS NOT NULL
GROUP BY
  continent
HAVING
  SUM(total_deaths) IS NOT NULL
ORDER BY
  total_case DESC
```
![image](https://user-images.githubusercontent.com/92245436/154839261-626c36f3-5dec-4d3a-9bbc-639b1ca8f005.png)

### Countries with highest infection count

```
SELECT
  location,
  population,
  MAX(total_cases) AS highest_infection_count,
FROM
  `covid-19-341809.global_covid_19.covid_cases`
WHERE
  continent IS NOT NULL
GROUP BY
  Location,
  Population
ORDER BY
  highest_infection_count DESC
LIMIT
  5
```
![image](https://user-images.githubusercontent.com/92245436/154840401-bbc2263c-14c6-4eef-b7a5-24261abe0dfa.png)


### Countries with highest percentage of population infected
```
SELECT
  location,
  population,
  MAX(total_cases) AS highest_infection_count,
  MAX((total_cases/population))*100 AS percent_population_infected
FROM
  `covid-19-341809.global_covid_19.covid_cases`
GROUP BY
  Location,
  Population
ORDER BY
  percent_population_infected DESC
LIMIT
  5
```
![image](https://user-images.githubusercontent.com/92245436/154840237-21d5fbec-78f0-420f-8514-9915aef15fe8.png)

### Countries with highest total death count

```
SELECT
  location,
  MAX(CAST(Total_deaths AS int)) AS total_death_count
FROM
  `covid-19-341809.global_covid_19.covid_cases`
WHERE
  continent IS NOT NULL
GROUP BY
  Location
ORDER BY
  total_death_count DESC
LIMIT
  5
```
![image](https://user-images.githubusercontent.com/92245436/154840520-c536f8ca-c7fb-4136-99c1-0aaf7205bc24.png)

### Continent wise total death count
```
SELECT
  continent,
  MAX(CAST(Total_deaths AS int)) AS total_death_count
FROM
  `covid-19-341809.global_covid_19.covid_cases`
WHERE
  continent IS NOT NULL
GROUP BY
  continent
ORDER BY
  total_death_count DESC
LIMIT
  5
```
![image](https://user-images.githubusercontent.com/92245436/154840666-eb1ad418-a84f-473f-977c-a8d0b3ccbe75.png)

### Infection fatality ratio
![image](https://user-images.githubusercontent.com/92245436/155381411-b0ac3aa7-8c83-4ce3-86b7-9a2f8c0e0d8f.png)

```
SELECT
  date,
  SUM(new_cases) AS total_cases,
  SUM(CAST(new_deaths AS int)) AS total_deaths,
  SUM(CAST(new_deaths AS int))/SUM(New_Cases)*100 AS death_percentage
FROM
  `covid-19-341809.global_covid_19.covid_cases`
WHERE
  continent IS NOT NULL
GROUP BY
  date
HAVING
  death_percentage IS NOT NULL
ORDER BY
  1,
  2
```
![image](https://user-images.githubusercontent.com/92245436/155293997-288cd4a7-7866-4397-9832-7a1c76c74bcf.png)

### Start date for covid vaccine 
```
SELECT
  dea.location,
  dea.date,
  dea.population,
  vac.new_vaccinations,
  SUM(new_vaccinations) OVER (PARTITION BY dea.Location ORDER BY dea.location, dea.Date) AS rolling_people_vaccinated
FROM
  `covid-19-341809.global_covid_19.covid_cases` dea
JOIN
  `covid-19-341809.global_covid_19.covid_vaccination` vac
ON
  dea.location = vac.location
  AND dea.date = vac.date
WHERE
  dea.continent IS NOT NULL
  AND vac.new_vaccinations IS NOT NULL
  AND vac.new_vaccinations > 0
ORDER BY
  2
```
![image](https://user-images.githubusercontent.com/92245436/155462107-4111af96-778c-44bf-b0dc-2a1f7f602a45.png)
