# cli.psql.database

set of commands it offers to create and manage databases

## Overview

PostgreSQL works with a **client - server** model, meaning that a SQL **server has
to be** instantiated and **active every time** you are going to **work with a database**

Therefore, `psql` is the **default** PostgreSQL **client**. And it enables you
to **type queries interactively**

## Cookbook

### Create a new database

You can **create any number of databases**, but their names must:

- Have an alphabetic first character
- Limited to 63 bytes in length

You can use the [createdb](./4v7t.md) command that `psql` provides to create a
database from the cmdline

```sh
  createdb <database-name>
```

Alternatevely you can use the [sql syntax](./vv3j.md) to create a database

```sql
  CREATE DATABASE <database-name>
```

### Delete a database

**If** you are the **owner** of a database **and don't** want to **use it
anymore**. You can use the [dropdb](./har9.md) command that `psql` provides to
create a database

```sh
  dropdb <database-name>
```

Alternatevely you can **use the sql syntax** to create a database

```sql
  DROP DATABASE <database-name>
```
