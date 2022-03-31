# lang.py.module.sql.pony.query

Working with Pony database query objects

## Synopsis

```py
  from pony.orm import select
```

## Overview

You can work on queries either using [generator](./grh0.md) expressions or
[labmda](./8uan.md) functions

## Cookbook

### Perform a select query with an generator expression

With the `select()` function you can pass a query as a
[comprehensio](./7lub.md) like structure

```py
  from pony.orm import select

# Getting customeres where the sum of the total price of it's orders is over 1000

  query = select(c for c in Customer
                 if sum(c.orders.total_price) > 1000)

# Returning a tuple of the instance and an aggregation
  query_tuple =  select((c, sum(c.orders.total_price))
                         for c in Customer if sum(c.orders.total_price) > 1000)
```

### Perform a select query with a lambda function

You can perform a select query by calling the `select()` method of the class
entity table you want to query

- You need to call it on the entity class table
- It accepts a [lambda](./8uan.md) filter function
- It **returns** a `Query` class instance and doesn't executed until iteration

```py
  products = Product.select(lambda prod: prod.price > 100)
```

### Functions you can use inside a select query

You can use the some of the following fucntions inside a `select()` query

- `avg()`: Get the average of a generator or set
- `len()`: Get the maximum value of a generator or set
- `min()`: Get the maximum value of a generator or set
- `count()`: Return the number of objects that match the query condition
- `sum()`: Get the sum of the values of a generator or set

Each of these, and more, can be used outside the `select()` function, you can
leanr more about them [here](https://docs.ponyorm.org/queries.html#functions-which-can-be-used-inside-a-query)

```py
  select(avg(c.orders.total_price) for c in Customer)
```

### Check if a query return at leat one result

You can use the `exists()` method of a query that will return `False` if the
query returns no results

```py
  select(c for c in Customer if len(c.cart_items) > 10).exists()
```

### Filter an existing query

You can use the `filter()` method on a query object with a lambda expression

```py
  query2 = query.filter(lambda person: person.age > 18)
```

### Perform nested queries

You can perform new queries **based on another query**:

```py
  query3 = select(customer.name for customer in query2
                  if customer.country == 'Canada')
```

### Iterate over a select query

**To execute** the **query** you **must iterate through** it, and then you can
access it's individual attributes

```py
  for p in Product.select(lambda p: p.price > 100):
      print(p.name, p.price)
```

### Operate on a select query as an indexable list

If you wish to iterate through the query as a list and slice and index search
it's results you can pass an `index-filter`

```py
  # Return all product elements query results as a list

  product_list = Product.select(lambda p: p.price > 100)[:]
```

### Limit query results

You can limit the number of results of a query with:

- Index the query like a list
- `.first()`: Get the first result
- `.last()`: Get the last result
- `.limit()`: Limit the number of results

```py
  query = select(p.price for p in Price if p.price > 100)
                .order_by(Product.price)
                .first()
```

### Sorting query results

You can use the `order_by()` method of a `select()` query to perform sorting of
your results

- By default the sorting will be done in ascending order
- To sort in descending order use the `desc()` function

```py
  from pony.orm import desc

  Product.select(lambda p: p.price > 100).order_by(desc(Product.price))
```

### Sort a query based on complex functions

You can pass a **lambda function** to your **sort criteria** for more **complex
sorting**. It takes **only one parameter** as an individual instance entity

```py
# Sort by the price of the product

  Product.select(lambda p: p.price > 100).order_by(lambda p: desc(p.price))

# Sort by the sum of the total price of the orders of the customers

  Customer.select().order_by(lambda c: desc(sum(c.orders.total_price)))
```

### Sort a query based on more than one sort criteria

To sort on **more than one criteria**, pass it as **comma separated arguments**
(`,`). For the lambda version return your sorting criteria as a [tuple](./hsr4.md)

**In this example**, we first sort by the product price in descending order and
then by the product name in ascending order

```pu
# As a normal query sorting operation

  Product.select(lambda p: p.price > 100).order_by(desc(Product.price), Product.name)

# As a lambda sorting function

  Product.select(lambda p: p.price > 100).order_by(lambda p: (desc(p.price), p.name))
```
