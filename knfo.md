# lang.py.module.sql.pony

An easy to use an idiomatic data-mapper sql ORM

## Synopsis

```py
  from pony import orm
```

## Overview

You an use pony as data-mapper ORM, meaning is best when you want to keep the
structure of our database and the code separate

- It's simple to use and has a reasonable amount of features
- It does not have a database migration tool
- It does not play well with `pyright` linters

## Cookbook

### Connect to a database

It **supports**:

- [Sqlite](./wl6v.md)
- [PostgreSQL](./27nt.md)

A **provider has to be given** and each provider has it's **own set of
parameters** to pass

- The binding can happen after the schema definitoin

```py
  from pony import Database

  db = Database()
  db.bind(provider='sqlite', filename='my_data.db', create_db=True)
```

### Generate the database mappings

Once the [entities of your schema](./sa7b.md) have been define you can sync the mappings
with the `generate_mapping()` method of the `Database()` instance

- `create_tables`: Creates tables if they don't exist already

```py
  db.generate_mapping(create_tables=True)
```
