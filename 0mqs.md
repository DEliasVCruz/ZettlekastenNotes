# cli.git.attributes



## Synopsis

```language

```

## Overview

## Cookbook

### Avoid errors of line endings between `Unix` and `Windows`

In windows the end of line indicator it's `\r\n` while
on `Linux` and other `Unix` like systems the end of line 
indicator it's `\n`

This will create problems in your project if it's not
handled correctly

Add this configuration to your project to avoid this
problem for good in any circumstance

```.giattributes
* text=auto
```
