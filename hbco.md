# lang.c.unions

Treat the same block of memory as different type or names

## Synopsis

```c
union number {
  int value;
  char bytes[sizeof(int)];
};
```

## Overview

They are essentially the same as [structs](./957e.md) just that instead
of each variable of the struct having it's own memory (thus the
final size of the struct is the sum of the size of it's variables)
a `union` allows for multiple names to the same variable

The names can **treat the variable as different types** and the final
size of the `struct` will be equal to the size of the variable name of 
the **biggest size** (plus any padding the compiler decides to add)

## Cookbook

### Creating a simple union

For this example we will examine a case where you would like to store
and access an `int` as both it's literal type value and also as an 
[array](./xp8m.md) of bytes

This will allow you to get the concrete `type` value if you want and
also have a convinient way to acces it's bytes withouth having to
do [pointer arithmetics](url) 

> Remember that an `int` is 32 bits and thus will use 4 bytes and
> that `sizeof` return the total length in bytes of the provided
> value

```c
// In this case the total size will be 4 bytes
// Since both types in the union are of the same size
union number {
  int value;
  char bytes[sizeof(int)];
};

union number parts;
parts.value = 5968145; // Arbitrary number to be greater than 255 (1 byte)

// This is printing each byte as a `char` (int8) value
printf("The int is %i, it's bytes are [%i, %i, %i, %i]",
parts.value, parts.bytes[0], parts.bytes[1], parts.bytes[2], parts.bytes[3]);
```

If you were not to have used `union` you would have to do
this instead

> Here we are getting the `int` pointer with `&parts` , offseting from the pointer by
> `n` bytes, then casting it as a `char *` and dereferencing that pointer (which
> will get 8 bits of memory, a byte, from that pointer)

```c
int parts = 5968145;

printf("The int is %i, it's bytes are [%i, %i, %i, %i]",
parts, *((char *)&parts+0), *((char *)&parts+1), *((char *)&parts+2), *((char *)&parts+3))
```

### Create a tagged union

### Access the members of union directly in the struct
