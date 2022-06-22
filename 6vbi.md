# lang.py.module.secrets

Built-in module to create true random values

## Synopsis

```py
  from secrets import SystemRandom

  random_generator = SystemRandom()
  rand_int = random_generator.randrange(1, 50)
```

## Overview

The `secrets` modules provides **true random** values generation unlike the
[random](./f4oh.md) module. This makes it best suited for cryptographic
porpuseses

## Cookbook

### Generate a secure random integer

To generate a random [integer]() number you can use the `randbelow` function.

- It returns a random integer lesser than the one provided

```py
  from secrets import randbelow

  rand_number = randbelow(23)   # Random integer from 0 to 22
```

### Select a random element

You can select a random element from a **non empty** [iterable](./p7q9.md) with
the `choice` function

- Can work for [lists](./7cxo.md), [strings](./4t3v.md), [tuple](./hsr4.md), etc

```py
  from secrets import choice

  name = "Daniel"
  letter = choice(name)     # i

  name_list = ["Daniel", "Jose", "Maria"]
  name = choice(name_list)  # Jose
```

### Generate a secure random integer from a range

You can create random integer numbers from a given range with either:

- `randit()`: The end of the range is **inclusive**
- `randrange()`: The end of the range is **exclusive**, allows a steping factor

In both methods the begining of the range is inclusive

- This is a method of the `SystemRandom` class, so you will a need an instance of it

```py
  from secrets import SystemRandom

  random_generator = SystemRandom()

  random_number = secretsGenerator.randint(0, 50)
  print(random_number)
# 23

  random_number2 = secretsGenerator.randrange(4, 40, 4)
  print(random_number2)
# 32
```

### Generate a secure random float

You can generate random floating numbers from a range of floating numbers with
the `uniform` method

- This is a method of the `SystemRandom` class, so you will a need an instance of it
- The last float of the range is exclusive

```py
  from secrets import SystemRandom

  random_generator = SystemRandom()
  random_float = random_generator.uniform(2.3, 25.8)    # 18.062235454990407
```
