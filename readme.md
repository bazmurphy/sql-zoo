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
