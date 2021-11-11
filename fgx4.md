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
- --continue: Continue with rebase process after fixing conflicts

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

First select the range to be rebased

```sh
  git rebase -i HEAD~2
```

Once in the interactive window given the following commits

```gitrebase
  pick 2e7e63e feat: add new (rename branch) recipe  to git.branch
  pick 414b875 feat: add options and new recipe to git.rebase.interactive
```

To re arrange the order of the commit you would just have to edit the file so
that the commits resemble the desired order

```gitrebase
  pick 414b875 feat: add options and new recipe to git.rebase.interactive
  pick 2e7e63e feat: add new (rename branch) recipe  to git.branch
```

### Split commits

There can be a case that you decide certain changes would be better if they
were committed separately. Here is how you can split a commit into multiple
parts

For this on the rebase window you will use the `edit` command on the commit you
want to split

```gitrebase
  pick 5749c6b refactor(git.reset): extract code comments
  edit 414b875 feat: add options and new recipe to git.rebase.interactive
  pick 2e7e63e feat: add new (rename branch) recipe  to git.branch
```

After that the rebase will stop at the commits that are marked with the `edit`
command. There you will [unstage all files](./z9bi.md) and **reorganized your
changes** into **separate commits**

```sh
  git reset head^
  git add <files-1>
  git commit [-m <separate-commit-1>]
  git add <files-2>
  git commit [-m <separate-commit-2>]
```

Finally **continue** with the **rebase** process

```sh
  git rebase --continue
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
