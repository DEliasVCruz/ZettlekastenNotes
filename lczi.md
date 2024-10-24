---
aliases: ["JavaScript Memory Leaks and How To Fix Them"]
tags: ["memory", "js", "performance"]
---

# cpt.js.memory_leaks

## Overview

## Symptoms

There are many consequences that come from unhanded memory leaks

1. Page unresponsive: 
  - Like when the browser tells you that the page is unresponsive
    and you either have to wait or manually restart/quit

2. When your browser gets slow and you can't switch tabs anymore

3. You `OS` (computer) gets slow because your browser begins to eat more `RAM`

## What is memory in `javascript`

Whenever you declare a new variable or object, it's allocated either to the
`stack` or to the `heap`. So now you get a reference to the value in memory
of your allocated resources

```js
const x = 10;
```

Problems start to arise when a value that is no longer being used or referenced
is not clear from memory and leaves there occupying space without serving any
porpoise for the application

## What is `GC` in `javascript`

Garbage collection in `javascript` happens automatically and it consist
of 3 steps

1. Find the root node in your code and recursively go through every child
  - The root node in the browser is the `window` object
  - In `nodejs` is the `global` variable

2. Mark every child including the `root` as `active` or `inactive`
  - `active`: Means this part of code is referenced in the memory
  - `inactive`: Means that it's not referenced from anywhere

3. Delete all `inactive` references from the memory

## When can a memory leak happen

Memory leaks happen when the `GC` fails to mark an `inactive` node as such
and does not deleted

1. When you have `global` variables

This variables are always gonna stay on the root, since it's accessing, and thus
the `GC` will never delete them

```js
"use strict"

window.x = 10
window.calc = function() => {}
```

You can prevent this by either:
  - Not ever using `global` variables
  - Setting the `"use strict"` directive, since it will throw errors as soon
    as you have `global` variables

2. When you have `setTimeout` or `setInterval`

If you use one of this functions and the callback function has dependencies
and the timeout is not cleared after being used

The callback is going to keep the reference to an object even after set object
might have been already deleted

A mitigation for this is to always `clear` your `timeouts`, that way when the
timeout is cleared, all the references inside it are also gonna be garbage
collected

```js
const myTimeout = setTimeout(() => {
  let node = document.getElementById('node')
}, 1000)

node.remove()

clearTimeout(myTimeout)
```

## When you keep a reference to a deleted object

Consider the case where you keep a reference to an object (ex an `html` node) 
in a `map`, even if you then delete the object you where referencing it wont
be garbage collected if you do not delete it's reference from the map

```js
const nodes = {
  btn: document.getElementById('btn')
}

# This will not be enough to trigger garbage collection
document.getElementById('btn').revome();

# This is necesary to ensure GC
delete nodes.btn
```
