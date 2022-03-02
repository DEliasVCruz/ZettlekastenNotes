# lang.py.module.sql.sqlite

Work with an sqlite database from within Python

## Synopsis

```py
  import sqlite3 as sqlite
```

## Overview

The `sqlite3` module is a **builtin** module of the `Python` standard library
and as such you **don't need to setup a database before using it**

- The basic object is a `connection` object, that **can be used to execute
  queries**

## Cookbook

### Create or connect to an sqlite database

You can use the `connect()` function to **connect** to a sqlite database
**given** a [path](./bwao.md)

**If no database** is **found** at that path, a **new database will be
created** at the specified location

```py
  import sqlite3
  from sqlite3 import Error

  try:
      connection = sqlite3.connect(./path/to/sql/database.db)
      print("Connection successful!")
  except Error as e:
      print(f"The error '{e}' ocurred")
```

### Execute arbitray commands and queries

To execute arbitray commands and queries you'll need to create a `cursor()`
object and use it's `execute()` method

- This **accepts** any **arbitray valid** `sqlite` query or **expression** as a [string](./4t3v.md)

- For creating tables and inserting records you need to:
  - **After executing the query** you have to commit your changes with `commit()`

```py
  query = """
  CREATE TABLE IF NOT EXISTS users (
    id INTEGER PRIMARY KEY AUTOINCREMENT,
    name TEXT NOT NULL,
    age INTEGER,
    gender TEXT,
  )
  """

  def execute_query(connection, query):
      cursor = connection.cursor()
      try:
          cursor.execute(query)
          connection.commit()
          print("Query executed successfully")
      except Error as e:
          print(f"The error '{e}' occurred")

  execute_query(connection, query)
```

### Extract queried data

When you perform a `SELECT` query, you need to invoke the `fetchall()` method
that will return a [list](./7cxo.md) where each element is a [tuple](./hsr4.md)
that maps to it's corresponing row

```py
def execute_read_query(connection, query):
    cursor = connection.cursor()
    result = None
    try:
        cursor.execute(query)
        result = cursor.fetchall()
        return result
    except Error as e:
        print(f"The error '{e}' occurred")


  select_users = "SELECT * from users"
  users = execute_read_query(connection, select_users)

  for user in users:
      print(user)
```

### Get the column names of your select queries

When executing a `slect` query, the **result dosen't capture the column
names**. For that you can use the `.description` atribute that gives usefull
**information about each column** in your result

- You can find the **column name** in the **first element of each description**

```py
  cursor = connection.cursor()
  cursor.execute(query)
  cursor.fetchall()

  column_names = [description[0] for description in cursor.description]
  print(column_names)

# Out:
  ['post', 'comment', 'name']
```
