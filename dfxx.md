# lang.psql.select.case

Execute a switch case statement operation in SQL

## Synopsis

```sql
  SELECT CASE
              WHEN <condition> THEN <result>
              ELSE <result>
         END
  FROM <table-name>;
```

## Overview

You can perform a **swtich case statement** that will evaluate the case test for
each row and return the specified value for witch the test is made

## Cookbook

### Perform nested case statements

You can embed switch **case** statements **inside of other** swtich **case** statements

```sql
  SELECT CASE
              WHEN A + B > C AND B + C > A AND A + C > B THEN
                  CASE
                      WHEN A = B AND B = C THEN 'Equilateral'
                      WHEN A = B OR B = C OR A = C THEN 'Isosceles'
                      ELSE 'Scalene'
                  END
              ELSE 'Not A Triangle'
          END
  FROM TRIANGLES;
```
