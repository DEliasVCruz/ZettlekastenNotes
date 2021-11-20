# lang.psql.dates

Data type for working with dates

## Overview

Every date [type](./x350.md) can be formatted to only include the **date or time**
stamp with `::[DATE|TIME]`

## Commands

- `INTERVAL`: Perform **arithmetic operations** on dates
- `EXTRACT()`: **Get specific parts** of a date (year, month, etc)
- `NOW()`: Get a timestamp of the **current date**
- `AGE()`: Get the **elapsed time** btween two dates

## Cookbook

### Add or subtract dates

You can add or subtract from date types with the `INTERVAL` command and
**passing a time** (ex. 5) **and measure** (ex. YEAR[S])

```sql
  SELECT (<data-type> [ - | + ] INTERVAL "<time> <MEASURE>")[::[DATE|TIME]];
```

### Get the current time

You can **get the current time** timestamp with the `NOW()` [function](./x41v.md)

```sql
  SELECT NOW()::[DATE|TIME];
```

### Extract specific values from a date

If given a date type you **only want a specific part of that timestamp** like for
example **the year or the month, etc**.

You can **use** the `EXTRACT()` function

```sql
  SELECT EXCTRACT(YEAR FROM NOW());
  SELECT EXCTRACT(MONTH FROM NOW());
  SELECT EXCTRACT(DAY FROM NOW());
```

You can even extract **day of the week** (`DOW`), **century** or even **milliseconds**

```sql
  SELECT EXCTRACT(DOW FROM NOW());
  SELECT EXCTRACT(CENTURY FROM NOW());
```

### Find the age based on a birthday

You can use the `AGE()` function to calculate the age based on a endign date
(`NOW()`) and an starting date (birthday)

By default this will output a detailed description of the **elapsed time**

```sql
  SELECT NAME,
  EXTRACT(YEAR FROM AGE(NOW(), date_of_birth)) AS AGE
  FROM person;
```
