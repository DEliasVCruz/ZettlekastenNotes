# cli.psql.csv

Export and import to csv data from SQL

## Synopsis

- With the client commands

```sql
  \copy (QUERY) TO '/path/to/file.csv' DELIMITER '<delimeter>' CSV [HEADER]
```

- In the SQL language

```sql
  COPY <table-name>[.<clumns>]
  FROM </path/to/file.csv>
  DELIMITER '<delimeter>' CSV [header];
```

### Overview

You can export and import csv data in and out of SQL.

## Cookbook

### Export csv data

You can **export** your sql table **to a csv** file either **with or without
the headers**

- Exporting from the SQL client

When you export with the `\copy` command in the `psql` client you can use
relative path and it will **download it into you local machine**

```sql
  \copy (SELECT * FROM person LEFT JOIN car ON car.id = person.car_id)
  TO '~/Documents/my_file.csv' CSV HEADER
```

- Exporting from the SQL server

When you export with the `COPY` command you do it **from the server** and you
need to **define the full path** to your local machine

```sql
  COPY (SELECT * FROM mytable) TO '~/Documents/my_file.csv' CSV HEADER;
```

### Import csv data

To import a csv file to a sql table you **first** need to **create a table**
that will **host the data**

```sql
  CREATE TABLE mytable (
      name VARCHAR,
      price MONEY
  )

  COPY mytable
  FROM '~/Documents/my_file.csv'
  DELIMITER ',' CSV HEADER;
```
