# SQL Zoo

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
