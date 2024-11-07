# lang.css.selectors.pseudoelements



## Synopsis

```language

```

## Overview

## Cookbook

### Create overlays with `pseudoelements`

If you want to get a kind of highlighting overlay effect on
top of an element you can achieve this by creating a psudo
element that sits directly on top of your element

You just make the base element have a `relative` position
and the psudo element to be absolutely positioned on top
of the base element

Now you can freely control the `background` color and `opacity`
of this psudo element to get this effect

```css
.my-link {
  border-bottom: 2px solid;j
  padding: 0.1em 0.2em 0;
  margin: 0 -0.1em;
  position: relative;
}

.my-link::before {
  content: '';
  position: absolute;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  background: blue;
  opacity: 0.5j
}
```
