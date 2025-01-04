# cli.mkfifo

Create `FIFOs` (named pipes)

## Synopsis

```sh
mkfifo [<options>] <pipe-name>
```

## Overview

This allows you to create named pipes that you could use
as intercommunication device between processes

This pipes are **one way communication** devices, there is
a listener and a producer. The producer sends messages and 
a listener can receive the message

Only one consumer can read the message at a time, once a 
consumer has read the message other consumers will not be 
able to listen to them

## Cookbook

### Create a name pipe and send messages

Once you create a named pipe you can send messages to the
pipe and anyone listening to it can then read the message

In one terminal you can type

```sh
mkfifo my_pipe
echo "hello world" > my_pipe
```

And in another read the message

```sh
cat < my_pipe
# hello world
```

> Since in essence this is just a file, you have to provide
> the exact path to the named pipe to use it
