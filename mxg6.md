---
tags: ['go', 'iterators', 'generators', 'lazy-eval']
---

# lang.go.syntax.iterators

Define custome iterable collection to loop over with the range keyword

## Synopsis

```go
func iter(yield func() bool)
```

## Overview

You can use custom iterators whenever you would want to use the `range`
keyword to iterate over collections that are not maps or slices

The values of a custom iterable are lazyly evaluated and only processed
and given upon requesting them

So basically an iterator is a function that returns an array of elements,
but instead of returning them all at once it only yields one element at
a time, for each iteration of the loop

## Cookbook

### Create a custom iterator

You create a custom iterator by defining a `function` that takes another
function (which may contain any number of argumets) and returns a `bool`

To function that it's passed as a `clousure` can have any name but it's
convention to call it `yield`

The returned `bool` value is used to indicate that we've stopped looping
in the iterator

The body of the function `yield` will be what it's define inside the
`range` iteration when using the custom iterable, meaning that as
long as you passed the required arguments to the yield function
you could preprocess them before they are passed to the body of the
iteration process

```go
funct myIterator(yield func(i int) bool) {
  for i := range 3 {
    // We check here for the case of an early return when iterating
    if !yield(i) {
      return
    }
  }
}

func main() {
  for i := range myIter {
    fmt.Printf("%d\s", i)
  }

  fmt.Println()

  // What it's compiled into
  myIter(func(i int) bool {
    fmt.Printf("%d\s", i)

    return true
  })
}

# 0 1 2
# 0 1 2
```

### Create a map function using iterators

You can create a functionality similar to `map` function, where you
apply a mutation over each element of a slice. You can use the `iter`
package to get aliases for the iterator function type

```go
package main

import (
  "fmt"
  "iter"
)

type Slice []int

fuunc (s Slice) Map(transform func(int) int) iter.Seq[int] {
  return func(yield func(int) bool) {
    for _, v := range s {
      mapedValue := transform(v)
      shouldContinue := yield(mapedValue)

      if !shouldContinue {
        return
      }
    }
  }
}

func main() {
  numbers := Slice{0, 1, 2, 3}

  doubled := numbers.Map(func(number int) int { 
    return number * 2 
  })

  for v := range doubled {
    fmt.Printf("%d\s", v)
  }
}

# 0 2 4 6
```

### Creating a simple generator function with iterators

Though you can build [generators in go](./a10r.md) using the standard language
features, with the introduction of iterator functions you can now do
it natively with a few lines

> A generator is a function that returns an array of elements, but instead 
> of returning them all at once it only yields one element at a time, for 
> each iteration of the for loop.

This feats similar to the functionality of a function iterator, but with
the limitation of not having methods to only grab the next value, or an
specific number of values

```go
func Sequence(yield func(int) bool) {
  i := 0
  
  for {
    // The body of range over statement will
    // be executed here
    if !yield(i) {
      return
    }

    // This will be executed after the body 
    // of the range over statement
    i++

    // On the next iteration the value passed to
    // the range over statement will be the new value
  }
}

func main() {
  for i := range Sequence {
    fmt.Println(i)
  }
}
```

## Sources

- Article on how to [generators using go iterators](https://makubob.medium.com/exploring-the-upcoming-go-generators-344b2fb98ff9) 
