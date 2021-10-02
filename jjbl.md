# cli.git.merge.conflict

When merging branches and commits sometimes some lines will have **conflicting
information**. Then you have to **manually decide wich part you want**.

## Synopsis

```sh
  git merge <branch you  are mering from> [<branch you are merging into>]
```

## Cookbook

### Structure of a merge conflict

To **end the merge conflict** you have to delete the parts in **<>** and **replace it**
with what you want instead

```git
  <<<<<<< HEAD (The branch you are currently)
  What you have on your branch
  =======
  What is on the same lines but in different branches
  \>>>>>>> <branch you are merging from name>
```

### Resolving a merge conflict

After you've finished making your changes you have to **stage the files that
have been resolved and commit them**

```sh
  git add . && git commit
```
