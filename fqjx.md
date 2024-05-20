# lang.py.syntax.print

Print messages to stdout

## Synopsis

```py
  print(*[message][, sep=][,end=])
```

## Overview

You can print to stdout in various ways

### Arguments

- `sep=`: Separator for argumets to build the string
- `end=`: End charactef for the sting
- `file=`: File object to redirect to
- `flush`: Avoid buffering of text until a new line character

## Definea custom separator and line end

You can use the `sep` and `end` arguments to **define** a **separator** for
your string and a **line end**. The **default** is `" "` and `\n`
**respectively**. But you can change it to any arbitrary sting

To **print different calls** to `print` in the **same line**, change the `end`
parameter to `''`

```py
  print('Mercury', 'Venus', 'Earth', sep=', ', end=', ')
  print('Mars', 'Jupiter', 'Saturn', sep=', ', end=', ')
  print('Uranus', 'Neptune', 'Pluto', sep=', ')

  # Mercury, Venus, Earth, Mars, Jupiter, Saturn, Uranus, Neptune, Pluto
```

### Redirect standard stream

There are **three** basic standard streams:

- **stdin**: Represented by `0`
- **stdout**: Represented by `1`
- **stderr**: Represneted by `2`

So to **write to a file** you pass a [file object](./7i8g.md) to the `file` parameter

```py
  with open('file.txt', mode='w') as file_object:
      print('hello world', file=file_object)
```

### Mock a file and redirect to memory

You can mock a file to **redirect** by writting **directly to memory** with the
[io]() module

```py
  import io

  fake_file = io.StringIO()
  print('hello world', file=fake_file)

  fake_file.getvalue()                      # 'hello world\n'
```

### Print text without buffering

By default `print` will only print text to the screen after a new line
character is encountered.

This is undesirable if you want to **print** non `\n` **text** to the screen
**sequentialy**. To a**void that** pass the `flsh=True` argument to forcefully flush
the stream without waiting for a newline character in the buffer

```py
  import time

  num_seconds = 3
  for countdown in reversed(range(num_seconds + 1)):
      if countdown > 0:
          print(countdown, end='...', flush=True)
          time.sleep(1)
      else:
          print('Go!')
```
