---
tags: ["syntax", "web", "semantic_html"]
---

# lang.html.global_attributes.lang

Define the language of an elment

## Synopsis

```html
<p lang="es-ES">Hola mundo!</p
```

## Overview

The `lang` global attribute helps in defining the language
of an `element` as in: 
  - The language that **non editable** elements are written in
  - Or the language that the editable elements should be written on

## Cookbook

### Set the general language of your whole application

The `lang` element is **inherited** from the parent element when
it's not explicitly defined

Therefore you can set a `lang` attribute at the top of your
html document element for it to be inherited as the deafult
`lang` attribute for all elements

> For accessability reasons parts that are in another language
> should have the language of those parts specified too with
> their own `lang` attribute

```html
<!DOCTYPE html>
<html lang="en">
  <body>
    <p>Some default text</p>
    <p lang="es">Pero esto es en otro idioma</p
  </body>
</html>
```

## Sources

- The `mdn` [reference](https://developer.mozilla.org/en-US/docs/Web/HTML/Global_attributes/lang)
