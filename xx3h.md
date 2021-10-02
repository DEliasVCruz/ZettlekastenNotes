# cli.git.bisect

Find where you last saw a particular entry on your commit history. Or to **find
which commit introduced a bug**.

## Synopsis

```sh
  git bisect [start|bad|good]
```

## Coockbook

### How to find the last commit where you had something that you no longer have

Sometimes you may have something like a function that you deleted many commits
ago, and now for some reson you **want to recover** that function but you
**don't remember where was the last commit in which you had it**.

```sh
# Begin the bisect command
  git bisect start
```

Use **bisect bad** on a commit where you don't have what you are looking for.
And then use **bisect good** on a commit where you have what you are looking
for. After your first round git will **automatically point to a commit in
between**. After this **repeat this** until your **HEAD** points to a commit
that has what your looking for.

```sh
  git bisect bad
  git bisect good
```
