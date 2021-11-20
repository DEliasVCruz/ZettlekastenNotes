# cli.psql

The command line PostgreSQL client

## Synopsis

```sh
  psql [options] [data-base [user]]
```

## Overview

The `psql` shell can be accessed either by flag options or interactively

## Options

- `-h`: Server **host** or socket directory
- `-p`: Server **port** to connect
- `-U`: **Username** to execute with
- `-l`: **List** all databases
- `-f`: **Execute** orders from **file**

### Interactive Commands

This are the commands you can use **inside interactive mode**

- `\c`: **Connect to** an specified **database**
- `\d`: **List tables** in your database
- `\i`: **Execute commands** from specified **file**
- `\x`: View **records in vertical** mode
- `\copy`:

## Cookbook

### Connect to a database

You **can connect** to a database **and specify** which **server host**,
**user** and **port** the database is associated to. By **default** it will
**use** the **localhost**, **main user** and **port 5432**

```sh
  psql -h <host-name> -p <port-number> -U <user-name> <database-name>
```

### List all the tables in your data-base

You can use `\d` (describe) to **list all** the created tables. If you want to
**see the details** of the keys on a **specific table** you can **pass the
name** of the table

```language
  \d [<table-name>]
```
