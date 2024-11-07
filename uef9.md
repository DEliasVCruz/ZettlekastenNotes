# lang.css.box_shadow



## Synopsis

```language

```

## Overview

## Cookbook

### Reduce the strength and size of a boxshadow

You may find that applying a normal shadow, may
cast too strong of a radius around your element

If you wanted it to be more subtle you can create 
a negative spread radius on a `box shadow` by adding 
this (`-1px`) to it's definition

This means that the `blur` now start from underneath
the element, and this has the effect of giving us
a more subtle shadow

```css
div {
  box-shadow: 0 2px 4px -1px red;
  transition: box-shadow 0.2s;
}
```
