# lang.py.type.tuple

A data type like a list but immutable

## Synopis

```py
  tuple = ("foo", "bar", 3)
```

## Overview

A tuple is like a list except that:

- Defined by enclosing it in `()`
- Are **immutable**

## Why use instead of list

- **Faster** manipulating a tuple than the equivalent list
- If you **don't want data to be modified**
- To use as **keys** on a [dictionary](./0loj.md)

## Cookbook

### Index and slice tupples

All the **normal mechanisms** for slicing and indexing [lists](./7cxo.md) and
[strings](./s479.md) **work** just **as well** with tupples, with the **use**
of `[]`

```py
  t = ('foo', 'bar', 'baz', 'qux', 'quux', 'corge')
  print(t[0])           # "foo"
  print(t[-1])          # "corge"
```

### Define a single element tuple

When you try to define a **tuple with just one element**, Python **will interpretate**
it **as an expression and evaluate** the element inside it instead of creating a
tuple

If you want to avoid that an create a tuple that contain only one element then
**preceed the closing parenthesis with** a coma (`,`)

```py
  t = (2,)
  type(t)       # <class 'tuple'>
```

### Swap variable values between them

Often times you will need to **swap two variable values** around in most languages
you would need a temporary intermediate value

```py
  a = 5
  b = 6

  temp = a
  a = b
  b = temp

  print(a,b)    # 6 5
```

But thanks to tupples and their **packing and unpacking** features you can do
this **in an idomatic way**

```py
  a = 5
  b = 6

  a, b = b, a

  print(a,b)    # 6 5
```

### Pack and unpack a tuple

Assaignment to a tuple occurs in order, and then the reverse can be done to a
set of variables as lonog as they follow the same order and lenght

```py
  t = (1,2,3)
  print(t)      # 1 2 3

  a, b, c = t
  print(a,b,c)  # 1 2 3
```
