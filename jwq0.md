---
tags: ["io", "files"]
---

# lang.c.file.write

Handling write operations with files in `c`

## Synopsis

```language
#include <stdio.h>

FILE *file = fopen("example.txt", "r");
if (file == NULL) {
  printf("Failed to open the file\.n");
  return 1;
}

int num = 2;
fprintf(ptr, "%d", num);
```

## Overview

The `c` standard library gives us a set of functions to
write data to text or binary files

## Cookbook

### Writing a string or character to a file stream

You can use the `fprintf` function to write a string 
or pattern to a file.

You can also use the `fputs` function to write an
unformatted string into a file with a new line

```c
int num = 24;
fprintf(file, "The number is %d\n", num);
fputs("Another line", file);
```

### Writing a single character from a file stream

You can use the `fputc` function to write a single 
character at a time on the file.

> The difference with `putc` is that it may be
> implemented as a macro in some systems

```c
char letter = 'H';
fputc(&letter, file);
```

### Write bytes directly into a binary file

You can write the bytes directly into a file with
the `fwrite` function. Which is very usefull for binary 
encoded formats

The function takes 4 arguments:
- Adress of the data to be written
- The size of the data to be written
- Number of times the data has to be written
- The pointer to the file to write to

> You can even write structs provided that you pass
> the correct data size of the struct

Assuming that an `int` consist of `4 bytes` then this
code will write `4 * 3 * 2` bytes into the file
in the [endianness](./p4bx.md) of the system

```c
typedef struct {
  int num1, num2, num3;
} my_struct;

int main() {
  FILE *file = fopen("myfile.bin", "wb");
  if (file == NULL) {
    return 1;
  }

  my_struct nums = {12, 24, 15};
  fwrite(&nums, sizeof(my_struct), 2, file);

  fclose(file);

  return 0;
}
```
