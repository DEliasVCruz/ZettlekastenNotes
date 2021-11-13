# cli.git.merge

When you have more than one branch that you want to **unite** then you can
peroforme a merge.

## Overview

Remember that the merging always happens as **merging the commit into your branch**

## Synopsis

```sh
  git merge <merged-branch> [<branch-to-merge-into> | default = <currenthead>]
```

## Options

- --no-ff: Always create a new commit object, avoid fast-forward

## Cookbook

### Merge a branch into your currently checked branch (Head)

- When you want to merge a branch into the branch you are currently on.
- You can also **merge multiple branches into your own at the same time**
- This **will always merge your branch alongside the others**

```sh
  git merge <branchid> [<ohterbranches>]
```

### Merge a remote branch into your local one

When working with [remotes](./95us.md) the **remote branch** your
[branch](./j4in.md) tracks, **may be some commits ahead**

You must first [review](./m36a.md) what **commits** may have been **aded**

```sh
  git log --oneline <branch>..origin/<branch>
```

Then **approve the changes and merge them** into your local main branch

```sh
  git checkout <branch>
  git log origin/<branch>
  git merge origin/<branch>
```
