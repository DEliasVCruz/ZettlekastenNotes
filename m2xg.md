# lang.psql.filtering

You can filter the displayed data based on conditions

## Synopsis

```sql
  SELECT <column-name> FROM <table-name> WHERE <conditions>;'
```

## Overview

You can perform conditional filtering of the [selected](./c76a.md) fields with
the `WHERE` command

You can **filter based on one** column or **many columns** as well as **any
number of conditions** in the order that they are defined

- You can **group conditions** using parenthesis `(...)`
- You **can't use** aggregator [function](./x41v.md) like `MIN()` inside `WHERE`

### Logic Operators

- `AND`: **Both** group of conditions **have to be satisfied**
- `BETWEEN`: **Select the records** that lie **inside** the specified **range**
- `IN`: **Check** if the record **equal** to a **set of values**
- `LIKE`: **Match** against a **pattern** using **wild cards**
- `REGEXP`: **Match** against a pattern using **regex**
- `OR`: **One or both** group of condition have to be satisfied
- `NOT`: **If** value does **not match the condition**
- `<=`: Less or equal
- `<>`: Not equal
- `=`: Equal to
- `>=`: Greater or equal

## Cookbook

### Filter based on equality

If you want to filter based on whether the **values of a field** are **equal**
to an specified **value** use the `=` sign

```sql
  SELECT * FROM person WHERE gender = "Female";
```

### Filter based on negation

When you want to match every value that **does not satisfy** the **test
condition** you can do so with the `NOT` command

```sql
  SELECT * FROM customers
  WHERE NOT city = 'Berlin';
```

### Filter based on multiple conditions

You can chain conditions with the **logic operators**

```sql
  SELECT * FROM person WHERE
      gender = "Male" AND
      (contry_of_birth = "Poland" OR country_of_birth = "China") AND
      last_name = "Pietersma";
```

### Filter based on empty or null values

If you want to select only those **records that have null/empty values** in the
specified field you can use the `IS NULL` command

```sql
  SELECT * FROM customers
  WHERE postal_code IS NULL;
```

### Filter based on values that are not empty or null

If you want only those records for which the specified **field is not
null/empty** then use the `IS NOT NULL` command

```sql
  SELECT * FROM customers
  WHERE postal_code IS NOT NULL;
```

### Specify a group of values the record can match

When you want to filter based on several values a field record has to match you
could chain `<field> = <value> OR` statements or you could use the `IN`
operator

**The following** SQL query:

```sql
  SELECT * FROM person WHERE
      country_of_birth = "China" OR
      country_of_birth = "Brazil" OR
      country_of_birth = "France";
```

Would be **the same as**:

```sql
  SELECT * FROM person WHERE
      country_of_birth IN ("China", "Brazil", "France");
```

### Select records inside a range

If you want to only return the records for which the **specified field lies
inside a range** of values you can use the `BETWEEN` command

```sql
  SELECT * FROM person
      WHERE <column-name>
      BETWEEN <lower-value> AND <upper-value>;
```

### Filter based on a pattern

You can match **based on** a general **pattern** defined by wild cards and the `LIKE`
command

The wild cards are as follow:

- `%`: Any character **any number** of times

```sql
  SELECT * FROM person
      WHERE email
      LIKE "%.com";
```

- `_`: Match any **single character**

```sql
  SELECT * FROM person
      WHERE email
      LIKE "___.com";
```

- `[]`: Match **one of** the characters

```sql
  SELECT * FROM customers
  WHERE city LIKE '[acs]%'

```

By default, the matching is **case sensitive**. If you want to do a **case
insensitive patter** matching then use the `ILIKE` command

You can also filter based on a **pattern that is not matched**

```sql
  SELECT * FROM person
      WHERE email
      NOT LIKE "%.com";
```

### Filter based on a regular expression

For more complex string matching you can use the `REGEXP` command to **match**
against a **regex** pattern

```sql
  SELECT city FROM station
  WHERE city REGEXP '^[aeiou].*'
```
