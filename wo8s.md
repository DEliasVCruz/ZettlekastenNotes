# lang.c.file

Handling files in `c`

## Synopsis

```c
#include <stdio.h>

FILE *file = fopen("example.txt", "r");
if (file == NULL) {
  printf("Failed to open the file\.n");
  return 1;
}
```

## Overview

The `c` standard library gives us a set of functions to
open, read and close files in various modes

### File opening modes

You can open a file in any of three modes:

- `w`: Open the file with the ability to (over) [write](./jwq0.md) it
- `r`: Open the file with the ability to [read](./mdav.md) it
- `a`: Open the file with the ability to write only to the
  end of the file

You can pass the `+` at the end of the mode to also include
the inverse operation, Ex. `a+` opens a file with the
ability to read and append

You may also add a `b` to indicate that you will be operating
ona binary file, however this has no effect in `unix`
systems, other systems like `windows` may require you
to do that distinction

## Cookbook

### Opening a file

You can use the `fopen` function from the `<stdio.h>` 
library to open a file, you just need to provide the 
name of the file and the mode in which you wish to 
open it

It will return a `FILE *` [struct](./957e.md) [pointer](./rmf8.md) that you use
to pass around as a **file handler** to the other functions
that expect it

If the return of `fopen` is `NULL` then an error has
occurred when trying to open the file

```c
#include <stdio.h>

FILE *file = fopen("example.txt", "r");
if (file == NULL) {
  printf("Failed to open the file\.n");
  return 1;
}
```

### Closing an opened file

You can use the `fclose` function to close a file
it will also ensure that any changes made to the
file are saved and free up the system

```c
fclose(file);
```
