# lang.py.module.sql.pony.schema

Declare the entities and schema of your database

## Synopsis

```language
  from pony.orm import Database, Required

  db = Database()

  class User(db.Entity):
      <attr-name> = Required(<type>)
```

## Overview

You can either design your schema with `Pony` mapped objects based on the
schema of an existing database

## Cookbook

### Define a different name for your table

By default it will map the class name to a corresponing table name in your
database

You can use the `_table_` magic attribute of your entity to specify a diferent
table name for the mapped table than the one in your class name

```py
  class PrimaryUnit(db.Entity):
      _table_ = 'user'
```

### Define a not nullable column

If you define a column as an instance of the `Required()` class then it will be
mapped as a `NOT NULL` column

```py
  class User(db.Entity):
      name = Required(str)
```

### Define a primary key column

You can specify that a column is a **primary key** with the `PrimaryKey()`
class

- `auto`: A [boolean](./6auy.md) if the key will be auto-generated

```py
  from pony.orm import PrimaryKey
  from uuid import UUID, uuid4

  class User(db.Entity):
      id = PrimaryKey(UUID, default=uuid4, auto=True)
```

### Define a composite primary key

You can define a **primary key** that consists of the **unique union of other
column** in your table

1. Define your composite columns
2. Call `PrimaryKey` without assigning it and pass the columns instances

```py
  class User(db.Entity):
      name = Required(str)
      last_name = Required(str)
      PrimaryKey(name, last_name)
```

### Define a secondary key

Table can only have one primary key. But they can have a **secondary composite
key** (from the **union of other column** values) with the `composite_key`
function

- This mean that the **set of columns** must have a **unique combination per record**

```py
  from pony.orm import PrimaryKey, Required, composite_key

  class User(db.Entity):
      id = PrimaryKey(UUID, default=uuid4, auto=True)
      name = Required(str)
      last_name = Required(str)
      composite_key(name, last_name)
```

### Define a column as nullable

You can set a column as an optional column (meaing it can accept `NULL` values)
with the `Optional()` class

- It's recommended to pas the `nullable=True` parameter anyway
- It accpets the same data type specification parameters as `Required()`

```py
  class User(db.Entity):
      name = Required(str)
      gender = Optional(str, nullable=True)
```

### Define a column as only unique values

If you want to specify that the column **can only consist of unique values** (no
duplicate data). You can use the `unique=True` parameter

```py
  class User(db.Entity):
      name = Required(str)
      email = Required(str, unique=True)
```

### Use a default value for your column

You define a default value for a column **either as a variable or a calable**
with the `default=` parameter

```py
  class User(db.Entity):
      name = Required(str)
      satus = Required(str, default='active')
```

### Use a different column name

By default, it will map your instance names to the name of the columns in your
database. You can specify a different name for the database column with the
`columns=` parameter

- It takes either a single [string](./4t3v.md) or a [list](./7cxo.md)

```py
  class User(db.Entity):
      name = Required(str)
      email = Required(str, columns='emai_adress')
```

### Define cascade delete rules

When defining an attribute that references or is reference by another entity,
you can pass the `cascade_delete` parameter. To specify what odd to happen in
case the given entity is deleted

```py
  class Person(db.Entity):
      name = Required(str)
      passport = Optional("Passport", cascade_delete=True)

  class Passport(db.Entity):
      number = Required(str)
      person = Required("Person")
```

### Define extra options for specific datatypes

### Define methods and properties

You can define methods and properties like you normally would inside your
entity definition

- They can call [queries]() and and entity methods
- They can be used inside your queries

```py
  class Person(db.Entity):
      first_name = orm.Required(str)
      last_name = orm.Required(str)
      entire_name = orm.PrimaryKey(str, default=(f'{first_name} {last_name}'))
      cars = orm.Set(lambda: Car)  # Instead of passing 'Car' as a string

      @property
      def full_name(self):
          return f'{self.first_name} {self.last_name}'

      @property
      def has_car(self):
          return not self.cars.is_empty()

      def cars_by_color(self, color):
          return orm.select(car for car in self.cars if car.color == color)
          # or return self.cars.select(lambda car: car.color == color)


  with orm.db_session:
      # persons' full name
      orm.select(p.full_name for p in Person)

      # persons who have a car
      orm.select(p for p in Person if p.has_car)

      # persons who have yellow cars
      orm.select(p for p in Person if orm.count(p.cars_by_color("yellow")) > 1)

      # sum of all cars that have owners
      sum(p.cars_price for p in Person)
```
