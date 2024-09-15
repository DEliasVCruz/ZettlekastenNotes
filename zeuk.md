# cpt.db.query.orm

An object relation mapper is a form of client library for constructing queries

## Overview

Is a form of constructing queries from a client library, to avoid having to
create `raw queries` and rather define your relationships in your code as
native object or structures

So then you can call methods or functions on those structures rather than have
to write direct `SQL` queries your self

Some well know `ORM` libraries are:
  - Python:
    - [Pony](./knfo.md) 
    - [SQLAlchemy](./abct.md) 
    - [Tortoise](./7tf0.md) 

## Drawbacks

They often get a bad rep, because they hide away the inner workings between your
application and the database. It's hard to optimize because you cann't directly
know what query or strategy is being performed, leading to problems like the
famouse [n+1](./ifsu.md) problem

## Cookbook
