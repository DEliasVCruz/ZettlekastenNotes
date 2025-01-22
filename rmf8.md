# lang.c.pointers.arithmetics

Perform arithmetic on pointer values to move across memory

## Synopsis

```c
int char[2] = {'a', 'b'};
printf("%c", *(char+1)) // "b"
```

## Overview

There are multiple arithmetic operations that you can perform
on pointers to move across the momory space

> Depending on the type of pointer that it is, the arithmetic
> operation will be performed in the maginitud of the pointer
> type size

## Cookbook

### Incrementing and decrementing pointers

You can use the standard `++` and `--` to increment or decrement
a pointer by `1` respectively

This will move the space in memory based on the size of the
type of the pointer

So for an `int` pointer it will move the pointer `4` bytes and
for a `char` pointer it will move it by `1`

> Keep in mind that this will modify the pointer in place
> since its equivalent to `<val> = <val> + 1`, so pass it
> to a new variable if you don't want the mutation

```c
#include <stdio.h>

int main() {
  int numbers[5] = {10, 20, 30, 40, 50};

  int *intpointer = &numbers[3];
  printf("%d", *intpointer); // 40

  intpointer++; // now 4 bytes from the original pointer value
  printf("%d", *intpointer); // 50

  intpointer--; // now back 4 bytes
  printf("%d", *intpointer); // 40

  return 0;
}
```

### Adding and substracting to pointers

Similarly you can add or substract arbitrary numbers to the
pointer value and it will move the corresponding byte size
in memory adresses

```c
#include <stdio.h>

int main() {
  int numbers[5] = {10, 20, 30, 40, 50};

  int *intpointer = &numbers[2];
  printf("%d", *intpointer); // 30

  // now 8 bytes from the original pointer value
  printf("%d", *(intpointer + 2)); // 50

  printf("%d", *intpointer); // 30

  intpointer -= 2; // now back 8 bytes
  printf("%d", *intpointer); // 10

  return 0;
}
```
