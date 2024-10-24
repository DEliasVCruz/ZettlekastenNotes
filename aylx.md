# lang.css.selectors.pseudoclass.focus



## Synopsis

```css
button:focus {
  ...
}
```

## Overview

### Variants

- `:focus-visible`: Only apply when the users focus on an element using the keyboard
- `:focus-within`: 

## Cookbook

### Only apply focus style only when the user navigates with keyboard

The default mode of `:focus` applies a style when the user clicks or
navigates with it's keyboard to an element

This might not be desirable, since you may not want the style applied
when the user clicks on an element but do want it when it navigates
with their keyboard (like tabbing)

For that you can use the `:focus-visible` variant

```html
<!-- This shows outlined when clicked -->
<button class="focus">Focus</button>
<!-- This does not show outline when clicked only when tabed -->
<button class="focus-visible">Focus visible</button>

<style>
button {
  font-size: 200%;
  outline-offset: 5px;

  & .focus:focus {
    outline: 5px solid Highlight;
  }

  & .focus-visible:focus-visible {
    outline: 5px solid Highlight;
  }
}
</style>
```
