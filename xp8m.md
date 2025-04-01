# lang.c.array

A continues block of memory that can hold more than one value

## Synopsis

```c
/* defines an array of 10 integers */
int numbers[10];
```

## Overview

In `c` you can define `arrays` that are a continues block of memory
that can hold more than one value of the same type

This means that the size of a given array will be equal to the
size of it's underlying types, times the length of the array

- For a `int numbers[10]` this will be `32 * 10` with a size of `320 bits`

Arrays in `c` are `zero` based, so for an array of size `10` the
array cells from `0` to `9` (inclusive) are defined

### Arrays as pointers

Arrays are actually [pointers](./xl2p.md) and when we access it's elements
with the `[]` operator we are actually dereferencing a pointer
to an offset from where the array pointer is

When you declare an array as part of the local context (stack) it
will retain the information of it's length and the type of data that
it have, but when you pass it as [function](./nt45.md) argument, it will
**degrade** into a pointer type and thus it will loose all the
information that it had as an array

> This is why we pass things like the length too so that we can
> now from the function body

Therefore the name of an array is a constant pointer to the first
element of an array.

This means that given an `char array[5];` (where the size of `char` is
`1 byte`) the notations `array`, `&array[0]` and `array + 0` will
all return a pointer that points to the same location

Further more, given the same example, `*(array + 1)` and `array[1]`
will give the same (dereferenced) value

## Cookbook

### Define and initialize an array in one statement

Though you can define an array and then populate it's elements one by
one, either through a loop or declaring each one manually

You can also populate an array immediately when defining it by putting
the values between `{}`

```c
int numbers[10] = {0, 1, 2, 3, 4, 5, 6, 7, 8, 9};
```

### Create a dynamic array

You can create a dynamic array by using the [malloc](./mh5c.md) function
to create a contiguous block of memory that you can traverse
with array notation

```c
// Allocate memory to store 2 characters

int n = 2;
char *pvowels = (char *)malloc(n * sizeof(char));

pvowels[0] = 'A';
*(pvowels + 1) = 'I';

printf("%c", *(pvowels));
printf("%c", pvowels[1]);

free(pvowels);

printf("\n");
```

### Define a multidimensional array

You can define and implement multidimensional arrays in `c`, by using
the same notation

- For a two dimensional array:

```c
char vowels[1][5] = {{"a", "e", "i", "o", "u"}};
```

You can also omit the first value in a two dimensional array, since the
compiler will be smart enough two calculate that for you, but you do need to
specify all the other dimension lengths

> This is only possible when declaring an implementing an array at the same
> time, for just definition you need to provided the explicit lengths

- For a two dimensional array of 3 rows and 4 columns each:

```c
int numbers[][4] = {
  {0, 1, 2, 3},
  {4, 5, 6, 7},
  {8, 9, 10, 11}
};
```

This is more like syntactic sugar since under the hood it will still
be a one dimensional array, as when it's passed to a function it will
degrade to single pointer to the array type value

```
int numbers[3][4] = {
  {0, 1, 2, 3},
  {4, 5, 6, 7},
  {8, 9, 10, 11}
};

// The same as

int numbers[12] = {0, 1, 2, 3, 4, 5, 6, 7, 8, 9, 10, 11};
```

### Indexing into a one dimensional representation of a two dimensional array

There is a neet trick for indexing into a two dimensional array that
it's represented as a one dimensional array

If you know the width of each row (meaning how many elements are in a row)
then you can use that and multiply it by the index number row you want
to get to, and then off set it by the column you want to get to

```c
int numbers[3][4] = {
  {0, 1, 2, 3},
  {4, 5, 6, 7},
  {8, 9, 10, 11}
};

int row_width = 4;

// Get the value at cords (2, 2) starting offsets at 0
int value = numbers[2 * row_width * 2];

printf("The number is %d\n", value); // The number is 10
```
