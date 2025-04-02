---
tags: ["io", "files"]
---

# lang.c.file.read

Handling read operations with files in `c`

## Synopsis

```c
#include <stdio.h>

FILE *file = fopen("example.txt", "r");
if (file == NULL) {
  printf("Failed to open the file\.n");
  return 1;
}

int num;
fscanf(file, "%d", &num);
```

## Overview

The `c` standard library gives us a set of functions to
read data from text or binary files

## Cookbook

### Reading a string or character from a file stream

You can use the `fgets` and `fscanf` functions to read
a string or pattern, respectively, from a file.

The `fgets` function will continue to read from the 
file until the `EOF` or a `newline` is reached, it
will read at most `n` characters and will terminate
with the `null byte` after the last character in the
buffer

> We could use this to device a way to read line 
> by line

```c
FILE *file;
char line[100];

fgets(line, sizeof(line), file);
printf("%s", line);
```

On the other hand `fscanf` will continue to read
from the file until it finds the values that fulfill
it's pattern or `EOF` is reached

```c
FILE *file;
char line[100];

fscanf(file, "%s", line);
```

### Reading a single character from a file stream

You can use the `fgetc` function to read a single 
character at a time from the file.

Keep in mind that `fgetc` will continue to read a new
character from the file until `EOF` or an error is
reached

> The difference with `getc` is that it may be
> implemented as a macro in some systems

```c
char letter = fgetc(file);
```

### Detecting the end of a file

When reading from a text file one character at a time
you can check for `fgetc` to return the `EOF` value

```c
char c;
while ((c = fgetc(file)) != EOF) {
  ...
}
```

### Reading bytes directly from a binary file

You can read the bytes directly from a file with
the `fread` function. Which is very usefull for binary 
encoded formats

The function takes 4 arguments:
- Adress of the data to be read into
- The size of the data to be read
- Number of times the data has to be read
- The pointer to the file to read from

> You can even read structs and arrays provided that 
> you pass the correct data size of the struct/array

```c
typedef struct {
  int num1, num2, num3;
} my_struct;

int main() {
  FILE *file = fopen("myfile.bin", "rb"):
  if (file == NULL) {
    return 1;
  }

  my_struct nums[2];
  // nums is already a pointer to the first struct
  fread(nums, sizeof(my_struct), 2, file);

  fclose(file);

  my_struct first = nums[0];
  fprintf("The number: %d, %d, %d\n", first.num1, first.num2, first.num3);

  my_struct second = nums[1];
  fprintf("The number: %d, %d, %d\n", second.num1, second.num2, second.num3);

  return 0;
}
```
