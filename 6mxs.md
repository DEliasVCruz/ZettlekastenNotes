# lang.psql.aggregation

You can aggregate repeated records of a field

## Synopsis

```sql
  SELECT <column-name> FROM <table-names>
  GROUP BY <column-name> HAVING <condition>;
```

## Overview

You can use the `GROUP BY` command to aggregate repeated columns and display
them as a resuming.

It is most commonly used with other aggregate [functions](./x41v.md) like `COUNT()`

### Commands

- `HAVING`: Perform **additional filtering after the aggregation** and summary

## Cookbook

### Add additional filtering after the aggregation

You can perform some **extra filtering** after the aggregation with the `HAVING`
command, this command is **different from** `WHERE` because it **does it's**
[filtering](./m2xg.md) **after the aggregation**

It also **must come before** the `ORDER BY` command

```sql
  SELECT country_of_birth, COUNT(*) FROM person
  GROUP BY country_of_birth HAVING COUNT(*) > 5
  ORDER BY country_of_birth;
```

### Find the minimum value for each record group

If you want to know what are the **minimum values for each aggregation field**

```sql
  SELECT brand, model, MIN(prince) FROM car
  GROUP BY brand, model;
```
