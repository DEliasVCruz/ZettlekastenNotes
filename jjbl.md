# cli.git.merge.conflict

When merging branches and commits sometimes some lines will have **conflicting
information**. Then you have to **manually decide wich part you want**.

## Overview

When merging branches you have to first the branch you want to merge from and
then provide the branch you want to merge into

## Options

- --abort: Discard all changes and start over from the merge process

## Synopsis

```sh
  git merge <branch you  are mering from> [<branch you are merging into>]
```

## Cookbook

### Structure of a merge conflict

To **end the merge conflict** you have to delete the parts in **<>** and
**replace it** with what you want instead

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

### Restart the merging process

If you want to discard any changes made in the merge process and start the
merge from scratch

```sh
git merge --abort && git merge <branch>
```

### Discard only some conflicting files

To abort the merge process only on some particular conflicting files use
[checkout](./it3j.md) on the file, which extracts the file and all the conflict
marker from the git index to it's base form

```sh
git checkout --conflict=diff3 <file-name>
```

### View each version of the merged file

A copy of each version of the merge file is kept during the merging process
(local, base, remote) to view each version in the command line you can use the
[cat-file]() command

To refer to each version append this to the `<file-name>` respectively

- `:1:` = base version
- `:2:` = local
- `:3:` = remote

```sh
# View the base hunk
git cat-file -p :1:<file-name> | tail -n 188 | head -n 7
```
