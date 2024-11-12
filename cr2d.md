---
tags: ["web", "fonts", "typography"]
---

# lang.css.fonts.font_face

Define custom font families to use in the browser

## Synopsis

```css
@font-face {
  font-family: <font-name>;
  src: url(<font-url>) format("<format-name>")[, <src>];
  font-weight: <weight>;
  font-style: <style>;
}
```

## Overview

If you don't want to be using the default `system fonts`
and you don't want to download fonts directly with `js`
you can do so by defining them with `css`

This is useful since it will naturally choose different
formats based on the browser capabilities

Since the default load behavior of this might not be
consistent across browser you might want to use different
[strategies](./x7zj.md) to load fonts

> The key value pairs inside the `font-face` block are
> called `descriptors` as for example `font-weight`

## Cookbook

### Define a custom font face to be used

You can define different fonts to be used in the browser
directly with `css` by using the `@font-face` at-rule

> You can define more than one format `src` and it will
> choose the correct one based on the browser capabilities

You can then use this fonts directly in your normal `css`
classes

> The download of the font is done once the declare font is
> used, not by the `@font-face` at-rule

```css
@font-face {
  font-family: HKGrotesk;
  src: url(/fonts/HKGrotesk-Light.woff2) format("woff2"),
       url(/fonts/HKGrotesk-Light.woff) format("woff");
  font-weight: 300;
  font-style: normal;
}

@font-face {
  font-family: CormorantGaromond;
  src: url(/fonts/CormorantGaromond-Light.woff2) format("woff2"),
       url(/fonts/CormorantGaromond-Light.woff) format("woff");
  font-weight: 400;
  font-style: normal;
}

h1 {
  font-family: HKGrotesk, sans-serif;
  font-weight: 300;
}

p {
  font-family: CormorantGaromond, serif;
  font-weight: 400;
}
```

### Control how the browser performs font synthesis

When a `font-face` does not define an specific `descriptor`
that can specify a required `font property` in your `css`
the browser will try it's best to match it by taking
from wherever it can find a definition that satisfies
this

Take for example a `font-face` that defines a bold weight
of `500` but you have an `element` that has a `class` that
specifies a `700` weight

By default The browser will take from wherever it can to
satisfy this requirement

You can control this behavior by using the `font-synthesis`
property, this can let you define whether or not the browser
should synthesize:
  - bold
  - italic
  - small-caps
  - subscript/superscript typefaces

```css
body {
  font-synthesis: none; /* do not perform any font synthesis */j
}

p {
  font-synthesis: style weight /* only synthesize on style and weights */
}
```

### Set a range of characters to be used from the font

When doing `font subsetting` you can get greater results by
defining the `unicode-range` descriptor on your `@font-face`
block to control what specific `unicode` character ranges
to use from your font family

In this case if the page does not use any character in this
range the font is not downloaded

> This a great way of subsetting system fonts

```css
@font-face {
  font-family: "Ampersand";
  src: local("Times New Roman");
  unicode-range: U+26;
}

div {
  font-size: 4em;
  font-family: Ampersand, Helvetica, sans-serif;
}
```

## Sources

- You can read more on the [font-face rule](https://developer.mozilla.org/en-US/docs/Web/CSS/@font-face) 
  from the `mdn` documentation
- A guide on how to [subsett](https://jakearchibald.com/2014/minimising-font-downloads/) fonts with the
  browser tools
