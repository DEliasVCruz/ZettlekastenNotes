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

### Saving the contents of an opened file

If you want to save to disk a file buffer while still
using the file (not yet close) you can use the `fflush` 
function

> You can also use `fflushall` to flush the buffers of
> all open streams

```c
fflush(file);
```

### Closing an opened file

You can use the `fclose` function to close a file
it will also ensure that any changes made to the
file are saved and free up the system

```c
fclose(file);
```

### Getting data from random access in a file

Normally as you [read](url) or [write](url) data to/from a
file the `cursor` will be moving allong from where
it started depending on the opening `mode`

So if you wanted to get to an specific record you
would have to `read`/`write` through the file
in a loop until you get to the record of interest

However you can do this efficiently with the `fseek`
function. It moves the cursro to an specified
record an it take `3` arguments

- The pinter to the file
- The offsent from wher to find the record
- The location from where to start the offset

> Offsets can be negative to move backwards

There are `3` possible offset starts:
- `SEEK_SET`: Starts the offset from the begining of the file
- `SEEK_END`: Starts the offset form the end of the file
- `SEEK_CUR`: Start the offset from the current location of the
  cursor on the file

> You can also use the function `rewind` to quickly reset the
> cursor to the begingn of the file

```c
typedef struct {
  int num1, num2, num3;
} my_struct;

int main() {
  FILE *file = fopen("myfile.bin", "rb"):
  if (file == NULL) {
    return 1;
  }

  // Move the cursor just at the beginig of the last written value
  fseek(file, -sizeof(my_struct), SEEK_END);

  my_struct nums[2];
  // We read it into the pointer of the last struct in the array
  fread(&nums[1], sizeof(my_struct), 1, file);

  // At this point the cursor is at the end of the read struct in the file
  // We now move it back twice so that we are at the start of the first struct
  fseek(file, -2*sizeof(my_struct), SEEK_CUR);

  // We read it into the pointer of the first struct in the array
  fread(nums, sizeof(my_struct), 1, file);

  fclose(file);

  my_struct first = nums[0];
  fprintf("The number: %d, %d, %d\n", first.num1, first.num2, first.num3);

  my_struct second = nums[1];
  fprintf("The number: %d, %d, %d\n", second.num1, second.num2, second.num3);

  return 0;
}
```

### Deleting a file

You can rename a file with the `remove` function

```c
int status = remove("my_file.txt");
if (status != 0) {
  fprintf("Error removing file\n");
}
```

### Renaming a file

You can change the name of an exiting file with 
the `rename` function

```c
int status = rename("my_file.txt", "other_name.txt");
if (status != 0) {
  fprintf("Error renaming file\n");
}
```

### Low level handling of files

You can perform ubuffered `io` on files, meaning that
each `read`/`write` request will result in accessing the
disk directly to `fetch`/`put` an specific number
of bytes

Here instad of file pointers, we use `low-level` file
handlers or `file descriptors`, which give an unique
integer number to identify each file

```c
To open a file.
int open(char *filename, int flag, int perms);

To create a file.
create(char *filename, int perms);

To close the file.
int close(int handle);
```
