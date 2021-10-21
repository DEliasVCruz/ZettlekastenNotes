# cli.git.rebase.interactive

With the `--interactive` (`-i` for short), will open an editor with a **list of
the commits** which are about to be changed

## Overview

This list accepts `commands` allowing the user to **edit the list** before
initiating the rebase action

## Options

- pick; Use the commit in the rebase
- squash: Merge commits together with the original message intact
- fixup: Merge commits but remove the original commit message
- reword: Use the commit but modified it's message
- --continue: Continue with rebase process after fixing conlficts

## Synopsis

```sh
  git rebase --interactive <branch-to-rebase-to>
```

## Cookbook

### Reword past commit message

You can use [rebase](./7ddq.md) to [ammend past commits](./nr07.md) messages

When in the interactive window you give the `reword` command to the **commit
you want to change the commit message of**

To **reword one of the 4 past commits** relative to `HEAD`

```sh
  git rebase -i HEAD~4
```

### Reorder past commits

If you want to move around past commits so that they will be presented in a
different order in commit history. You can do it moving the commit lines in the
interactive rebase windows to the desired order

First select the the range to be rebased

```sh
  git rebase -i HEAD~2
```

Once in the interactive window given the following commits

```gitrebase
  2e7e63e feat: add new (rename branch) recipe  to git.branch
  414b875 feat: add options and new recipe to git.rebase.interactive
```

To re arrange the order of the commit you would just have to edit the file so
that the commits resemble the desired order

```gitrebase
  414b875 feat: add options and new recipe to git.rebase.interactive
  2e7e63e feat: add new (rename branch) recipe  to git.branch
```

### Rebase on to an upstream branch

You may want to rebase your work on top of an upstream branch `<origin/name>`.

```sh
git remote add [<remote-name>] <remote-url>
git fetch upstream
git checkout [<remote-name>] 
git rebase [<remote-name>]/master
git push --force origin feature
```
