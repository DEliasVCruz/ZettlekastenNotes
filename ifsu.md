# cpt.db.query.problems.n+1

A performance issue when there are many, many queries being performed

## Overview

Typically found when working with [orms](./zeuk.md) is a problem that
originates from structuring your code so that you first do a query to get
a list of records and then you do a query for each of this records
to get their related data

This can lead to bad performance:
  - In the time that it takes the client to fetch all the data
  - In the preasure that we are puting the in the database with many queries
  - Each individual query consumes the most ammount of time in network IO
    - Thease add up when wating for each individual result in sequence

## Examples

### Fetching related elements of a list of items

Here we see a common problem where the `ORM` is first used to list all the
books and then for each individual book item we are doing a new query
for it's reviews

The number of queries exectued will be equal to:
  - `N`: as the number of books returned from listing the items
  - `+1`: refering to the initial query to list all the items

Thus it will be the number of elemts returned from the list plus the first
initial query to get the list `N+1`

```js
books = db.books.all().limit(20)

for (book of books) {
  reviews = book.reviews().limit(5)
  ...
}
```

## Cookbook
