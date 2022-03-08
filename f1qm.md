# lang.py.module.sql.pony.relations

Stablish relations between Pony table enteties

## Synopsis

```py
  from pony.orm import Required, Set

  class <entity-name>(db.Entity):
      fk = Required(<FK-Entity>)

  class <FK-Entity>(db.Entity):
      <entities> = Set(<entity-name>)
```

## Overview

You can stablish relationship between table entities as `sets` and `required`
foreing key. **Each relation must have it's colection counterpart** in the other
entity

- `Pony` will take care of creating intermediary tables for `many-to-many`
  relationships

## Cookbook

### Define a foreing key

To reference another table entity as a foreing-key you need to pass to the
`Required()` class either

- A string with the name of the entity class
- The entity class if it already has been define
- A [lambda](./8uan.md) that returns the entity class

```py

  class FK1(db.Entity):
      id = PrimaryKey(int, auto=True)

  class FK3(db.Entity):
      id = PrimaryKey(int, auto=True)

  class User(db.Entity):
      name = Required(str)

      fk_1 = Required(FK1)          # Foreing key as class
      fk_2 = Required('FK2')        # Foreing key as string
      fk_3 = Required(lambda: FK3)  # Foreing key as lambda

  class FK2(db.Entity):
      id = PrimaryKey(int, auto=True)

```

### Define a one to many realtionship

Here we have an entity that holds a reference `foreing-key` to another entity.
And that other entity can be a foreing key to many other entities

Thus it holds a `Set()` of instances of that entity and that counter
relationship must be defined

```py
  class Citizen(db.Entity):
      name = Required(str)
      district = Required('District')

  class District(db.Entity):
      name = Required(str)
      citizens = Set(Citizen)
```

### Define a many to many relationship

When defining tales that have a `many-to-many` realtionship, Pony will
**automatically** create any **intermidiate table**

- To do this you need to define `Set()` in both entities

```py
  class Product(db.Entity):
      tags = orm.Set("Tag")


  class Tag(db.Entity):
      products = orm.Set(Product)
```

### Customize many-to-many relationships intermidiate table

You can pass the `table` and `columns` parameteres to the `Set()` class to
specify the name of the intermidiate table and it's columns

```py
  class Student(db.Entity):
      name = orm.Required(str)
      courses = orm.Set("Course", table="Study_Plans", columns=["course", "semester"])


  class Course(db.Entity):
      name = orm.Required(str)
      semester = orm.Required(int)
      students = orm.Set(Student, column="student_id")
      orm.PrimaryKey(name, semester)

  # The final table will be called 'Study_Plans'
  # It will have the column names: 'studen_id' 'course' 'semester'
```

### Handle multiple relationships between entities

**When** having **entities** that **have many realtionships**, you need to
provide the `reverese` parameter to **know what is it's counterpart** in the
other entitiy

```py
  class User2(db.Entity):
      tweets = orm.Set("Tweet", reverse="author")
      favorites = orm.Set("Tweet", reverse="favorited")


  class Tweet(db.Entity):
      author = orm.Required(User2, reverse="tweets")
      favorited = orm.Set(User2, reverse="favorites")
```

### Define a self referential relationship

When defining a self referential realtionship, you need to **provide** the
`reverse` parameter **to know what it's counterpart is**

```py
  class Person(db.Entity):
      name = orm.Required(str)
      spouse = orm.Optional("Person", reverse="spouse")  # symmetric one-to-one
      friends = orm.Set("Person", reverse="friends")  # symmetric many-to-many
      manager = orm.Optional("Person", reverse="employees")  # one side of non-symmetric
      employees = orm.Set("Person", reverse="manager")  # another side of non-symmetric
```
