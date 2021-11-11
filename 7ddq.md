# cli.git.rebase

Sometimes we don't want to have merge commits but instead a **clean linear branch**,
then we woudl use **rebase** instead of the **merge command**

## Synopsis

```sh
  git rebase <brach you are rebasing into> [<branch you are rebasing from> | <HEAD>]
```

## Options

- -i: Interactively rebase commits

## Cookbook

### Rebase branchA into branchB

When you rebase you put the **all the commits** from the branch you are merginng
from **infront of the branch you are merging into**

```sh
  git rebase branchA branchB
```

This will rebase branchB **infront of where branchA is pointing to**
