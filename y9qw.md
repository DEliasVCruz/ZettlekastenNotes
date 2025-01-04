---
tags: ["memory", "system", "errors"]
---

# cpt.system.segmentation_fault

When a program attempts to access unreachable memory

## Overview

This is a common error when working with [c](./xl2p.md) programs

This error happens when a programs tries to access memory
that it doesn't have access to, hence the name of the error
`segmentation` for memory segmentation violation

This can happen when dereferencing a [freed](./mh5c.md), invalid 
or `null` pointer, but can also be caused by [stack overflows](./klxm.md) 

When this happens the system [signal](./ywfv.md) `SIGSEGV` (for
Signal Segmentation Violation) is sent to the offending
process and causing it to terminate
