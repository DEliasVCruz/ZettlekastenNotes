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
