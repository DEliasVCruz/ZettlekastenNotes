# lang.psql.table

Perform SQL operations on tables with the TABLE keyword

## Synopsis

```sql
  [COMMAND] TABLE <table-name> (
      <operations>
  );
```

## Overview

### Commands

- `CREATE TABLE`: Start a **new table** and **define** it's **structure**
- `INSERT INTO`: **Specify** what **columns** you are going to **enter values to**

## Cookbook

### Create a new table

The basic table creation has the following structure

- **Specify** the **column name**
- **Specify** the [data type](./x350.md)
- **Specify** any conditional [constrains](./q09z.md)

```sql
  CREATE TABLE <table-name> (
      <column-name> <data-type> <constrains>
  )
```

A **table** should always **have a noun as a name**, in the following example
we create the **person table**

```sql
  CREATE TABLE person (
      id int,
      first_name VARCHAR(50),
      last_name VARCHAR(50),
      gender VARCHAR(6),
      date_of_birth DATE,
  );
```

### Delete a table

You can use the `DROP` command to delete a table

```sql
  DROP TABLE <table-name>;
```

### Insert records into tables

After you create your table structure you'll have to start **populating** your
**table with** actual **data**

To add data you can **use** the `INSERT INTO` command to **define what columns**
of your table you are going to **insert values into**

After you've define the columns, use the `VALUES` command to **define the values
to be inserted**. It has to be in the **same order that the columns** where
previously defined

Inside the `VALUES` command:

- Strings are defined with quotes
- Numbers are define without quotes
- Dates are define with quotes and specifying the `DATE` type

```sql
  INSERT INTO <table-name> (
      <string-type-column>
      <int-type-column>
      <date-type-columns>
  )
  VALUES ('<Value-1>', <Value-2>, DATE '<date-format>');
```
