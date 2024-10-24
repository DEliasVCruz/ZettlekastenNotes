# lang.go.syntax.generics



## Synopsis

```language

```

## Overview

## Cookbook

### How to type assert a type parameter value

Since the type of `x` (where it's a type parameter of a generic) is exactly
of type parametr you can't do type assertion on it

In this case something like this, won't work:

```go
_, ok = x.(int)   // ... cannot use type assertion on type parameter value ...
```

You can only do type assertions on interface values. So you must convert
first `x` to a valid interface type first like `any`/`interface{}`

```go
func isInt[T any](x T) (ok bool) {
    _, ok = any(x).(int) // convert, then assert
    return
}
```

## Sources

- Stack overflow  [response](https://stackoverflow.com/a/71588125) on type assertion of
  type paramters

