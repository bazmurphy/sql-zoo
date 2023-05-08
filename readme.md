# SQL Zoo

https://sqlzoo.net/

## 1. SELECT basics

### 1.1

```sql
SELECT population FROM world
  WHERE name = 'Germany'
```

### 1.2

```sql
SELECT name, population FROM world
  WHERE name IN ('Sweden', 'Norway', 'Denmark');
```

### 1.3

```sql
SELECT name, area FROM world
  WHERE area BETWEEN 250000 AND 300000
```

## 2. SELECT from world

### 2.1

```sql
SELECT name, continent, population FROM world;
```

### 2.2

```sql
SELECT name FROM world
WHERE population >= 200000000;
```

### 2.3

```sql
SELECT name, gdp/population AS per_capita_gdp
FROM world
WHERE population >= 200000000;
```

### 2.4

```sql
SELECT name, population / 1000000
FROM world
WHERE continent='South America';

```

### 2.5

```sql
SELECT name, population
FROM world
WHERE name IN ('France', 'Germany', 'Italy');
```

### 2.6

```sql
SELECT name
FROM world
WHERE name LIKE 'United%';
```

### 2.7

```sql
SELECT name, population, area
FROM world
WHERE (area > 3000000 OR population > 250000000);
```

### 2.8

```sql
SELECT name, population, area
FROM world
WHERE (area > 3000000) != (population > 250000000);

```

### 2.9

```sql
SELECT name, ROUND(population / 1000000, 2), ROUND(gdp / 1000000000, 2)
FROM world
WHERE continent='South America'
```

### 2.10

```sql
SELECT name, ROUND(gdp/population, -3)
FROM world
WHERE gdp >= 1000000000000;
```

### 2.11

```sql
SELECT name, capital
FROM world
WHERE LENGTH(name) = LENGTH(capital);
```

### 2.12

```sql
SELECT name, capital
FROM world
WHERE LEFT(name, 1) = LEFT(capital, 1) AND name != capital;
```

### 2.13

```sql
SELECT name
FROM world
WHERE name LIKE '%a%'
AND name LIKE '%e%'
AND name LIKE '%i%'
AND name LIKE '%o%'
AND name LIKE '%u%'
AND name NOT LIKE '% %';
```

## 3. SELECT from nobel

### 3.1

```sql
SELECT yr, subject, winner
FROM nobel
WHERE yr = 1950;
```

### 3.2

```sql
SELECT winner
FROM nobel
WHERE yr = 1962
AND subject = 'literature';
```

### 3.3

```sql
SELECT nobel.yr, subject
FROM nobel
WHERE winner = 'Albert Einstein';
```

### 3.4

```sql
SELECT winner
FROM nobel
WHERE yr >= 2000
AND subject = 'peace';
```

### 3.5

```sql
SELECT yr, subject, winner
FROM nobel
Where (yr >= 1980 AND yr <= 1989)
AND subject = 'literature';
```

### 3.6

```sql
SELECT yr, subject, winner
FROM nobel
WHERE winner IN ('Theodore Roosevelt','Jimmy Carter', 'Barack Obama');
```

### 3.7

```sql
SELECT winner
FROM nobel
WHERE winner LIKE 'John%';
```

### 3.8

```sql
SELECT yr, subject, winner
FROM nobel
WHERE (subject = 'physics' AND yr = 1980)
OR (subject = 'chemistry' AND yr = 1984);
```

### 3.9

```sql
SELECT yr, subject, winner
FROM nobel
WHERE yr = 1980
AND subject NOT IN ('chemistry', 'medicine');
```

### 3.10

```sql
SELECT yr, subject, winner
FROM nobel
WHERE (yr < 1910 AND subject = 'Medicine')
OR (yr >= 2004 AND subject = 'Literature');
```

### 3.11

```sql
SELECT yr, subject, winner
FROM nobel
WHERE winner LIKE 'Peter Gr%nberg';
```

### 3.12

```sql
SELECT yr, subject, winner
FROM nobel
WHERE winner LIKE 'Eugene O''Neill';
```

### 3.13

```sql
SELECT winner, yr, subject
FROM nobel
WHERE winner LIKE 'Sir%'
ORDER BY yr DESC, winner ASC;
```

### 3.14

```sql
SELECT winner, subject
FROM nobel
WHERE yr = 1984
ORDER BY subject IN ('physics','chemistry'), subject ASC, winner ASC;
```

## 4. SELECT within SELECT

### 4.1

```sql
SELECT name
FROM world
WHERE population >
(SELECT population
FROM world
WHERE name='Russia');
```

### 4.2

```sql
SELECT name
FROM world
WHERE continent = 'Europe'
AND gdp / population >
(SELECT gdp / population
FROM world
WHERE name = 'United Kingdom');
```

### 4.3

```sql
SELECT name, continent
FROM world
WHERE continent IN
(SELECT continent
FROM world
WHERE name IN ('Argentina', 'Australia'));
```

### 4.4

```sql
SELECT name, population
FROM world
WHERE population >
(SELECT population
FROM world
WHERE name = 'United Kingdom')
AND population <
(SELECT population
FROM world
WHERE name = 'Germany');
```

### 4.5

```sql
.
```

### 4.6

```sql
.
```

### 4.7

```sql
.
```

### 4.8

```sql
.
```

### 4.9

```sql
.
```

### 4.10

```sql
.
```

## 5. SUM and COUNT

### 5.1

```sql
SELECT SUM(population)
FROM world;
```

### 5.2

```sql
SELECT DISTINCT continent
FROM world;
```

### 5.3

```sql
SELECT SUM(gdp)
FROM world
WHERE continent = 'Africa';
```

### 5.4

```sql
SELECT COUNT(area)
FROM world
WHERE area >= 1000000;
```

### 5.5

```sql
SELECT SUM(population)
FROM world
WHERE name IN ('Estonia', 'Latvia', 'Lithuania');
```

### 5.6

```sql
SELECT continent, COUNT(name)
FROM world
GROUP BY continent;
```

### 5.7

```sql
SELECT continent, COUNT(name)
FROM world
WHERE population >= 10000000
GROUP BY continent;
```

### 5.8

```sql
SELECT continent
FROM world
GROUP BY continent
HAVING SUM(population) > 100000000;
```

## 6. JOIN

### 6.1

```sql
SELECT matchid, player
FROM goal
WHERE teamid = 'GER';
```

### 6.2

```sql
SELECT id,stadium,team1,team2
FROM game
WHERE id = 1012;
```

### 6.3

```sql
SELECT player,teamid, stadium, mdate
FROM game
JOIN goal
ON game.id = goal.matchid
WHERE teamid = 'GER';
```

### 6.4

```sql
SELECT team1, team2, player
FROM game
JOIN goal
ON game.id = goal.matchid
WHERE player LIKE 'Mario%';
```

### 6.5

```sql
SELECT player, teamid, coach, gtime
FROM goal
JOIN eteam
ON goal.teamid = eteam.id
WHERE gtime <= 10;
```

### 6.6

```sql
SELECT mdate, teamname
FROM game
JOIN eteam
ON game.team1 = eteam.id
WHERE coach = 'Fernando Santos';
```

### 6.7

```sql
SELECT player
FROM game
JOIN goal
ON game.id = goal.matchid
WHERE stadium = 'National Stadium, Warsaw';
```

### 6.8

```sql
SELECT DISTINCT player
FROM game
JOIN goal
ON game.id = goal.matchid
WHERE (team1 = 'GER' OR team2 = 'GER')
AND teamid != 'GER';
```

### 6.9

```sql
SELECT teamname, COUNT(teamname)
FROM eteam
JOIN goal
ON eteam.id = goal.teamid
GROUP BY teamname;
```

### 6.10

```sql
SELECT stadium, COUNT(matchid)
FROM game
JOIN goal
ON game.id = goal.matchid
GROUP BY stadium;
```

### 6.11

```sql
SELECT id, mdate, count(id)
FROM game
JOIN goal
ON game.id = goal.matchid
WHERE (team1 = 'POL' OR team2 = 'POL')
GROUP BY id, mdate;
```

### 6.12

```sql
SELECT matchid, mdate, COUNT(matchid)
FROM game
JOIN goal
ON game.id = goal.matchid
WHERE teamid = 'GER'
GROUP BY matchid, mdate;
```

### 6.13

```sql
SELECT
  mdate,
  team1,
  SUM(CASE WHEN teamid = team1 THEN 1 ELSE 0 END) AS score1,
  team2,
  SUM(CASE WHEN teamid = team2 THEN 1 ELSE 0 END) AS score2
FROM game
LEFT JOIN goal
ON game.id = goal.matchid
GROUP BY mdate, matchid, team1, team2;
```
