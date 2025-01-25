# lang.c.functions.pointers

Define a function definition with dynamic implementations

## Synopsis

```c
void (*function_name)(int);
```

## Overview

There are times where you want to define a function for
which the implementation may vary depending on the needs
of the program

Or when you wan to pass a function as an argument to
another function, you only option in that case is a function
pointer

## Cookbook

### Defina and use a function pointer

A function function pointer only needs it's name, return value
and argument types as part of it's definition after that you
can pass it a pointer to any already implemented function

```c
#include <stdio.h>

void someFunction(int arg) {
  printf("This function is called with %d\n", arg) ;
  printf("We are finishing the function\n");
}

int main() {
  // Define the function pointer
  void (*my_function) (int);
  
  // Asign the function pointer
  my_function = &someFunction;

  printf("We are calling the pointer function\n")

  // Dereference the function pointer and call it
  (my_function)(2);

  printf("We are back to the main execution")

  return 0;
}
```

### Pass a function pointer as an argument

Some functions allow you to pass a function pointer
as one of it's arguments, this is to provide with
flexibility on some implementation aspects

For example the `qsort` function of the `stdlib.h` 
library, allow you to pass a `compare` function that
you can implement however you want as long as it
accepts the same type of arguments and returns the
same type of value

- Check [qsort](http://www.cplusplus.com/reference/cstdlib/qsort/) for more information

```c
#include <stdio.h>
#include <stdlib.h> // for qsort

// Thease are void to allow for greater flexibility
// On what things can be compare
int compare(const void* left, const void* right) {
  return (*(int*)right - *(int*)left); // Sort in descending order
}

int main() {
  int (*cmp)(const void*, const void*);
  cmp = &compare;

  int array[] = {1,2,3,4,5,6,7,8,9};
  int arrayLen = sizeof(array)/sizeof(*array);
  int valueSize = sizeof(*array);

  qsort(iarray, arrayLen, valueSize, cmp);

  for (int i = 0; i < arrayLen; i++) {
    printf("Value %d is %d\n", i, array[i]);
  }

  return 0;
}
```

### Define an array of function pointers

It's important to understand that when you declare
a function pointer the name of de declaration will
go in the part of the name of the function

- So this would be wrong

```c
void (*)int functions[];
```

Instead, to (in this case) declare an array of function
pointer you have to do this

```c
#include <stdio.h>

void f1 (int val) {
  printf("The value is %d\n", val)
}

void f2 (int val) {
  printf("The value is %d\n", val++)
}

int main() {
  // This will be the correct why to declare it
  // and optionally intialize it

  void (*functions[])(int) = {&f1, &f2};

  int i = 0
  while (i < 2) {
    // And this is how you would call each function
    (functions[i])(i);

    c++;
  }

  return 0;
}
```
