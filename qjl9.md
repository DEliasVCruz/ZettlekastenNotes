# lang.psql.joins

Combine and display relational tables

## Synopsis

```sql
  SELECT <columns> FROM <table-name>
  [LEFT|RIGTH] JOIN <table-name> ON <table>.<foreing-key> = <table>.<primary-key>;
  [WHERE <conditions>]
```

## Overview

You can combine tables together based on common relationships between the
tables with the `JOIN` command

## Cookbook

### Inner join (Interjection)

It takes **whatever** is **common in both tables**. If you have a record in
table A that is also present in table B.

For example a **foreing key that is present in both tables**

```sql
  SELECT person.first_name, car.brand, car.price FROM person
  JOIN car ON person.car_id = car.id;
```

### Left join (Left Bijection)

It includes **all the records of the left table** as well as the records from
the **rigth table that have an intersection**.

The **records** from the **left table** that **don't have an intersection are
still included** but does from the **right table** that **don't have an
intersection are not**

```sql
  SELECT * FROM person
  LEFT JOIN car ON person.car_id = car.id;
  WHERE car.* IS NULL
```
