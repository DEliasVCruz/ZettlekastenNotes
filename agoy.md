---
tags: ["memory", "security", "system"]
---

# cpt.system.stack_canary

A stack memory corruption protection technique

## Overview

A stack canary is a memory corruption protection technique
most commonly used to protect against [buffer overflow](./b3a1.md) 
attacks

> Since most buffer overflow attacks target a portion of memory
> where the `return adress` of a function is stored

Its implemented by storing a **randomly chosen** `int` (`4 bytes`)
number that sits **between any number and the return address**

Since it sits right before the return address, when the function
is ready to `return` before we jump to the return address, the
`canary` is checked to make sure it's the same original value. If
it's **not the same** value then the **program will crash** and no
further code will be executed

This defends against a buffer overflow, since in order to 
overwrite the return address, it must also overwrite the 
canary. And since the attacker doesn't know the canary value
the computer will be alerted and crash

## Bypassing a stack canary

The main downside to this technique is that is relatively
straightforward to bypass:

- Using a `stack leak`, to get the value of the canary
  straight from the stack
- Guess the value

### Bypassing a stack canary by guessing the value

Depending on the system the value of the canary can be
a `32 bit` number, meaning between `0` and approx. `4` billion
and the value changes for each program run

But we could take advantage of the `forking` process of
some programs to get theoretically unlimited changes to
guess the canary value since `forked` child programs
use the **same** stack canary as the parent program

Since guessing the value directly can still be a huge
labor we can make use of a method that will reduce
are guessing work to **at most** `1024` guesses

We can take advantage of the fact that an `int` number
is represented by `4 bytes` of memory, so we can
instead try to guess the value of each individual byte
that can only be between `0` and `255` for each byte (`8` bits)

At each point we will only try to guess one `byte` at
a time, meaning that if we guess wrongly the program
will crash. But if we guess correctly it will work
normally since the rest of the bytes will remain
unchained

We repeat this process for every byte until we no longer
crash the programs after overwriting all `4` bytes

> Since each `byte` can only have `256` possible values
> and we only have to repeat this process `4` times, the
> total maximum number of guesses we could make is
> `1024` (`256 * 4`)
