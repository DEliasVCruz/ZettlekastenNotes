# lang.psql.sort

You can sort and order your records based on a specified field values

## Synopsis

```sql
  SELECT [COMMAND] <column-name> FROM <table-name> ORDER BY <column-name> [ASC|DESC];
```

## Overview

You can **order and sort** your [selected](./c76a.md) **records based on a
field** and it's **values** with the `ORDER BY` command. By default it will
perform this ordering in ascending order (1 2 3)

You **can also** combine multiple columns when you sort, so as to **create
nested and sequential sorting of fields**

You **can not use** the `ORDER BY` command **on** a [view](./qxox.md) that was
**already constructed with** an `ORDER BY` clause. If you want' something like
that you will have to creaate a [new table](./rolo.md) based on the query **or**
just use **unite** each query **by surroding** each one **with** `()`

## Cookbook

### Sort records based on ascending or descending order

By **default** when **sorting by** a specified **column name**, it will be
sorted in **ascending order**

This will sort based on the values in the specified column in the order that is
specified

- **Ascending** order:

```sql
  SELECT <column-name> FROM <table-name> ORDER BY <column-name> [ASC];
```

- **Descending** order:

```sql
  SELECT <column-name> FROM <table-name> ORDER BY <column-name> DESC;
```

### Sort based on more than one column

When sorting you can **specify more than one field to sort by** and it will do so
**in** the **order** that you specify the fields

For example, **this will sort base on the column id and** then sort that sorted
[table](./rolo.md) based on **the name column**, all either on ascending or
descending order

```sql
  SELECT * FROM person ORDER BY id, name [ASC|DESC];
```

### Perform union on two separetly sorted queries

When performing [union](./c76a.md) on two separetly sorted queries SQL will
return an unsorted result, If you want to **preserve the sorting from each
query** then surround each query with `()`

You can even **add** an **extra** `GROUP By` **sorting** condition **for** the
**whole union** with this method

```sql
  (SELECT name, year FROM bands ORDER BY name)
  UNION all
  (SELECT name, year FROM albums ORDER BY name)
  ORDER BY year;
```
