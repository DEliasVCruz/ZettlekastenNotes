---
tags: ["performance", "compare", "go"]
---

# lang.go.pkg.unique

Make efficient canonical representations of objects for comparison

## Synopsis

```go
import (
    "unique"
)

func main() {
  helloHande := unique.Make("hello")
  worldHandle := unique.Make("World")
}
```

## Overview

The `unique` package of the standard library can be used to create
canonical representation of objects, so that we can make more
efficient comparisons than by directly comparing their underlying
values

This is very useful for performance critical applications where
you need to make a lot of comparisons between different types

You do this by creating a `handle` of the value, this will work
as the canonical version of the item, so that it can be easily
compared with another handle

Storing them also becomes more efficient since you are not storing
multiple versions of the same value, but rather a one true canonical
version of it

## Cookbook

### Efficiently compare two types for equality

You can use it to make fast and efficient comparisons between
string or even `structs`

But you first have to make a handle of the value you want
to compare, and unique handles can only be compare to other unique
handles

> Since this needs to create a handle for each value, it's important
> to keep in mind that this results in much "verbose" code that might
> be harder to read and extended

You can use the `Make` function to create a unique handle of a value

```go
package main

import (
    "fmt"
    "unique"
)

func main() {
  helloHande := unique.Make("hello")
  worldHandle := unique.Make("World")

  fmt.Println(helloHande == worldHandle) # false
}
```

### Get the original value of a unique handle

You can have access to the original value of the `unique` handle
by using the `Value` method

```go
package main

import (
    "fmt"
    "unique"
)

func main() {
  helloHande := unique.Make("hello")

  fmt.Println(helloHande.Value()) # hello
}
```

### When is using unique handles not necessary

It's overkill to use `unique` handles when you are comparing numbers
since this is already as fast as it can get

You may also just want to create `enums` with int values for efficient
membership comparisons
