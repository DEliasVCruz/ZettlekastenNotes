# lang.py.module.sql.sqlalchemy

The standard ORM library for working with sql databases in python

## Synopsis

```py
  from sqlalchemy import Column, Integer, String, ForeignKey, Table
  from sqlalchemy.orm import relationship, backref
  from sqlalchemy.ext.declarative import declarative_base

  Base = declarative_base()
```

## Overview

This is an `Object-Relational Mapper` (ORM) library for **working** with
[sql](./wl6v.md) databases in an **object orientated** way

**Tables** are **defined as models** since they **include more information**
about the entity than a regular [sql table definitio](./rolo.md)

### Classes

You **construct tables** in an `OOP` approach, there for most parts of table are
generated from their **respective classes**

- `Table()`: Create a basic instance of a table object
- `Column()`: Create columns for your `Table` object
- `ForeignKey()`: Specify a foreign key relation inside your `Column`

## Cookbook

### Create a basic instance of a table

You can create a basic named table instance with the `Table()` [class](./unhs.md).

- The **first argument** is the **name** of the table
- The second argument is `declarative_base().metada` to allow functionality
- Then you can specify any number of `Column` objects

This method of creating table is **better suited for** `many-to-many` relationship
tables where it's **main identifier** is comprised of **foreign keys**

```py
  from sqlalchemy import Column, Integer, String, ForeignKey, Table

  Base = declarative_base()

  author_publisher = Table(
      "author_publisher",
      Base.metadata,
      Column("author_id", Integer, ForeignKey("author.author_id")),
      Column("publisher_id", Integer, ForeignKey("publisher.publisher_id")),
  )
```

### Declare columns for your table

To create a column in your table structure you need to do so by passing a
`Column()` class instance for each column in your table

It takes some of the following parameters:

- The column name (**Optional**)
- The column type
- `primary_key`: Boolean if the column value is a primary key
- A `ForeignKey` class instance

**If** the object is **call from** a declarative table definition (**as a
class**) then you can **skip passing a name**

```py
  from sqlalchemy import Column, String, Integer

  first_name = Column(String, primary_key=False)
  author_id = Column(Integer, ForeignKey('author.author_id'))
```

### Specify a foreing key in your table column

You can especify that a `Column()` instance references a foreing key by passing
an instance of the `ForeignKey()` class

- It takes a [string](./4t3v.md) as a `<lower-case-table-name>.<key-name>` structure

```py
  fk_author_id = ForeignKey("author.author_id")
```

### Define an entities collections

In a `one-to-many` relationship a **single entetity** can have **many
instances** of **another entity**

Thous you would normally not include this collections as attributes of an
entity, you can specify the collections relationship with the `relationship()`
function

It can take some of the following **parameters**:

- The **class name** to withch it is **related to** (as a `string`)
- `secondary`: If the table is related to another through secondary association table
- `back_populates`: The name of the complementary collection of the relation
- `backref`: Create an attribute to inspect the referenced entity

By **convetion** the **collection** would be **named in plural**

```py
  class Author(Base):
      __tablename__ = "author"
      author_id = Column(Integer, primary_key=True)
      first_name = Column(String)
      last_name = Column(String)

# This aknowledges the foreign key in the Books table class
      books = relationship("Book", backref=backref("author"))


  class Book(Base):
      __tablename__ = "book"
      book_id = Column(Integer, primary_key=True)
      author_id = Column(Integer, ForeignKey("author.author_id"))
      title = Column(String)
```

### The backref parameter

When you creation a relationship with another table, the `backref` parameter
will create an attribute with the same name for the referenced entity

You can then access the attributes of that original entity instance from
within referenced entity

```py
  book = session.query(Book).filter_by(Book.title == "The Stand").one_or_none()
  print(f"Authors name: {book.author.first_name} {book.author.last_name}")
```

### Define an entities many to many relationship

Usually for a `many-to-many` relationship you would define a complementary
table where each row will represent an unique permutation of the relationship

This mean that each entetity wouldn't have a related foreing key to the other
entities

But you can still express this relationship inside each table class definition
with the following parameters of the `relationship()` function:

- `secondary`: It points to the `Table` instance of the `many-to-many` table
- `back_populates`: The name of the corresponding collection in the other entity

```py
  class Author(Base):
      __tablename__ = "author"
      author_id = Column(Integer, primary_key=True)
      first_name = Column(String)
      last_name = Column(String)
      publishers = relationship(
          "Publisher", secondary=author_publisher, back_populates="authors"
      )

  class Publisher(Base):
      __tablename__ = "publisher"
      publisher_id = Column(Integer, primary_key=True)
      name = Column(String)
      authors = relationship(
          "Author", secondary=author_publisher, back_populates="publishers"
      )
```
