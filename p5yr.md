# lang.py.module.pickle

Serialize complex data structures into compact byte format

## Synopsis

```py
  import pickle
```

## Overview

You can **serialize and deserialize** complex data structures, like an **object
state**, into compact byte forms for easy **transport** over a **network** or
saving to disk

Keep in mind that this pickle objects can only be operated by `Python` and are
non human readable

If you want a human readable and language agnostic form of serialization, you
can use [json]()

## Cookbook

## Serialize an object into a pickle

You can create a pickle of the current state of your object instance with the
`dump[s]` method

- `.dump()`: Dump the pickle object into a file
- `.dumps()`: Dump the pickle object into a string representation

## Deserialize a pickle into an object

You can turn a pickle object back into it's original object instance state with
the `load[s]` method

- `.load()`: Load the pickle object from a file
- `.loads()`: Load the pickle object from a string representation

### Define what gets serialized and what happens at deserialization

You can use the [magic methods](./a8n3.md) `__getstate__` and `__setstate__` to
define **what state** of the object **gets serialized** and **what happens
when** the state of the object is **restored at deserialization** respectively

```py
  import pickle

  class foobar:
      def __init__(self):
          self.a = 35
          self.b = "test"
          self.c = lambda x: x * x

      def __getstate__(self):
          attributes = self.__dict__.copy()
          del attributes['c']
          return attributes

      def __setstate__(self, state):
          self.__dict__ = state
          self.c = lambda x: x * x

  my_foobar_instance = foobar()

  my_pickle_string = pickle.dumps(my_foobar_instance)
  my_new_instance = pickle.loads(my_pickle_string)

  print(my_new_instance.__dict__)
```
