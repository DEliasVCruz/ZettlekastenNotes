# lang.psql.joins

Combine and display relational tables

## Synopsis

```sql
  SELECT <columns> FROM <table-name>
  [LEFT|RIGTH|CROSS] JOIN <table-name> [ON <table>.<foreing-key> = <table>.<primary-key>]
  [WHERE <conditions>];
```

## Overview

You can combine tables together based on common relationships between the
[tables](./rolo.md) with the `JOIN` command

### Commands

- `USING`: Specify the **field name to join on**

## Cookbook

### Inner join (Interjection)

It takes **whatever** is **common in both tables**. If you have a record in
table A that is also present in table B.

For example a **foreign key that is present in both tables**

```sql
  SELECT person.first_name, car.brand, car.price FROM person
  [INNER] JOIN car ON person.car_id = car.id;
```

### Left join (Left Bijection)

It includes **all the records of the left table** as well as the records from
the **right table that have an intersection**.

The **records** from the **left table** that **don't have an intersection are
still included** but does from the **right table** that **don't have an
intersection are not**

```sql
  SELECT * FROM person
  LEFT JOIN car ON person.car_id = car.id;
  WHERE car.* IS NULL
```

### Make joins when both fields are name the same

When the **primary key and foreign key** have the **same record name** in
**both table** you **can omit** the `<table>.<foreing-key> = <table>.<primary-key>`
expression, **and use** the `USING` command

```sql
  SELECT * FROM person
  JOIN car USING(car_id);
```

### Perform a cross join

You can **combine each row** of one table with each row of another **withouth**
an **specific join point**.

This will give you every possible combination of rows. For example if there are
5 rows in one table and 10 in the other then the join will give you 50 rows

```sql
  SELECT b.base_id, s.suply_id, s.name
  FROM base AS b
  CROSS JOIN supply AS s;
```
