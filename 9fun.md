# lang.css.fonts.system_fonts

Use the native platform UI fonts for your website

## Synopsis

```css
body {
  font-family: -apple-system, BlinkMacSystemFont, "Segoe UI"
}
```

## Overview

You can take advantage of using the system predefined UI fonts
for your web app, they come with the advantage that they'll be
pre-installed

It great if you wan't to give your app a kinda `native` look,
though it's recommended to be used mainly for interaction text
rather than long form content

## Cookbook

### Set a font family that works with most major system ui fonts

Here is how you can orginaze your `font-family` so that it works
with most system UIs

> Keep in mind that this change over time and this may 
> need to be updated

1. The first section targets `apple` systems and `chrome` on `Mac OS X`
2. The second section is for knonw system UI fonts, like for windows,
   android, ubuntu, etc.
3. Finally in the thrid grouping are the fallback fonts

```css
font-family:
  /* 1 */ -apple-system, BlinkMacSystemFont,
  /* 2 */ "Segoe UI", "Robot", "Oxygen", "Ubuntu", "Cantarell", "Fira Sans",
  "Droid Sans",
  /* 3 */ "Helvetica Neue", sans-serif;
```

## Sources

- An old [article](https://www.smashingmagazine.com/2015/11/using-system-ui-fonts-practical-guide/) on how to use system UI fonts
  - It also goes on some details on the common pitfals
