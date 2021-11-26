# lang.py.type.generator

A special function that return an iterable that is not stored in memory

## Synopsis

```py
  def my_generator():
    # operations
    yield <value>
    [<operations>]
```

## Overview

Is a special kind of [function](./8xrz.md) that return a **lazy**
[iterator](./p7q9.md) that you **can loop through** but it **does not store**
it's contents in **memory**

So you can **acces** it's **elements one by one** without storing it's previous
or next element in memory

Unlike regular functions the **state** of the function **is remembered** after
each call

But remember you can **only iterate** through an interator **one time only**.
Once you've **exahausted** an iterator youw **will get** an `StopIteration`
[execption](./wvgx.md)

## Methods

The generator object has some special methods

### **self**.send()

You can use `yield` as an expression to **operate on the yielded value** and
then **send it back** to the generator on it's **next function call** with it's
**new state**

In this example once the `infinite_palindromes()` **function** is **called
again** and a **palindrom** has been **found** the **value of** `i` will be `10
** (digits)` that was **pass through with** the `.send()` method; **otherwise**
it will be `None`

This is because the `i` will **only resume** it's state **if** the `yield`
expression **is hit**

```py
  def infinite_palindromes():
      num = 0
      while True:
          if is_palindrome(num):
              i = (yield num)
              if i is not None:
                  num = i
          num += 1

  pal_gen = infinite_palindromes()

  for i in pal_gen:
      digits = len(str(i))
      pal_gen.send(10 ** (digits))
```

### **self**.throw()

This allows you to **raise** an [exception](./wvgx.md) with the generator. In
the following example the **iteration is stopped** with the error

```py
pal_gen = infinite_palindromes()

for i in pal_gen:
    print(i)
    digits = len(str(i))
    if digits == 5:
        pal_gen.throw(ValueError("We don't like large palindromes"))
    pal_gen.send(10 ** (digits))
```

### **self**.close()

This allows you to **stop the iteration of a generator** since it **will
raise** a `StopIteration` error

```py
pal_gen = infinite_palindromes()

for i in pal_gen:
    print(i)
    digits = len(str(i))
    if digits == 5:
        pal_gen.close()
    pal_gen.send(10 ** (digits))
```

## Cookbook

### Read large data sets

The **usual way** of **reading** through a **file** might be to enter all it's
row into a list and then do operations **on** that **list**.

**But if** it's a **large file** you might end with a very large **list** that
is **fully stored in memory**

The `open()` function will return a generator object. So you could access each
row of the file with the `yield` [statement](./4g9v.md)

```py
  def csv_reader(file_name):
    for row in open(file_name, "r")
      yield row
```

### Define multiple yield statements

When you call a special method, like `next()`, on a generator object; the **code**
will be **executed up to** the `yield` statement.

On the **next** function **call** it **will resume from that last yield
statement** and continue executing.

Effectively you **could have multiple yield statements** that will work as "break
points" in your function

```py
  def multi_yield():
      yield_str = "This will print the first string"
      yield yield_str
      yield_str = "This will print the second string"
      yield yield_str


  multi_obj = multi_yield()

  print(next(multi_obj))      # This will print the first string
  print(next(multi_obj))      # This will print the second string

  print(next(multi_obj))
# Traceback (most recent call last):
#   File "<stdin>", line 1, in <module>
# StopIteration
```

### Create data pipelines

Data pipelines allow you to **string together code** to **process large
datasets** or streams of data **without maxing** out your machine’s **memory**.

Take for example parsing a large CSV file and finding the total sum

```py
  file_name = "techcrunch.csv"
  lines = (line for line in open(file_name))
  list_line = (s.rstrip().split(",") for s in lines)
  cols = next(list_line)
  company_dicts = (dict(zip(cols, data)) for data in list_line)
  funding = (
      int(company_dict["raisedAmt"])
      for company_dict in company_dicts
      if company_dict["round"] == "a"
  )
  total_series_a = sum(funding)
  print(f"Total series A fundraising: ${total_series_a}")
```
