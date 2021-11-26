# lang.psql.views

Limited queriable versions of other tables

## Synopsis

```sql
  CREATE VIEW <view-name> [(column names)] AS
  <QUERY>;
```

## Overview

You can create limited version of existing tables. In practice this is like
**saving a query reulst into another table**. You **can** then share and **perform
queries** on this new table

Vies **can be composed of** the results of **complex queries**, involving
**multiple tables**

Some of the resons why you would use this:

- **Security**: **Giving** developers **limited acces** to the **original table**

```sql
  CREATE VIEW people_on_mars AS
    SELECT CONCAT('m', maritan_id) AS id, first_name, last_name
    FROM martian_public
      UNION
    SELECT CONCAT('m', visitor_id) AS id, first_nmae, last_name
    FROM visitor;
```

Then you can reference the view like any other table

```sql
  SELECT * FROM people_on_mars;
```

## Do union of two sorted views

You can't make further [sorting](./lhgd.md) to an already sorted view. Even if
it's two separated and individualy sorted views coupled together by
[UNION](./c76a.md) command

If you attempt this then the **sorting of both views will be lost**

**If** you **want** to do **union** on two **sorted queries sorround each one**
with `()`
