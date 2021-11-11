# cli.tr

Replace or delete characters

## Synopsis

```bash
  tr [options] "<searched_character>" "<replacement>"
```

## Overview

You can use `tr` kinda like [sed](./i6f5.md) to replace characters in a string. Is
**better used** for simple **special character** replacement

## Cookbook

### Replace new lines for spaces

If you wanted to make all **new line** separated strings into one **space
separated** string

```bash
  echo fiel_with_new_lines.txt | tr "\n" " "
```
