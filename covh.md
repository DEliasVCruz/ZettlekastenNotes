# cli.doas

A drop in replacement for sudo

## Synopsis

```sh
  doas <program>
```

## Overview

This is a substitute to the `sudo` command, that can do all that a general user
would need without the complex permission managment

## Cookbook

### Install doas in your system

### Configure doas for use

You need to create and edit the file in `/etc/doas.conf`. This allows that any
member of the `wheel` group can run `doas` to run something as a different user

```conf
  -- /etc/doas.conf

  permit :wheel
```

Then you need to change the file permission so as **only** the **root**
[user](./fa42.md) can actually read it

```sh
  sudo chown -c 0400 /etc/doas.conf
```

### Don't require password every time

By default you would have to enter the password every time you use the command,
but you can configure it so once you use the password it won't ask you for it
again until after some time

- Just add this to the `/etc/doas.conf` file

```conf
  -- /etc/doas.conf

  permit persist :wheel
```

### Add permitions

You can add different permissions with the `permit` command the **basic
structure goes as**

```conf
  -- /etc/doas.conf

  permit <permission> [<group>] [as <user>] [cmd <command> [args <command-arguments]]
```

### Do not ask for a password when using an specific command

**In this example** we permit not having to enter a password when using the
`pacman -Syu` command as `root` user for every member of the `:wheel` group

```sh
  permit nopass :wheel as root cmd pacman args -Syu
```

### Emulate a doasedit command

By default there is no equivalent `sudoedit` command for doas, but you can use
the following sript to emulate it

- From this [source](https://github.com/AN3223/scripts/blob/master/doasedit)
