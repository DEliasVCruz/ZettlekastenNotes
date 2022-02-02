# cli.py.debug.pdb.stack

Inspect the frames of the current call stack

## Synopsis

```pdb
  (Pdb) w
```

## Overview

The **call stack** is the current **set of** callable **functions** that are
**waiting to be executed** in order

You can inspect this call stack and see **which function called which** and in **what
order**

## Cookbook

### Print the current call stack state

You can use the `w` command to print the current state of the call stack.

The **call stack** is **represented** from the **most recent call** at the
**bottom** and goes back in time up. The first two lines show the current stop
point. Therefore the **third line is the most recent caller**

```pdb
  (Pdb) w                     # Print the current call stack state
```

### Move along the call stack

You can move along the history of the call stack with:

- `u`: Move up to the **previous call**
- `d`: Move down to the **next most recent call**

They both accept a `<count>` to move **count times** up or down

```pdb
  (Pdb) u 2                 # Move up two frames in the call stack
  (Pdb) b 2                 # Move back down two frames in the call stack
```
