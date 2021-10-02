# cli.run_commands

You can run various commands on your linux shell/terminal. Here you can find
how to execute commands on various ways

## Overview

Here `command` is **any program or process** that you run from your shell

## Cookbook

### How to run a program or process on the background

- While **still outputting messages** to the terminal

```sh
  command &
```

- **Without any messages**

```sh
  command > /dev/null 2>&1 &
```

### How to detach a background process from the current shell

With this you can **keep background processes running after a shell exits**

```sh
  disown [%<job#n>]
```

### How to list jobs running on the background

You can see a list of background programs **attached to the current shell**

```sh
  jobs -l
```

### How to bring a background process back to the foreground

When there is **multiple jobs** just add **% followed by the job number**

```sh
  fg [%<job#n>]
```

### How to terminate a background process

For that you may want to use `kill`
