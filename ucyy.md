# cpt.system.data_execution_protection

Memory policy to mark areas as either writable or executable

## Overview

Also known as:
  - `DEP` for short
  - Executable space protection
  - `Nx` bit

In a typical memory space address, meaning the 
portion of memory assigned to a program to be able 
to work in, we will have two sections

- The `code` section that it's **read only** and **executable** 
  and contains the code that will be run

- The `stack` section that is **writable** but not **executable** 
  and will contain data used by the program

> This is define as the `write xor execute` policy or as
> `w^x` for short, and is supported at a hardware level

It solves the common [buffer overflow](./b3a1.md) vulnerability
where an attacker over writes a **return address** to
point back to the buffer where now custom code will
live and be executed. But now will not be able to be
executed

However there might still be portions of memory that
might need to be both writable and executable such
as in the case of `jit compilers` that produce code
on the fly and need to store and execute the newly
produce code
