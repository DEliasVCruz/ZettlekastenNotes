# lang.py.module.sql.pony.transactions

Handler for database transaction management with Pony

## Synopsis

```py
  from pony.orm import db_session

  @db_session
  def my_transaction();
      ...
```

## Overview

`Pony` takes care off the heavy lifting when interacting with your database
through transactions

You just need to **wrap any interaction** with either the `db_session` function in
it's [decorator](./ff01.md) form or [context manager](./1rwn.md) form

A transaction is **executed and handle** with the **following commands**:

- `commit()`: Complete a single transaction after calling it
  - **Saves all changes** made within the current session
- `rollback()`: Go back to the state of db before the last transaction
  - **Rollback the current transaction**

The `db_session` function `commits` a transaction **automatically** after
leaving it's context. **And** it performs `rollback` if something goes wrong

- **Each session** defines a **single** `atomic` transaction
- Instance variables will only be available inside the session

## Cookbook

### Execute a transaction

You should wrap all your transactions under the `db_session`:

- As a **decorator**:

```py
  @db_session
  def func():
      # a new transaction is started

      p = Product[123]      # Only available for this sesion
      p.price += 10
      # commit() will be done automatically
```

- As a **context manager**:

```py
  with db_sesion:
      # a new transaction is started

      p = Product[123]      # Only available for this sesion
      p.price += 10
      # commit() will be done automatically
```

### Perform several transactions within the same db_session

If you need more than one transaction within the same database session you can
**call** `commit()` or `rollback()` **at any time** during the session, and
then the **next query will start a new transaction**.

```py
  @db_session
  def func1():
      p1 = Product[123]
      p1.price += 10
      commit()          # the first transaction is committed
      p2 = Product[456] # a new transaction is started
      p2.price -= 10
```

### Access the values of a newly created instance within the same session

Whe create a new instance (row) of an entity table inside a `db_session` to be
abble to referecne inmediately you first need to call the `flush()` function to
be able to reference it's attributes

```py
  class Customer(db.Entity):
      id = PrimaryKey(int, auto=True)
      email = Required(str)

  @db_session
  def handler(email):
      c = Customer(email=email)
      # c.id is equal to None
      # because it is not assigned by the database yet
      c.flush()
      # c is saved as a table row to the database.
      # c.id has the value now
      print(c.id)
```

### Commiting when using more than one database

If you are working with more than one database you may want to prematurily
commit to one or the other database by calling `.commit()` on the database
instance as a method

```py
  db1 = Database()

  class User(db1.Entity):
      ...

  db1.bind('postgres', ...)


  db2 = Database()

  class Address(db2.Entity):
      ...

  db2.bind('mysql', ...)

  @db_session
  def do_something(user_id, address_id):

      # Commit to the frist database
      u = User[user_id]
      db1.commit()

      # Second transaction for the first database
      # Same transaction for the second database
      a = Address[address_id]
      ...
```

### Using with a generator or a coroutine

You can't use the `db_session` inside a [generator](./grh0.md) or an
[asyncrounous]() process you need to wrap this processes inside the `db_session`

```py
  @db_session
  def my_generator( x ):
      obj = MyEntity.get(id=x)
      yield obj
```

### Specifying when a transaction finish inside a generator

When using a **generator for a transanction**, the program **can reenter** the
generator code for **several times**. In this case, when your program leaves the
generator code, the `db_session` is **not over, but suspended**

you have to explicitly commit or rollback current transaction before the
program leaves the generator on yield

```py
  @db_session
  def my_generator( x ):
      obj = MyEntity.get(id=x)
      yield obj
      obj = MyEntity[x]
      commit()
      yield obj
```

### Locking transactions and database access for concurrency

Ther will be times when multiple operations are done at the same time by
different transactions

To handle this gracefully, systems like `Pony` implement some `locking`
protocol to ensure data integrigty

You can read about it [here](https://docs.ponyorm.org/transactions.html#optimistic-concurrency-control)
