---
aliases: ["Guide to typography in web design"]
tags: ["fonts", "typography", "web", "design"]
---

# Typography for web design

> Typography it's the art and science of arraying
> text to be both legible and appealing

A font is a combination of characters inside a
typeface

You want to pick a font that matches the energy
of the project you are working on

## Types of fonts

### Serif fonts

They are called like that because they have little
decorative lines hanging at the end of the characters
called `serifs`

This fonts are associated with:
  - Tradition
  - Stability
  - Enduring value

So this are typically used by banks, jewelry and 
lawyers.

- They are perfect if you want your designs to appear
  timeless

- You should avoid them if you are designing something
  contemporary or playful

### San-serif fonts

> They literally mean "without serifs"

- This are the ones we use for a modern looking feel
- The disadvantage is that they can look a little
  boring and homogeneous

Some advantages are:

- A high degree of versatility, can be used almost
  everywhere
  - Since they like a distinct personality

- Lots of variability within a typeface, usually at
  least 8 weights
  - You can adjust the sizing and thickness to create
    different combinations withing the same typeface
  - That means you can use a single typeface for your
    entire brand

- Usually a lot more legible than `serif` fonts

Choose this fonts if:
- You have a modern brand
- Looking for more versatility
- Optimizing for legibility

### Display typeface

This are typefaces built specifically for logos, headings
or titles

They can be `serif`, `san-serif`, made out of weird symbols
or basically anything you want

They are designed to be unique, they don't make good
paragraphs, buttons or labels

If you won't a small chunk of text to really stand out
use a `display typeface`

### Mono space fonts

Most typefaces are **proportional**, meaning different
letters take out more or less space

That it's not true for mono spaced typefaces, where each
character takes exactly the same amount of space

> They are mostly used for text editors and coding

## The 10 most important variables for typography

### Point vs pixels

The fundamental building block of typography are
characters

But the fundamental building block of a character is
called a point

The point is the default unit of measure in typography
and it translate in the physical world to 1/12 of an
inch

> It's a unit of size 12 points = 1 inch

If you are designing for a screen they you will use
pixels instead of points

But this are not literal pixel size but rather
another sizing convention

So a pixel should be worth `.75` points, so 1 inch
in the physical world is worth 16px which is the
same as 12 points

## Em and REM

If you are designing for exclusively digital then this
are the most important units to know

> Its useful to think `em` stands for equal measurement

So `em` is a unit of measurement that sets the size
of the character equal to the size of the font

- On the web the default size of a font it's 16px
- So if you want a heading to be 32px you would set
  it to be equal to 2em

This is great cause it's lets users change the size
of your typography by changing the `em`
  - This happens naturally by zooming in or out on
    a website

If you want to change the default size of `em` to
anything other than 16px then you can use `rem`

> `rem` stands for `root em`

Because this follows the `font-size` you have
defined for your `root` element

> The `:root` element defines stylistic variables
> for your whole website

```css
:root {
  font-size: 18px;
}
```

So if you set this variable, every part of your design
that uses `rem` now becomes proportional to what you
set as your `root` font size

- So if I set it to 18px then `1rem` would be `18px`
- And if I want twice the size (36px) then I would 
  set `2rem`

And your site remains responsive if someone wants to
zoom in or out on your website

### Typefaces weight

This describes the boldness or thickness of a font

Generally the bolder fonts command more visual
attention and are more likely to be used for:
- Titles
- Buttons

Thinner weights are easier to read at smaller sizes
so they are better for:
- Paragraphs
- Labels

> It pays a huge role in the legibility of your font

A large and extremely thin headline is usually harder
to read than a bolder one

Likewise a bold paragraph is too dense to differentiate
between individual characters

### The `baseline`, the `capline` and the `x-height`

The `baseline` it's the invisible line upon which your 
font rests

In the other direction characters extend above the
baseline and their max height it's determined by
the `capline`

The `capline` it's a sealing that stops the upper
case letters of a font

The lower case letter have their own invisible line
to limit their size and it's called the `x-height`

> Some typefaces let you manipulate the `x-height` to
> get more variability in your design

This all make up our measurements for a single line
of text

### The line height

> In print typography it's known as `leading`

For the space between lines, they are measured from
base line to base line between lines

So they are basically the space between the line bellow
relative to the line above

You can manipulate the line height to increase the
legibility of your text to different sizes

> Generally speaking the default line height does not
> look very good and it's about 125% of the font size

The rule of thumb for line height it's that it's
inversionally proportional to the size of your fonts

So your biggest headline might have that it's exactly
equal to the size of your text

While the smallest paragraph might have a line height
that's `1.5` bigger than your paragraph

> This rules may change depending on your typeface

### Letter spacing

> In print typography it's known as `tracking`

The spacing between character also plays a huge role
in the legibility of your fonts

It's also inversionally proportional to the size
of your font

The bigger the text the more the eye has to move
to read each letter, and to minimize this visual
strain, putting letters 1 or 2 pixels together
can improve the legibility

At smaller sizes the space between letter should be
increased slightly so that you can more easily
make out individual characters

### Kerning

Any font that isn't mono spaced comes with it's own
default character spacing

So most fonts have different spacing between different
character combinations

So letter combinations like `WA` may have more spacing
between them so that you can tell each letter apart

> You can manipulate the kerning of each letter to
> achive special effects

### Accesible contrast

It's the color different between your typography and
the background

Generally text it's accessible if your have a contrast
ratio of `7:1` or greater

- You can use [contrast checkers](https://webaim.org/resources/contrastchecker/)
  - To test for the accessability for contrast combinations
  - To ensure that your text it's legible in small and
    large sizes

## A typography system

Building one makes our whole design look clean, consistent
and makes creating new text sections as easy as putting
together pieces

The basis of our system is typographical hierarchy

- The idea is to create rules for each type in our design
  so that it's easy to read and navigate

This hierarchy is generally divided into 4 categories
- Headings
- Paragraphs
- Buttons
- Labels

To build our headings hierarchy we start by defining the
largest heading style

  - We set our font variables to what looks good for our
    product
  - We adjust those parameters to get smaller thinner and
    more spaced out the smaller we go

After defining our headings we go for our paragraphs,
buttons and labels

  - In general we follow the same rules as our headings
  - The smaller the text the thinner and more spaced
    out it will be

An important exception it's in our buttons, which are
often bolder than the paragraphs so visitors know where
to click and to compensate for this increased weight
we will also increase the spacing slightly to avoid
having squishy characters

Finally labels are often design to be smaller than
paragraphs with less color contrast

  - Used for annotations above images
  - As pop-ups inside paragraphs

## The spacing between text elements

This is called designing around a grid, because we
use grid boxes to decide how fare text can go before
wrapping

In web design you want to use 12 columns because it's
a very divisible number

- Your headline might take about 12 columns
- Your paragraph only 6 columns
- A button just 1 column

## Choosing typefaces

Four our sans-serifs a very legible style it's

- Humanist Sans: They are more legible for web copys
  - Tahoma
  - Gill Sans
  - Frutiger

- Geometrics: Letter forms based no gemotric shapes
  - Futura
  - Bank gothic
  - Gotham

## File formats for fonts

- OpenType (`.otf`): Includes the most customization options
- Woff (`.woff`): Preferred format for web fonts, compressed and load faster
- Woff2 (`.woff2`): They are even more compressed for faster loads
