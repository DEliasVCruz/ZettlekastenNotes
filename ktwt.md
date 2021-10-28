# cli.git.branch.orphan

An orphan branch has no parents (meaning, git history) when it is created. The
history of the orphan branch is separate from other branches in the repository

## Overview

Creating an orphan branch is very similar to [creating a branch](./j4in.md)
through the [create and switch](./it3j.md) to a new branch method but this new
branch will not share any of the commit history the main or any other branch it
was created from

### Use case

It might be useful if you want to have a branch that you will not need to keep
in sync with the rest of the changes in your repo

## Synopsis

```sh
  git checkout --orphan <branch-name>
```

## Cookbook

### Delete all past commits and start a new history

If you want to start fresh

```sh
git checkout --orphan <new-branch>
git add .
git commit -m ["<new-first-commit>"]
git branch -D <main-branch>
git branch -m main # Rename new branch to main
git push -f origin main # Rewrite history!!
```
