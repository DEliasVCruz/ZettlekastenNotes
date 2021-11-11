# lang.py.type.list

List are the basic type of **data structure** in python

## Overview

You can use lists to hold a set of **data elements** that you can **reference
later** by a **index number**. And they are defined by `[ ]` and **comma
separated**

They are **zero-based** indexed, meaning the **first element** has an index of 0

## Cookbook

### Create a list

There are **different ways to create** lists

- **Statically** define it

```py
  my_list = ["first element", "second element", "final element"]
```

### Append to an empty list

You can **add more** elements to **the end** of a list with `self.append()`

```py
  my_list = []
  my_list.append("some element")
```

If you append another list it will be appended as a **nested list**. If you
want to **append only the items one by one** you should use `extend()`

```py
  list1 = [1, 2 , 3]
  list2 = [4, 5 , 6]
  list1.append(list2)           # [1, 2, 3, [4, 5 , 6]]
```

### Append individual elements from a list into another

If you don't want to have a nested list and one to append a list into another
as one single list, you can use `self.extend(<iterable>)`

Furthermore this will **work in any iterable**

```py
  list1 = [1, 2 , 3]
  list2 = [4, 5 , 6]
  list1.extend(list2)           # [1, 2, 3, 4, 5 , 6]
```

If you **try to extend** a list with a **single string** then it will add **each
character** one by one **as new elements** in the list

```py
  my_string = ["apple", "pear", "banan"]
  my_string.append("hola")
  print(my_string)              # ["apple", "pear", "banan", "h", "o" , "l", "a"]
```

### Reference an element in a list

You can reference an element by its index **starting from** 0, you can also
reference the last element by the index `-1`

```py
  my_string = ["apple", "pear", "banan"]
  print(my_list[-1])            # ["banana"]
```

### Reference an element inside a nested list

A list can also be **composed of more list**. You can then reference by their
**subindex**

```py
  nested_list = [["some nested element", "anoter"], "some element"]
  print(nested_list[0][0])      # "some nested element"
```

### Split elements in a list

You can reference only a **subset of elements** in a list with `[<start>:<end>]`

This can also be used to **split** [strings](./4t3v.md) as in a way a **string is**
like a **list of characters**

It **does not include the upper limit** as part of the indeces split

```py
  my_string = ["apple", "pear", "banana"]
  print(my_string[:2])          # ["apple", "pear"]
```

### Turn a list into a single string

You can **join** elements in a list into a **single string** with `str.join(<list>)`

```py
  courses = ["Math", "English", "Biology"]
  courses_str = ", ".join(courses)      # "Math, English, Biology"
```

### Find the index of an element

To **reference** the index of an **specific element** in a list, you can use
the `self.index(<element>)`

```py
  courses = ["Math", "English", "Biology"]
  print(courses.index("Math"))          # 0
```

### Insert an element on an specified index position

You can insert an element into an **arbitrary index position** with
`self.insert(<index>, <element>)`. This will **shift up** every element from the
**specified index** forward

```py
  courses = ["Math", "English", "Biology"]
  courses.insert(1, "Chemistry")        # ["Math", "Chemistry","English", "Biology"]
```

### Remove the last element of a list

You can **use a list** as a **stack or quee** with the help of `self.pop()`.
**Together** with `append`, you can **replicate the behavior of a stack**

```py
  courses = ["Math", "English", "Biology"]
  courses.pop()     # ["Math", "English"]
```

### Perform sorting and reversing a list

**REMEMBER!!** thi will **PERFORM MUTATION mutation**

You can **sort** the elements in a list with `self.sort()` and you can
**reverse every** element (the last being the first and so on) with
`self.reverse()`

```py
  courses = ["Math", "English", "Biology"]
  courses.reverse()                 # Reverse the order of elements
  courses.sort()                    # Sort in ascending order
```

You can also **sort them in decreasing order**

```py
  courses = ["Math", "English", "Biology"]
  courses.sort(reverse=True)        # Sort in decreasing order
```

### Sort a list without altering the orignal list

You can **sort** the elements in a list **without modifying** the **original
list** with the `sorted()` builtin

Furthermore `sorted()` works on any [iterable]() including **strings** in which
case it will **return** a **list of sorted characters** in the string

```py
  courses = ["Math", "English", "Biology"]
  courses_sorted = sorted(courses)
```

### Check if an element is in the list

You can check wheter a list **contains** a **specific element** with the
`"element" in [list]` test keyword

```py
  courses = ["Math", "English", "Biology"]
  if "Math" in courses:
    print("There is Math")

  bool("Chemistry" in courses)      # False
```

### Find the max an minimum element

You can use the built-ins `max()` and `min()` with list to find the **maximum
and minimum value** element

```py
  nums = [2, 4, 6, 7, 1, 3, 9]
  print(min(nums))                  # Returns the min value
  print(max(nums))                  # Returns the max value
```

### Remove an arbitrary element

You can **remove an arbitrary** element that **matches** a given string in a list

```py
  courses = ["Math", "English", "Biology"]
  courses.remove("Math")            # ["English", "Biology"]
```

### Adding up lists together

Using the `+` operator to add list together **won't perform a matricial sum**
on the values of the list, **even if it's numeric elements**

This will **just join the elements** of both lists **into one list**

For that you are better off using **numpy**

```py
  list1 = [1, 2 , 3]
  list2 = [4, 5 , 6]
  print(list1 + list2)           # [1, 2, 3, 4, 5 , 6]
```
