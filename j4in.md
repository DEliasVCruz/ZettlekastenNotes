# cli.git.branch

You can create **branches** to move between different **versions** of your project.
They are **cheap to create and destroy**

## Synopsis

```sh
  git branch [flag-options] <branchname>
```

## Options

- -D: Delete an existing branch
- -v: See the last commit on each branch
- -m: Rename a branch
- --merged: List branches that are already merged into the current branch
- --no-merged: List branches that haven't been merged into the current branch
- -l: List only local branches
- -r: List or delete only remote branches
- -a: List both remote tracking branches and local ones

## Cookbook

### Create a new branch

You can use this command to **create** a **new non-existing** branch. This **wont
switch you into the new branch** it will just create it.

To start working on that new branch you'll first have to [switch to it](./it3j.md)

```sh
  git branch <newbranch>
```

### Delete a branch

To delete an existing branch

```sh
  git branch -D <branchname> [or multiple branches]
```

### Point branch to a new commit (movin branches around)

Once you create a new branch it will **point to your current head** to make it
**point to a different commit** you first have to [checkout the branch](./it3j.md):

And **while on that branch** you [reset](./z9bi.md) the branch to a **new commit**

```sh
  git checkout <branchname>
  git reset --hard <commitid>
```

After you reset your branch to a new commit. **All commits that come after this
version are effectively undone**

### Create a new branch with your [stashed](./z9bi.md) changes

```sh
  git stash branch <branchname> [<stash>]
```

### Delete a remote branch

```sh
  git push <remote> --delete <branchname>
```

### Rename a local branch

```sh
  git branch <branchname> -m <newname>
```

### Only clone an specified branch from a remote repo

To fetch a specific branch’s content. This command is useful to fetch the
required branch quickly

```sh
  git clone -b <branch name> --single-branch <remote>
```
