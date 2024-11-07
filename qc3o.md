# lang.css.inheritance

How defaults and inheritance works in `css`

## Synopsis

```css
{
  margin: initial;
  padding: inherit;
  border: 1px solid currentColor;
}
```

## Overview

You can use the `currentColor` value for setting an elements 
color to the inherited or base color of the defined element 
or it's parent

When `css` is loaded the `defaults` are actually the `user agent 
styles` that get automatically injected and defined by the
browser

The true default of `css` are actually the `inital` values
which mostly are `none` or `0`, you can explicitly set/reset
styles to their initial value by given them `initial`

At the same time some `property` values can be inherited
due to the cascading nature of `css` but not all are
`inherited` and you can manually define them as so or
make it explicit by passing `inherit` as their value

> Things like `margins` are not inherited

In most cases `currentColor` works as `inherit` since it
give the color to the one define by it's parent or to
the `initial` value of the `color` property in case they
are not inherited

## Cookbook

### Given a `currentColor` to a border

The color of a border is not defined since their
is no sensible default for this, so it's usually set
to whatever is the `color` property of the element

This happens automatically or you can set it explicitly
with either the `initial` or `currentColor` value

```css
.inital-based {
  border-color: initial;
  color: white;
}

.current-color-based {
  border: 1px solid currentColor;
  color: red;
}
```

### Blend multiple backgrounds in a gradient

You can create overlapping backgrounds by either setting
up one after the other (in a stacking manner) in the
`background-color` property or, if you just need two
layers, then you can set one up in the `background-color`
and another in the `background-image`

> You can set a semi transparent black with an `hsl`
> that defines a `hue` of `0`, a `saturation` of `100%`
> a `luminoscity` of `0%` and the desired alpha
> transparency of `0.5`

```css
body {
  background-color: currentColor;
  background-image: radial-gradient(
      transparent, -- transparent center color
      hsla(0, 100%, 0%, 0.5) -- semi transparent black
  )
  color: red
}

.compact {
  background-image: currentColor radial-gradient(
      transparent, -- transparent center color
      hsla(0, 100%, 0%, 0.5) -- semi transparent black
  )
  color: red
}
```

## Sources

- A [video](https://www.youtube.com/watch?v=krbKkLPXwlQ) on using `currentColor`
