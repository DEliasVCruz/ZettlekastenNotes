# lang.psql.index

Lower query times by indexing commonly queried columns

## Synopsis

```sql
  CREATE INDEX [<index-name>]
  ON <table-name> (<column-names>)
  ANALIZE
```

## Overview

You **can index multiple table** columns so that **queering** based on this
columns **happens faster**

They are a **trade-off between speed** of querying **and extra storage space**
for the created queries. Also, you'll have to **update** all the relevant
**indices when updating tables**

## Cookbook

### Index based on multiple table columns

You can **build compound indexes** that will **work when** the compounded
columns are **queried together**

When creating multi columns indices **the order matters**, think of it **as
sorting orders**

```sql
  CREATE INDEX person_first_name_last_name_idx
  ON person (last_name, first_name);
  ANALIZE
```

### Display the querying strategy

You can use the `EXPLAIN ANALIZE` command to **display** the **query strategy**
done with the [SELECT](./c76a.md) command

```sql
  EXPLAIN ANALIZE
  <query>
```
