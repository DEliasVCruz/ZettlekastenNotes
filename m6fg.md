# lang.js.array

Creating an manipulating arrays in `javascript`

## Synopsis

```js
const myArr = [];
```

## Overview

## Cookbook

### Iterate over an array

There are multiple ways to iterate over an array in
javascript here are some common ones and use cases

#### The standard for loop

Prior to `ES2015+` this was the only way to iterate
over and array using a classic `c` style loop

```js
const myArr = [1, 2, 3];

for (let i = 0; i < myArr.length; i++) {
  console.log(`The ${i} element is: ${myArr[i]}`)
}
```

#### Using the `for-of` loop syntax

Now we can use the `for...of` loop syntax to iterate
over the **just** the elements of an array with a 
simpler syntax

```js
const myArr = [1, 2, 3];

for (const num of myArr) {
  console.log(`The element is: ${num}`)
}
```

### Iterate over an array elements and index

Using the traditional methods of looping over an array
you can't have access to the `index` and `element` of the
array at the same time

But you can use the `.entries()` method of the array
object to achive this behaviour

- Keep in mind that:

  What `entries` returns is not actually a `[number, any][]`
  array, but rather an [iterator](./8nxp.md), that means
  that it will call `interator.next()` under the hood until
  the iterator is depleated, so the return value can only
  be iterated over once

  If you wish to get the actual `[number, any][]` array
  to store in a variable and use multiple times you will
  have to turn the iterator into an array

```js
const myArray = ['a', 'b', 'c'];

for (const [idx, elem] of myArray.entries()) {
  console.log(`The ${idx} element is: ${elem}`)
}
```

Yet another way that we can achieve our goal is using the
`.forEach` method of the array object, if you prefer taking
a more functional style

```js
const myArray = ['a', 'b', 'c'];

myArray.forEach((elem, idx) => {
  console.log(`The ${idx} element is: ${elem}`)
})
```

### Create an array from an iterator

You can convert an iterator to a traditional javascript array
by using the `Array.from()` object method or by using the
`spread` operator to unpack it's values into a new array

```js
const myArray = ['a', 'b', 'c'];
const myArrayFrom = Array.from(myArray.entries()) // [[1, 'a'], [2, 'b'], [3, 'c']]
// or
const mySpreadArray = [...myArray.entries()] // [[1, 'a'], [2, 'b'], [3, 'c']]
```

### Reverse an array without mutating it

When reversing an array you would topically think of
using the `.reverse()` method of the array object, however
this will perform an **in place** reversing of the array
and in essence mutate the original array

```js
const myArr = [1, 2, 3];
console.log(myArr); // [1, 2, 3]

myArr.reverse();
console.log(myArr); // [3, 2, 1]
```

If you want however to reverse an array without modifying the
original one you have several options

#### Combining `.slice` and `.reverse`

You can use the `.slice()` method of the array object to first
return a new array and then use `.reverse()` on that new array

> Since `slice` is being called without arguments it will
> return a copy of the whole array

```js
const myArr = [1, 2, 3];
console.log(myArr); // [1, 2, 3]

const reversed = myArr.slice().reverse();

console.log(reversed); // [3, 2, 1]
console.log(myArr); // [1, 2, 3]
```

#### Using the spread operator and `reverse`

Since `ES6+` we can use the `spread` (`...`) operator to clone the
array by unpacking it's elements into a new array and the calling
`reverse` on the new one

> Using the `spread` operator might be more concise but also
> slightly less performant than other options

```js
const myArr = [1, 2, 3];
console.log(myArr); // [1, 2, 3]

const reveresed = [...myArr].reverse()

console.log(reversed); // [3, 2, 1]
console.log(myArr); // [1, 2, 3]
```

#### With a reverse for loop

We can also use a standard for loop to create a new array
by traversing the original one in reverese

```js
const myArr = [1, 2, 3];
const reversed = [];

for (let i = myArr.length - 1; i >= 0; i--) {
  reversed.push(myArr);
}

console.log(reversed); // [3, 2, 1]
console.log(myArr); // [1, 2, 3]
```
