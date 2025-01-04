# lang.c.dynamic_allocation

Store data without initially knowing the size of the data

## Synopsis

```language
person *myPerson = (person *)malloc(sizeof(person));
```

## Overview

We won't always now how big is going to be the size of some
data, or if it's going to eventually grow, at compile time.

Dynamic allocation allows us to do this at `runtime`, so we
can have arbitrarily large data as we need it

### Allocate data dynamically

To allocate a chunk of memory, we need to have a pointer ready
to store the location of the newly allocated memory.

We can access the allocated memory by using that same pointer,
and we can use that pointer to free the memory later

Under `linux` systems we make use of the `malloc` function from
`<stdlib.h>` to reserve space on the `heap`

This function receives the `size in bytes` of data that we
want to allocate, and it returns a `void pointer` (which is
a pointer that doesn't have a type)

Since the `void pointer` does not have a type we need to
[type cast it](./e6e6.md) to the type that we are expecting

> Though this is not strictly necessary since `c` implicitly 
> converts the type of the returned pointer to the type of
> the pointer it's assigned to. But it's a good practice

```c
person *myPerson = malloc(sizeof(person));
```

## Cookbook

### Dynamically allocate a structure

Let's say you have a [function](./nt45.md) that you want it to return a
newly created [structure](./957e.md). Since the define structure will
only live on the stack of the function, to be able to access
it after the function returns we need to allocate it and return
the pointer

> Here we make the size of the new allocation to be just
> enough to hold the size of the person `struct` in bytes

```c
#include <stdlib.h>

typedef person * person_t;

person_t new_person() {
  return (person *)malloc(sizeof(person));
}
```

### Free allocated data

You can use the `free` function from `<stdlib.h>` to release 
the memory used by the allocation

> This does not delete the variable of the pointer but rather
> just free the memory, the pointer will still point to
> somewhere in memory and we can allocate new data to it

```c
#include <stdlib.h>

free(myPerson);
```
