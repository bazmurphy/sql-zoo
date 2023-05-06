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

# 2. SELECT from world

## 2.1

```sql
SELECT name, continent, population FROM world;
```

## 2.2

```sql
SELECT name FROM world
WHERE population >= 200000000;
```

## 2.3

```sql
SELECT name, gdp/population AS per_capita_gdp
FROM world
WHERE population >= 200000000;
```

## 2.4

```sql
SELECT name, population / 1000000
FROM world
WHERE continent='South America';

```

## 2.5

```sql
SELECT name, population
FROM world
WHERE name IN ('France', 'Germany', 'Italy');
```

## 2.6

```sql
SELECT name
FROM world
WHERE name LIKE 'United%';
```

## 2.7

```sql
SELECT name, population, area
FROM world
WHERE (area > 3000000 OR population > 250000000);
```

## 2.8

```sql
SELECT name, population, area
FROM world
WHERE (area > 3000000) != (population > 250000000);

```

## 2.9

```sql
SELECT name, ROUND(population / 1000000, 2), ROUND(gdp / 1000000000, 2)
FROM world
WHERE continent='South America'
```

## 2.10

```sql
SELECT name, ROUND(gdp/population, -3)
FROM world
WHERE gdp >= 1000000000000;
```

## 2.11

```sql
SELECT name, capital
FROM world
WHERE LENGTH(name) = LENGTH(capital);
```

## 2.12

```sql
SELECT name, capital
FROM world
WHERE LEFT(name, 1) = LEFT(capital, 1) AND name != capital;
```

## 2.13

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

# 3. SELECT from nobel

## 3.1

```sql
SELECT yr, subject, winner
FROM nobel
WHERE yr = 1950;
```

## 3.2

```sql
SELECT winner
FROM nobel
WHERE yr = 1962
AND subject = 'literature';
```

## 3.3

```sql
SELECT nobel.yr, subject
FROM nobel
WHERE winner = 'Albert Einstein';
```

## 3.4

```sql
SELECT winner
FROM nobel
WHERE yr >= 2000
AND subject = 'peace';
```

## 3.5

```sql
SELECT yr, subject, winner
FROM nobel
Where (yr >= 1980 AND yr <= 1989)
AND subject = 'literature';
```

## 3.6

```sql
SELECT yr, subject, winner
FROM nobel
WHERE winner IN ('Theodore Roosevelt','Jimmy Carter', 'Barack Obama');
```

## 3.7

```sql
SELECT winner
FROM nobel
WHERE winner LIKE 'John%';
```

## 3.8

```sql
SELECT yr, subject, winner
FROM nobel
WHERE (subject = 'physics' AND yr = 1980)
OR (subject = 'chemistry' AND yr = 1984);
```

## 3.9

```sql
SELECT yr, subject, winner
FROM nobel
WHERE yr = 1980
AND subject NOT IN ('chemistry', 'medicine');
```

## 3.10

```sql
SELECT yr, subject, winner
FROM nobel
WHERE (yr < 1910 AND subject = 'Medicine')
OR (yr >= 2004 AND subject = 'Literature');
```

## 3.11

```sql
SELECT yr, subject, winner
FROM nobel
WHERE winner LIKE 'Peter Gr%nberg';
```

## 3.12

```sql
SELECT yr, subject, winner
FROM nobel
WHERE winner LIKE 'Eugene O''Neill';
```

## 3.13

```sql
SELECT winner, yr, subject
FROM nobel
WHERE winner LIKE 'Sir%'
ORDER BY yr DESC, winner ASC;
```

## 3.14

```sql
SELECT winner, subject
FROM nobel
WHERE yr = 1984
ORDER BY subject IN ('physics','chemistry'), subject ASC, winner ASC;
```

# 4. SELECT within SELECT

## 4.1

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
