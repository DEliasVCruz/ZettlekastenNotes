# lang.py.syntax.classes.dataclass

Simplify classes definition by automating common requirements

## Synopsis

```py
  from dataclasses import dataclass

  @dataclass[(<arguments>)]
  class <clas-name>:
      <attribute>: <type> [= <default-value>]
```

## Overview

The `dataclass` decorator allows you to **save time** when defining
[classes](./unhs.md) by having **common operations implementations** for your
custom class set automatically

What sets it apart is that it has basic data model [magic methods](./a8n3.md)
like `__init__,` `__repr__,` and `__eq__` implemented for you.

- Otherwise, they **work like** and are define like **any other class**
- This makes classes **easier** to **maintain, implement and use**

### The field function

The `dataclasses` module provides a `field` functions that lets you **customize
each field** of a data class **individually**

It can achieve so with the following parameters:

- `default`: Default value of the field
- `default_factory`: Callable function that returns the value of the field
- `init`: If use field in `__init__()` method (**Default** is `True`)
- `repr`: If use field in `repr` of the object (**Default** is `True`)
- `compare`: If include field when doing comparison (**Default** is `True`)
- `hash`: If use field when calculating `field()` (**Default** same as `compare`)
- `metadata`: A mapping with information about the field

### Dataclass options

You can call the `dataclass` decorator with **different options**:

- `init`: If it should add an `__init__` method (**Default** is `True`)
- `repr`: If it should add a `__repr__` method (**Default** is `True`)
- `eq`: If it should add an `__eq__` method (**Default** is `True`)
- `order`: If it should add ordering methods (**Default** is `False`)
- `unsafe_hash`: If it should force add a `__hash__` method (**Default** is `False`)
- `frozen`: If it should make attributes **immutable** (**Default** is `False`)

### Alternatives

Thou as good as they are, `dataclasses` can be, if so desired, substituted by
**other data structures** like:

- `attrs`: The inspiration for the `dataclass` module

  - Very similar in structure and functionality
  - Can do everything `dataclasses` can
  - Has some **more flexibility and features**
  - Is not part of the standard library (**external dependency**)

- `NamedTuples`: They allow you to create [tuples](./hsr4.md) with values are
  named and access as attributes

  - It provides less features than a `dataclass`
  - Is still a regular tuple, **no awareness** of it's **own class**
  - Will compare two different named tuples
  - It's **completely immutable**

## Cookbook

### Add type hints

Adding **type hints** to your variable declarations is **mandatory**. But
**if** you **don't want** to set an specific type for your variable you can use
the `Any` type from the [typing](./k62q.md) module to catch any type

- This, however, **won't enforce** the type annotations **at runtime**

```py
  from dataclasses import dataclass
  from typing import Any

  @dataclass
  class WithoutExplicitTypes:
      name: Any
      value: Any = 42
```

### Define immutable default values

When defining variables and attributes, is **bad practice** to pass a **mutable
object**, such as [lists](./7cxo.md), as a **default value**

You can use the `field` function and it's `default_factory=` parameter to
**handle** cases like this when you need to **specify a default** value with a
**mutable object**

- The argument to `default_factory` can be **any zero parameter callable**
- Trying to define a bare default mutable object will cause a value error

```py
  from dataclasses import dataclass, field
  from typing import List

  def make_french_deck():
      return [PlayingCard(r, s) for s in SUITS for r in RANKS]

  @dataclass
  class Deck:
      cards: List[PlayingCard] = field(default_factory=make_french_deck)
```

### Define a custom attribute field

You can also use the `field` function to **customize** the **characteristics**
of **each attribute** in your class

- You can **access** the `metadata` information with the `fields` function

```py
  from dataclasses import dataclass, field, fields

  @dataclass
  class Position:
      name: str
      lon: float = field(default=0.0, metadata={'unit': 'degrees'})
      lat: float = field(default=0.0, metadata={'unit': 'degrees'})

# Get the metadata from the third attribute
  lat_unit = fields(Position)[2].metadata['unit']
  print(lat_unit)                                       # degrees
```

### Allow for instance comparison

By default the `dataclass` won't implement `magic methods` for comparing
instances of your `dataclass` with `<`, `>`, `<=`, `>=` operators

You can pass the `order=True` option to the `dataclass` decorator to enable it

```py
  @dataclass(order=True)
  class PlayingCard:
      rank: str
      suit: str
```

### Define a custom comparison criteria

When implementing the `order` option in your `dataclass` by **default** the
**comparison criteria** that it will use is by **comparing** each
**attribute** values of the comparing instances **as tuples**

But there might be cases where you need a custom comparison criteria. For that
you need to define a `sort_index` attribute

But since this attribute is calculated from other attributes, you can use the
`__post__init__()` special **magic method** to do **special processing after**
the regular `__init__`

This will **still do** comparison by **comparing attributes** as **tuples**,
but the **first element** of the tuple will serve as the **first sorting
index**, unless there are ties

```py
  @dataclass(order=True)
  class PlayingCard:
      sort_index: int = field(init=False, repr=False)
      rank: str
      suit: str

      def __post_init__(self):
          self.sort_index = (RANKS.index(self.rank) * len(SUITS)
                             + SUITS.index(self.suit))
```

### Create immutable attributes

You can **specify** that the **attributes** of your class **will be
immutable**, meaning they **won't** be able to **be re-assigned** after being
defined, with the `frozen=True` option

```py
  @dataclass(frozen=True)
  class Position:
      name: str
      lon: float = 0.0
      lat: float = 0.0
```

### Managing inheritance

You can use inheritance you would normally, with just **some caveats**:

- When a **child** class defines **new attributes**, they will **positionally
  last** over it's parents attribute when creating an instance

```py
  @dataclass
  class Position:
      name: str
      lon: float
      lat: float

  @dataclass
  class Capital(Position):
      country: str

  Capital('Oslo', 10.8, 59.9, 'Norway')
```

- **If** a **parent** class has some **default values** then it's **children**
  classes must define attributes with **default values**

```py
  @dataclass
  class Position:
      name: str
      lon: float = 0.0
      lat: float = 0.0

  @dataclass
  class Capital(Position):
      country: str              # This won't work
```

- If an **attribute** of a **parent** class is **redefine** inside a child
  class it will **keep** it's **positon** on the **argument list** when crating
  an instaance

```py
  @dataclass
  class Position:
      name: str
      lon: float = 0.0
      lat: float = 0.0

  @dataclass
  class Capital(Position):
      country: str = 'Unknown'
      lat: float = 40.0

  Capital('Oslo', 10.8, country='Norway')
```
