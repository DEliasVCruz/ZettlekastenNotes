---
aliases: ["How to work with fonts in the web"]
tags: ["performance", "web", "fonts", "typography"]
---

# cpt.web.fonts

Working with fonts in the web

## Overview

When working with `web fonts` it's important to remember
this things:

- Each different weight and variant of the `typeface` 
   is represented by it's own file

  Therefore we need to be very careful with how many
  fonts are we bundleling with our application

- Those many files can be large

  Therefore they may take a **long time** to load and
  may even fail to download

- Highly disruptive in case of failure

  If font loading goes wrong it can completely undermine
  the purpose of your site

That is why without a **fallback** `web fonts` can be
incredibly disruptive when they fail

### Web Font Fallback

We can achieve fault tolerance by adding an adequate
fallback font

To **responsibly work with web fonts** we require two
steps

- **Reliably loading fonts**: This means we are loading the
  fonts in a consistent way that grantees we show the fallback

- Tuning the fallback font: This means making that fallback
  font look as similar to the eventual font as possible

You can load web fonts using the [@font-face](./cr2d.md) at-rule
on your `css` but keep in mind that if you use fallback 
fonts along side them then the default behavior of this 
is not great across browsers, so you might still want to 
load fonts with a custom loader in `js`

- On `Edge` the fallback font will be show immediately
- On other browser they might show a blank screen for up
  to `3s` waiting for the web font to respond before
  showing the default font
- Mobile browser might just wait as long as the webfont
  takes and never show the default

> This is called Flash Of Invisible Text (`FOIT`) and
> it's our enemy since it blocks page rendering

To mitigate this you can use 2 strategies:
  - Using `@font-face` + **custom loader** 
  - Load fonts files manually with `js`
    - The packages you install with `google-fonts` do
      this on your behalves

#### Custom Font Loading

If you give full control to the browser on how to load
your fonts it might do it in a very choppy way, if you
want full control on how the fonts are loaded there are 
many possible techniques

By default font faces are dormant, waiting for something
to trigger their download

You can take advantage of this to apply fonts only when
they are ready and load them your self before hand

So you can use js to load the fonts and then apply the
class where the font is used dynamically to your elements
after they are fully loaded

> In this method you have to specify before hand each
> variant that you want to be loaded

- We can use the `fontfaceobserver.js"` library to load
  fonts our selves

```js
// We name this file `loadFonts.js`

const typefaces = {
  HKGrotesk: [
    {weight: 300, style: 'italic'}
    {weight: 300, style: 'normal'}
    {weight: 500, style: 'italic'}
    {weight: 500, style: 'normal'}
  ],
  CormorantGaromond: [
    {weight: 400, style: 'normal'}
    {weight: 700, style: 'normal'}
  ]
}

Object.keys(typefaces).forEach((name) => {
  const variables = typefaces[name].map((variant) => {
    const loader = new FontFaceObserver(name, variant)
    return loader.load() // This is a promise
  })

  Promise.all(variants /* array of promises */).then(() => {
    /*
      Add the name of the font face as a class name at the
      root `html` element
    */
    document.documentElement.classList.add(name)
  })
})
```

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

.HKGrotesk .sans-serif {
  font-family: HKGrotesk, sans-serif;
}

.CormorantGaromond .serif {
  font-family: CormorantGaromond, serif;
}
```

```html
<html ..>
  <head></head>
  <body>
    ...
    <script src="/fontfaceobserver.js"></script>
    <script src="/loadFonts.js"></script>
  </body>
</html>
```

### Tuning The Font Fallback

If you are using a fallback font to display while you
wait for your web font to load it can look very yanki
the transition from one font to another

That's why it's good to **tune** your fallback font to
look as similar as possible to the web font of your
choosing and minimize the visual impact of the transition

You can use pages like:
  - [moder font stacks](https://modernfontstacks.com/) 
  - [css font stacks](https://www.cssfontstack.com/) 

This pages will help you compare different **system fonts** 
based on their usage across operating systems and choose
the best fallback font for your use case

Then the next step is to use [font style matcher](https://meowni.ca/font-style-matcher/) 
to adjust the `css` properties of your default font
until it most closely matches the look of your web font

We want to use this tool just to find the relation between
this fonts to use in our `css`

One way to apply this different rules might be by using
different classes that loaded depending on when they are
present

So for example you will have the base class with the
styles for the fallback font and a class for when the
font is loaded that will overwrite the styles to the
relevant ones for you web font

```css
h1 {
  font-family: Georgia, serif;
  font-size: 3.25rem;
  font-weight: 300;
  line-height: 1.42;
}

html .fonts-loaded h1 {
  font-family: CormorantGaromond, serif;
  font-size: 4rem;
  font-weight: 700;
  line-height: 1.15;
}
```

> This is straight forward but might become tedious to do
> for every class

The other approach is to use atomic `css` to define custom
utility classes that will be used repeatedly in your `html`
elements

```css
html.CormorantGaromond .serif {
  font-family: CormorantGaromond, serif;
}

/* Serif fallback tweeks */
/* 
  We are ussing `not` to ensure our changes
  wont leak over when we load our fonts
*/
html.not(.CormorantGaromond) .serif {
  font-family: Georgia, serif;
  letter-spacing: 0.046em;
  line-height: 1.42;
}

/* For bold serif clases */
html.not(.CormorantGaromond) .serif .b {
  font-weight: 300;
}

/* For diferent font size serif clases */
html.not(.CormorantGaromond) .serif .f1 {
  font-size: 2.44rem;
}

html.not(.CormorantGaromond) .serif .f4 {
  font-size: 1rem;
}
```

```html
<h1 class="serif b f1"></h1>
<h2 class="serif f4"></h1>
```

You might also be able to achieve an even cleaner solution
by using `css` variables

### Important Terms To Know

#### Font Synthesis and Font Matching

When a `font-face` is define the browser will only try to
exactly match on the `font-family` property of an element,
the rest of the properties don't have to be exact and
might be **fuzzy matched** 

If no appropriate `descriptor` of the defined `font-face`
can be match to a `property` then the browser may perform
`font synthesis` to grab from whether it's defined and
display something

For example if you hand a `font-face` that did not
provide an `italic` style and then you had a `class` or
`element` that requires this `style` then the browser
will try it's best to display an `italic` variant
even if it needs to take it from another `font`

> This is all known as `Faux-italic` or `Faux-bold`

You can control this behavior by using the [font-synthesis](https://developer.mozilla.org/en-US/docs/Web/CSS/font-synthesis#browser_compatibility) 
`property` in your `css`

#### Font Subsetting

This involves modifying your font file to include only a
small portion of the original glyph and features

This is typically done to optimize a font file on the
web, but you got to be careful since this might result
in broken fonts or may be against the license

You can use in conjunction with the [unicode-range](https://developer.mozilla.org/en-US/docs/Web/CSS/@font-face/unicode-range)
of the `font-face` block for even better results

#### System Fonts

For a lot of sites that you might be building, `web fonts`
might not be worth the trade-off

You can get away with using `system fonts`, since this
defaults for most user are good enough and familiar
to your users

## Sources

- A [video](https://www.youtube.com/watch?v=tO01ul1WNW8) on web fonts 
- A [glossary](https://www.zachleat.com/web/webfont-glossary/#foft) of terms that are useful to know
  when handling fonts on the web
- A [guide](https://jeremias.codes/2016/05/font-loading-strategy-static-generated-sites/) on using the font observer to load fonts custom
