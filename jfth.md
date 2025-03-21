# lang.c.strings

How to work with string in `c`

## Synopsis

```c
char *name = "Daniel Vilela";
```

## Overview

In `c` strings are actually [arrays](./xp8m.md) of `characters`, so we can
define a simple string as a [pointer](./xl2p.md) to an array of characters

### String as pointers

When you declare a `string` as a `char` pointer, the follwing
happens

```c
char *name = "Daniel";
```

1. A local (stack) variable called `name` gets allocated, which is
   pointer to a single character
2. The string `Jhon` is stored sequentially (character by character)
   somewhere in memory
3. The `name` variable it's initialized to point to where the first
   character of the string (`J`) resides at (which is followed by
   the rest of the `string` in memory)

This means that we can access the `name` variable as an `array`
and it will work, accessing it's `0` element will return the
value of the character `J`

Since we know that the memory is sequential, we can keep moving
ahead in the `index` to get the next value of the string, until
we reach the **null string terminator** `\0` which represents 
the end of the `string` in memory

## Cookbook

### Create a read only string

If you define a `string` as a `pointer` to a character array, then
this will create a string that can only be used for reading

```c
char *name = "Jhon Smith";
```

### Create a mutable string

If you want to create a string that you can modify and 
manipulate, then you need to define the string as a
local character `array`

This notation is different since it allocates an `array`
variable so we can manipulate it

> When using a string literal for the definition then
> you don't need to set the explicit length, the compiler
> can calculate it for you

```c
char name[] = "Daniel Vilela";
```

If you want to manually define the character array, then
you need to add `1` to the length to account for the
`null` string terminator

> The string terminator is an special character equal to 0
> That would be represented in bits as `00000000`, and it
> indicates the end of a string

```c
char name[14] = "Daniel Vilela";
```

### Calculate the length of a string

You can use the `strlen` function from the `<string.h>` library
to calculate the length, without the string terminator, of 
a `string`

```c
#include <string.h>
#include <stdio.h>

int main() {
  char *name = "Daniel Vilela";

  /* The lenght is 13 */
  printf("The lenght is %d\n", strlen(name));
}
```

### Compare strings

You can compare the equality of two strings using the `strncmp` 
function from the `<string.h>` library

> Do not use the unsafe version `strcmp`

It returns the number `0` if the strings are equal, and any
other different number if they are different

> This means that in conditional expression you have to do
> the check of the result for it to work properly

The arguments are the two string to be compared and the
maximum comparison length

```c
#include <stdio.h>
#include <string.h>

int main() {
  char *name = "Jhon";

  if (strncmp(name, "Jhon", 4) == 0) {
    printf("Hello, Jhon\n");
  } else {
    printf("Go away\n");
  }

  /* Do a pseudo begins with */

  char *code = "IPF123";

  if (strncmp(code, "IPF", 3) != 0) {
    printf("Use a valid code");
  }
}
```

### Concatenate strings

You can append a string into another string (string 
concatenation), using the `strncat` function from the
`<string.h>` library

It takes three arguments:
  - The `dest` string (the string we are appending to)
  - The `src` string (the string we are taking to add from)
  - `n`, which is the maximum number of characters to append
    from the `src` string

It will append the **first** `n` characters of the `src` string
to the `dest` string

Where `n` will be the minimum between the `n` passed as an 
argument and the `length` of the `src` char array

> This function can only be used with `dest` strings define 
> as character arrays, the `src` string can be a `char *`

Keep in mind that the `dest` string (character array) `buffer`
has to have enough `capacity` (array lenght) to hold the
newly added charcters (plus the string terminator)

```c
#include <stdio.h>
#include <string.h>

int main() {
  char dest[20] = "Hello";
  char src[20] = "World";

  strncat(dest, src, 3);

  /* This prints "HelloWor" */
  printf("%s\n", dest);

  strncat(dest, src, 20);

  /* This prints "HelloWorWorld" */
  printf("%s\n", dest);
}
```

### Empty a string

You can set a string as empty (liek `""`) by setting it's
first value to the **null character** `'\0'`

> Look out how this is define using `''` rather than `""`

```c
char name[14] = "Daniel Vilela";

name[0] = '\0';
```

### Convert a string to a number

You can use the `atoi`, `atol` functions, from the `<stdlib.h>` 
to convert from an [ascii](./q8iq.md) string to a `int` 
or `long` respectively, this however do not detect errors on 
the conversion from string to number

```c
char *str_value = "16";
int value = atoi(str_value);
```

### Convert a string to a number while handling errors

If you want to handle errors then you need the `strtol` function
from the `<stdlib.h>` library. It will handle the base you give
it for the `ascii` number and it can take a `pointer` to a `char *`
to set where the parsing stopped due to a non numeric character

This means you can check if the the provied string started with
a non numeric value by checking if the pointers are the same, and
check if it contained a non numeric character by checking then
if the pointer does not point to the `null terminator`

For other kind of errors (like out of bound value) you can check
the `errno` value that will be set after the call

```c
#include <stdlib.h>
#include <errno.h>
#include <limits.h>
#include <stdio.h>

int main(int argc, char **argv) {
  char *value_str = argv[1];
  char *endptr;

  long value = strtol(value_str, &endptr, 10); // On base 10

  if ((errno == ERANGE && (value == LONG_MIN || value == LONG_MAX)) || 
    (errno != 0 && value == 0)) {
    
    perror("strtol");

    return 1;
  }

  if (endptr == value_str) {
    printf("Pliss use a numeric value\n");

    return 1;
  }

  if (*endptr != '\0') {
    printf("Pliss use a numeric value\n");

    return 1;
  }
}
```

### Convert a number into a string

To be able to convert a number into a string you will first 
need to find out how big of a `buffer` you are going to need
to store the string, you can use the property of the `snprintf`
function of telling you how much it would have write, to
get that size, then allocate a buffer and actually write it

```c
#include <stdio.h>

int main() {
  int my_number = 1340;

  // Pass a null buffer and set max write to 0
  int buff_size = snprintf(NULL, 0, "%d", my_number);

  // Add one to account for the null terminator
  char str_buff[buff_size + 1];


  snprintf(str_buff, buff_size+1, "%d", my_number);

  printf("%s\n", str_buff);

  return 0;
}
```
