# web.css.color

Manipulate color of different elements with css

## Synopsis

```css
p {
  color: #ffffff;
  background-color: red;
}
```

## Cookbook

### Set colors with hex

You can use a [hex](./4gzy.md) to set the color, 
is a very common way and it uses one hex value for 
the `RGB` (and optionally `A`) value to set the `red`, 
`green` and `blue` values (also accepts `alpaha`)

In this case we have full red and nothing of the
other ones

```css
body {
  background-color: #ff0000; // red
  color: #ffffff; // white
}
```

You can use a short hand of just using 3 digits, and it
will be treated as if each one is repeated twice

```css
body {
  color: #abc; // equal to #aabbcc
}
```

### Set the color of text

You can set the color of text with the
`color` attribute

```css
p {
  color: red;
}
```

### Set the color of the background of an element

You can set the backgroudn color of an element
with the `background-color` element

```css
div {
  background-color: red;
}
```
