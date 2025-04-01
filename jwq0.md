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

### Writing a single character from a file stream

You can use the `fgetc` function to read a single 
character at a time from the file.

Keep in mind that `getc` will continue to read a new
character from the file until `EOF` or an error is
reached

```c
char buffer[100];
fgets(buffer, sizeof(buffer), file);
```
