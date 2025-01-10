# cpt.data.graph.binary_tree

The traditional tree like dynamic graph structure

## Overview

A binary tree is a special case of a [k-ary tree](https://en.wikipedia.org/wiki/M-ary_tree) 
where `k` is `2`, therefor it constitutes a `graph` data structure
in which each `node` has **at most** `2` children

They are primarily used to implement:
   - Binary search trees
   - Binary heaps

Common operations include `insertion`, `deletion` and 
`traversal` (ex. search). This operation range in difficulty depending
on if the tree is **balanced** or the `nodes` to operate on are `leaf`
or `branch` nodes

A binary tree is considered to be `balanced` if the **depth** of the left
and right **subtree** of every node differs by **at most** `1`

Having a `balanced` tree allows for a predictable `depth` also now as
the tree `height`. This is the measure of node from `root` to `leaf`,
where the **height** of the `root` is `0` and subsequent `nodes` are
(1, 2,..n) respectively

> The `height` of a balanced tree can be expressed as `log2(n)` where
> `n` is the number of `nodes` in the tree (without counting the
> `root` node)

### Searching a binary tree

Searching (traversing) a binary tree can be done in one of two ways:

- **Depth-first-search** (`DFS`): where one starts at the `root` node 
  and goes as far as possible on each branch before backtracking

- **Breath-first search** (`BFS`) where one first searches each node 
  on the current level before moving to the next one

## Cookbook

### Searching a binary tree by depth-first search (`DFS`)

### Searching a binary tree by breath-first search (`BFS`)

### Turning a linked list into a binary tree
