# lang.psql.dates

Data type for working with dates

## Overview

Every date [type](./x350.md) can be formatted to only include the **date or time**
stamp with `::[DATE|TIME]`

## Commands

- `INTERVAL`: Perform **arithmetic operations** on dates
- `EXTRACT()`: **Get specific parts** of a date (year, month, etc)
- `NOW()`: Get a timestamp of the **current date** (not operational)
- `CURRENT_DATE`: Get only the current date at the start of the transaction
- `CURRENT_TIME`: Get only the current time at the start of the transaction
- `CURRENT_TIMSTAMP`: Get only the current timestamp at the start of the transaction
- `MAKE_DATE()`: Create a date from it's integer values
- `AGE()`: Get the **elapsed time** btween two dates

## Cookbook

### Operate over dates

You can add or substract dates to get new dates or intervals

- Add or substract days to a date by adding or substracting an integer to the date
- Substract dates producing the number of days elpased

```sql
  SELECT DATE '2022-08-05' + 1 -- 2022-08-06
  select date '2022-08-05' - '2022-08-04' -- 1
```

### Add or subtract date interval

You can add or subtract from date types with the `INTERVAL` command and
**passing a time** (ex. 5) **and measure** (ex. YEAR[S])

```sql
  SELECT (<data-type> [ - | + ] INTERVAL "<time> <MEASURE>")[::[DATE|TIME]];
  SELECT (DATE '2022-08-05' - INTERVAL "1 DAY") -- 2022-08-04
```

### Get current date and times

You can use `CURRENT_DATE` to get the date without time zone and `CURRENT_TIME`
to get the current time with time zone and you can get a time stamp with `CURRENT_TIMESTAMP`

- This can be operated on
- Their values don't change during the transaction

```sql
  SELECT CURRENT_DATE - 1; -- Get the date for yesterday (2022-08-04)
```

### Get the current time stamp of the transactio

You can **get the current time** timestamp of the executed transaction with the
`NOW()` [function](./x41v.md)

- This is made with the time zone in mind
- This can not be operated on

```sql
  SELECT NOW()::[DATE|TIME];
```

### Get only the date or the time of a timestamp

You can turn any date type into just the date or time part by appending `::[DATE|TIME]`

```sql
  SELECT NOW()::DATE    -- 2022-08-05
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

You can also use the equivalent `date_part`

```sql
  SELECT DATE_PART(month, date '2022-08-05') -- 5
```

### Create dates from individual parts

You can create date tipe values from integer values

```sql
  SELECT MAKE_DATE(2022, 08, 25) -- 2022-08-25
```

### Truncate the precision of a date

You can truncate down a date or time to an specified precision wiht `date_trunc`

- It works with time stamps and with zone info too

```sql
  SELECT DATE_TRUNC('hour', TIMESTAMP '2001-02-16 20:38:40') -- 2001-02-16 20:00:00
```

### Normalize the presentation of a set of measure dates

This is usefull if you have a measuer of days or hours that goes beyond the
normal amount of this measure that a month or day may have respectively

- Use `justify_days` to get the number of months and days in 30 day months
- Use `justify_hours` to get the number of days and hours

```sql
  SELECT JUSTIFY_DAYS(INTERVAL '35 days') -- 1 mon 5 days
  SELECT JUSTIFY_HOURS(INTERVAL '27 hours') -- 1 day 03:00:00
```

### Find the age based on a birthday

You can use the `AGE()` function to calculate the age based on a endign date
(`NOW()`) and an starting date (birthday)

- By default this will output a detailed description of the **elapsed time**
  and `interval`

```sql
  SELECT NAME,
  EXTRACT(YEAR FROM AGE(NOW(), date_of_birth)) AS AGE
  FROM person;
```

You can also get the interval time between a given date and the current date
by only passing the timestamp

```sql
  SELECT AGE(TIMESTAP '1957-06-13') -- 62 years 6 mons 10 days
```
