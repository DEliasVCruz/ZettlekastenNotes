# lang.html.element.link

Represents information for external resources

## Synopsis

```html
<link 
  rel="alternate" 
  href="https://example.com/fr/html" 
  hreflang="fr"
  type="text/html"
  title="French HTML" />
```

## Overview

## Properties

### `hrreflang`

Is used to indicate the language and geographical targeting
of a page. This can be used by browsers to select the more 
appropiate page

### `rel`

It indicates the relationship between the resource represented
by the `link` element and the current document

The most common use case is for specifying a link to an external
style sheet with `stylesheet`

## Cookbook

### Specifying different version of your app for different languages

When you have an app that can work in multiple languages, is common
practice to put the different versions under different paths perfixed
by the language like `https://mysite.com/es/home`

You can help the browser know which version to get based on the most
suitable language for the user by specifying this different versions
as `link` elements with the `hreflang` property based on it's language

For `SEO` purposes you can use it in conjuction with the `rel` property 
set to either the value of:
  - `canonical`: To indicate web crawlers that the given `URL` is
    the master copy of a page (it's most representative version)
  - `alternative`: To indicate to serach engines that there is 
    another `URL` with the same content but in different form

> It's good practice to also specify a fallback `link` for the `x-default`
> language that will match any language that has not been defined

```html
<head>
  <link rel="canonical" hreflang="en" href="https://mywebsite.com"/>
  <link rel="alternative" hreflang="es" href="https://mywebsite.com/es"/>
  <link rel="alternative" hreflang="fr" href="https://mywebsite.com/fr"/>
  <link rel="alternative" hreflang="x-default" href="https://mywebsite.com"/>
</head>
```

## Sources

- The `mdn` [reference](https://developer.mozilla.org/en-US/docs/Web/API/HTMLLinkElement) for the `HTMLLinkElement`
- An [article](https://simplelocalize.io/blog/posts/what-is-hreflang/) on how to properly use the `hreflang` tag
