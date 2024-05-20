# lang.py.oper.function.map_filter_reduce

There are verious builtin functions for functional programming

## Synopsis

```py
  [map|filter|reduce](<function>, <iterable>)
```

## Overview

This function return [generator](./grh0.md) objects that needs to be iterated
through or wrapped around a [list()](./7cxo.md) fucntion

This is a great way to **procces and transform** item in a **iterable without**
the need of a `for loop`

But keep in mind that this is **not considered pythonic**. For **more
pythonic** approches you can use **generator expressions** or list
[comprehensions](./7lub.md)

### Map()

You can use the map function to execute a function on every element of an
[iterable](./p7q9.md)

```py
  def addition(n):
    return n + n

  numbers = (1, 2, 3, 4)
  result = list(map(addition, numbers))
  print(result)             # [2, 4, 6, 8]
```

- You can use it with a [lambda](./8uan.md) function for quick mapping

```py
  base = [1, 2, 3, 4]
  incremented_base = list(map(lambda x: x + 1, base))
  print(incremented_base)   # [2, 3, 4, 5]
```

- You can also **pass any** other **built** in function

```py
  strings = ['1', '2', '3']
  numbers = list(map(int, strings))
  print(numbers)            # [1, 2, 3]
```

### Filter()

You can use filter to get the elements of a list based on whether it satisfies
a given function

```py
  numbers = [1, 2, 3, 4, 5, 6, 7, 8, 9, 10]

  def check_even(number):
      if number % 2 == 0:
            return True
      return False

  even_numbers = list(filter(check_even, numbers))

  print(even_numbers)     # [2, 4, 6, 8, 10]
```

- You can also use a lambda function for a quick filter

```py
  ages = [1, 2, 3, 4, 5, 6]
  less = list(filter(lambda x: x < 4, ages))
  print(less)           # [1, 2, 3]
```

- You can also get all the [truthy](./6auy.md) values if you pass `None` as the
  filter function

```py
  random_list = [1, 'a', 0, False, True, '0']
  filtered_list = list(filter(None, random_list))

  print(filtered_list)  # [1, 'a', True, '0']
```

### Reduce()

To acces this function you first need to imported from the
[functools](./50x9.md) module

You can use reduce to apply a function to an iterable and reduce it to a
**single cumulative value**

The basic functionality of `reduce()` is to take an existing function, apply it
cumulatively to all the items in an iterable, and **generate a single final
value**.

- **Apply** a function to the first two values of an iterable to get a partial
  result

- **Use** that partial result together with the next element to generate
  another partial result

- **Repeat** the process until the iterable is exhausted and return a single
  comulative value

```py
  from functools import reduce

  li = [1, 2, 3, 4]
  result = reduce(lambda x, y: x + y, li)

  print(result)         # 10
```

## Cookbook

### Process multiple iterables with map

You can use process more than one iterable if the function allows for more than
one argument.

You just need to pass each iterable with to the map function. The mapping will
stop at the length of the shortest iterable

- In this example we use `pow()` to raise each element in the first iterable to
  the power of the corresponding element in the second iterable

```py
  first_it = [1, 2, 3]
  second_it = [4, 5, 6, 7]

  powers = list(map(pow, first_it, second_it))

  print(powers)           # [1, 32, 729]
```

### Use methods of a class on every element with map

You can also use map to apply a method of an instance of a [class](./unhs.md)

```py
string_it = ["processing", "strings", "with", "map"]
capitalized = list(map(str.capitalize, string_it))

print(capitalized)      # ['Processing', 'Strings', 'With', 'Map']
```

### Mapping a function that needs extra arguments

If the function you are mapping accepts extra arguments that you want to pass,
you will be better off using a [lambda](./8uan.md) function

```py
with_dots = ["processing..", "...strings", "with....", "..map.."]
processed = list(map(lambda s: s.strip("."), with_dots))

print(processed)        # ['processing', 'strings', 'with', 'map']
```

### Pass an initializer to reduce

You can pass an initial value to the reduce function, by specifying it as it's
third argument. This is most commonly used when you know you are going to
operate on potentially empty iterables

```py
  result = reduce(my_add, [], 0)

  print(result)         # 0
```
