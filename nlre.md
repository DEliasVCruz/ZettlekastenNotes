# cli.base64

Encode and decode text from and to `base64` encoding

## Synopsis

```sh
base64 [options] [<file>]
```

## Overview

You can use this command to encode or decode files into and from
`base64` encoding, you can also use it along the pipe operator
to use it on text without require a file

- The default behavior of the command is to `enconde` data
- This is part of the **GNU core utils** 

### Options

- `-d`: Decode data
- `-i`: When decoding, ignore non-alphabet characters

## Cookbook

### Encode/Decode base64 text from a piped command

The command accepts processing data piped from the result of another
command

- This is the only way to use the command without passing a file

```sh
echo "hello world" | base64
# aGVsbG8gd29ybGQK

echo "aGVsbG8gd29ybGQK" | base64 -d
# hello world

base64 "hello world"
# base64: 'hello world': No such file or directory
```

### Decode the contents of a bas64 encoded file

This will print out the contents of the file after being
decoded as a `base64` encoded file

- This will not modify the contents of the file in place

```sh
base64 -d file.txt
# hellow world

cat file.txt
# aGVsbG8gd29ybGQK
```
