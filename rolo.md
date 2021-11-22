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
- `ALTER TABLE`: **Make modifications** to you table after defining it
- `DELETE FROM`: **Delete records** from a table
- `AS TABLE`: **Create a table based on another** existing table

## Cookbook

### Create a new table

The basic table creation has the following structure

- **Specify** the **column name**
- **Specify** the [data type](./x350.md)
- **Specify** any conditional [constrains](./q09z.md)

```sql
  CREATE TABLE <table-name> (
      <column-name> <data-type> <constrains>
  );
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

### Change the schema of a table after creating it

If you want to **modify your table structure** after you have define it, but you
don't want to delete and recreate it again, you can use the `ALTER TABLE`
command

You can `ADD` or `DROP` parts of your schema

```sql
  ALTER TABLE <table-name> [ADD|DROP] <structure>;
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

### Insert records from another table

You can also **insert data from another table** into a new table **by specifing
a query** as the data to insert

```sql
  INSERT INTO mytable
  (SELECT * FROM person WHERE age < 25);
```

### Delete a record from a table

When wanting to **delete** a record you **should always use the primary key**
in the `WHERE` command. But you could delete by any field value with the
`DELETE` command

```sql
  DELETE FROM <table-name> WHERE <condition>;
```

### Define foreign keys

You can **reference** [primary_keys](./wbnd.md) from other tables as foreign keys

Since you are reference fields in other table, the **order in which you create
those tables matters!!!**, if you create a table that **references** another
**before** that table and the referenced **field is created**, it will **result
in an error**

```sql
  CREATE TABLE person (
      id BIGSERIAL PRIMARY KEY,
      first_name VARCHAR(50),
      <table-name>_id BIGINT REFERENCES <table_name> (<referenced_column_name>)
  );
```

### Reference a field in a different table

You can **reference a column from an specific table** with
`<table-name>.<column-name>`

```sql
  SELECT person.first_name, car.brand, car.price FROM person
  JOIN car ON person.car_id = car.id;
```

### Copy a table

You can **create new tables based on other tables** structures with the `AS TABLE`
command.

Furthermore, you **can specify if you don't want to copy the table data**
along (meaning you only want the structure)

- **Only** copy the **table structure**

```sql
  CREATE TABLE copy_table
  AS TABLE my_table
  WITH NO DATA;
```

- Copy with the structure and data

```sql
  CREATE TABLE copy_table
  AS TABLE my_table;
```
