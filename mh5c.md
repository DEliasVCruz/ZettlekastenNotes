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

Keep in mind that under certain circumstances `malloc` can
return a `NULL` pointer, so it's a good pracrtice to check
for it

```
char *buff = (char *)malloc(n * sizeof(char));j
if (buff == NULL) {
  return 1;
}

// continue execution
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

### Dynamic memory allocation for arrays

Since we know that we can traverse [arrays](./xp8m.md) using pointers 
and we can also dynamically allocate contiguous blocks of
memory using pointers. We can mix this two concept to
dynamically allocate an array

This is usefull when we don't know at compile time how big
our array needs to be, so we can allocate as much memory
as needed at runtime

It's also usefull when we want to create an array inside a
function stack scope and have still be used by it's parent
caller if a pointer to the allocated array it's returned

> In this case we use `array` notation to traverse a block
> of memory from a `pointer`

```c
#include <stdlib.h>

// Allocate memory to store 5 characters

int n = 5;
char *pvowels = (char *)malloc(n * sizeof(char));

pvowels[0] = 'A';
pvowels[1] = 'E';
*(pvowels + 2) = 'I';
pvowels[3] = 'O';
*(pvowels + 4) = 'U';

for (int i = 0; i < n; i++) {
  printf("%c", pvowels[i]);
}

free(pvowels);

printf("\n");
```

### Dynamically allocate a two dimension array

The only difference with the normal way of creating
a dynamic array is that here we will allocate a pointer
to a pointer for the main array and then allocate the
block memory for each pointer

> This can be generalize to n-dimesions arrays

```c
#inlcude <stdlib.h>
#include <stdio.h>

int nrows = 2;
int ncolums = 2;

// Allocate memory for nrows pointers
char **pbuff = (char **)malloc(nrows * sizeof(char *));

pbuff[0] = (char *)malloc(ncolumns * sizeof(char));
pbuff[1] = (char *)malloc(ncolumns * sizeof(char));

pbuff[0][0] = 'A';
pbuff[0][1] = 'B';
pbuff[1][0] = 'a';
pbuff[1][1] = 'b';

for (int i = 0; i < nrows; i++) {
  for (int j = 0; j < ncolumns; j++) {
    printf("%c", pbuff[i][j]);
  }

  printf("\n")
}

// Free individual row pointers
free(pbuff[0])
free(pbuff[1])

// Free top level pointer
free(pbuff)
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
