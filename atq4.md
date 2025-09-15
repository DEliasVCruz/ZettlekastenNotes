---
aliases: ["What to keep in mind when designign an app"]
tags: ["design", "web", "style", "colors"]
---

# Design system principles

## General rules

###  Visual hierarchy

It helps show the order of importance among elements

### Contrast

Helps distinguish elements and make them readable or
accessible

### Balance

It helps in moderate the spacing, alignment or the placement
of different elements

### Consistency

It helps in keeping elements harmonical and avoids user
confusion

### Simplicity

It keeps things clear and straight forward for users

### Feedback

For extra interactions, giving users feedback of their
actions keeps them engaged, and gives them some clear
reactions for their actions

> Feedback should not get in the way of usability and
> core goals of the apps, fancy animations are not
> great if they delay user actions too much

## More design rules

### Design as little as possible

What is the minimum you need to achieve some functionality
or affordance for your users, start from there

- Most of the time you just need a heading an input

> Simple designs are easier to use and thus better designs

### Use the laws of similarity and proximity

- Similar things means they belong to the same group
  - Use shape of things
  - Use size of things
  - Use color of things

> This makes the design consistent and easier to implement

- Things that are closer together belong to the same group
  - Use spacing of things

> This gives us a better understanding of layout and spacing

Make the designs simple enough to be understood as a whole,
as a collection of sections and groups

> The design should be scanable within seconds

###  Elements need more spacing than you think

When you are focus on designing an specific element, the
spacing might seem to much for you, but remember that the
user scans the whole UI before focusing on individual
elements

So start with a lot of spacing, and look at the design as
a whole. Then start to remove the spacing taking the previous
rule into account, until you are happy with the results

### Use a design system

For a simple website you just need to define key design
elements and you are good to go

> You may want bigger typescales for landing pages and
> smaller typescales for UIs, within this you may want
> to have different scales for big and small UIs

For UIs you need a more complex and detail design system
that covers a lot of scenarios

- For spacing: Separate and start the values that are
  divisible by four
    - Linear increments for smaller values
    - Exponential increments for bigger values

> For font size and margins we use `rem` unis, this way
> the design can adapt to the user system preferences

To assign a `rem` value just divide the `pixel` value by
16 (`1 rem = 16 pixels`)

Line height is inversionally proportional to the font
size

This means smaller text needs greater line height than
bigger text for legibility

> Greater line height also acts as margin top on text
> elements, this way you don't have to design spacing
> between all text elements

- Designs the key elements

Start with the `buttons` and `links`
  - Generally you need two types for each
  - One for primary actions and one for secondary actions
  - For the typescale use the body text size
  - For the colors, use your accent colors

### Hierarchy is everything

We need to emphasize certain elements in the page, to help
the users navigate and find important actions

To emphasize important elements we can use:
  - Size
  - Weight
  - Color

> It's very easy to overdue this things, so start small, 
> little changes can have big impact on the overall design

To emphasize an element begin by asking:
  - What's the first thing the user will look for?

> Sometimes to emphasize something, you need to de-emphasize
> other competing elements

When you are done with the emphasizing design, zoom out
to see if what you where trying to emphasize stands out from
the rest of the information

> If the design isn't scanable, you need to do adjustments
> most will scan in a z-like patter from left to right, top
> to bottom

- Introduce depth to add some character
- Use colors and shadows to elevate important elements
  - They can also be used to replace solid borders
- The closer something feels to the user, the more it will
  attract their focus
- Use your accent colors to highlight important elements
