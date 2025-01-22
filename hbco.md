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

If you comine unions and structs you can have `tagged unions`, which can be
used to **store multiple different types** one at a time

For example let's say you have a `number` struct that you want to
use to store different types of numbers depending on their size

You could do something like this:

```c
struct number {
  int type; // To know what type to access
  int intNum;
  float floatNum;
  double doubleNum;
};
```

This is ok but know you will have a struct that it's the size of
the sum of all it's types, even though you just will want to
effectively store one type per struct instance


You could then do something like this instead:

```c
struct number {
  int type; // To know what type to access
  union {
    int intNum;
    float floatNum;
    double doubleNum;
  } num_t;
};

struct number n;
n.type = 0; // This might be better as a type or a constant
n.num_t.intNum = 32;
```

This way the total size of the struct is only the size of 
the `type` + the size of the largets type of the union (in this case
it's `double`)

### Access the members of union directly in the struct

You can omit having to access the members of a nested `union`
in a struct with the name of the union if you just don't include
it in the nested definition

> This are also called anonymus unions

```c
typedef struct {
  int type; // To know what type to access
  union {
    int intNum;
    float floatNum;
    double doubleNum;
  }; // no name!
} number;

number n;
n.type = 0;
n.intNum = 32; // Access directly
```

### Use structs inside a union for name and index access

An intersting use case for structs inside unions is that
you can use it to access members of a struct both by name
(for readability) and by index (for iteration)

This can happen if the elements of your struct are of the
same size and you have an array of the same size and type
since the memory layouts will match

> In this case the order of the structs will match the
> order where they are found in the array

```c
union Coins {
  // A struct the tracks the count of each coin
  struct {
    int quarter;
    int dime;
    int nickel;
    int penny;
  }; // anonymus strcucts can also be access directly
  int coins[4];
};

union Coins change;
// We compute the size of the array here (total_bytes_size / element_bytes_size)
for (int i = 0; i < sizeof(change) / sizeof(int); i++) {
    change.coins[i] = i * 2;
}

// There are 0 quarters, 2 dimes, 4 nickels, and 6 pennies
printf("There are %i quarters, %i dimes, %i nickels, and %i pennies\n",
change.quarter, change.dime, change.nickel, change.penny);
```

### Access a tag union using a switch case
