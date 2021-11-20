# lang.psql.primary_keys

A value in our column which uniquely identifies a record in any table

## Overview

They are **unique identifiers** for records in your table. Most of the time,
integers are used as primary keys.

A primary key is **not restrained to a single columns**, you can compose a primary
key based on multiple columns

## Commands

- `PRIMARY KEY`: **Define** the field to be used as **primary key**

## Cookbook

### Define a field as a primary key

You can specify a field as a primary key by adding the `PRIMARY KEY` command
**at the end of the field definition** and this **acts as** a
[constrain](./q09z.md) for the field since it will **ensure that any value is
not repeated**.

It is **common practice** to use the `BIGSERIAL` data [type](./x350.md) for the
primary key, since this will **increase automatically with each record**

```sql
  CREATE TABLE person (
      id BIGSERIAL PRIMARY_KEY,
      first_name VARCHAR(50),
      last_name VARCHAR(50),
  );
```

### Define primary keys composed by multiple columns

You can add primary keys that are **based on more than one column**. But remember
that this will mean that **the composed value of those columns has to be unique**

```sql
  ALTER TABLE <table-name> ADD PRIMARY KEY (<column>[, <columns>]);
```

### Define foreign keys

You can **reference primary_keys** from other [tables](./rolo.md) as foreign keys

```sql
  create table person (
      id bigserial primary key,
      first_name varchar(50),
      <table-name>_id BIGINT REFERENCES <table_name> (<referenced_column_name>)
  );
```

### Deleting a foreign key record

**If** you are going to **delete a record** that is **referenced in another
table** as a foreign key, you **first** have to **delete that foreign key
reference** from the table
