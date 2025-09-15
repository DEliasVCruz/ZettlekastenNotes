# Design layout and spacing

## The 4 pixel rule

It means that almost every element (images, icons, etc), 
section, container, layout or anything in your design should 
be divisible by 4 pixels

For laying out sections we can use it to set

## The max width of our sections:

- We pick a number that it's over 1000px up to 1440px and
  that it's also divisible by 4
    - 1000, 1128, 1256, 1440

## For the padding between sections:

- You want to go for double the spacing between related
  elements in your design
  - Asumming an inner section spacing of 16px
  - You would go for 2x as 32px for the spacing between
    elements

## For your containers size and margings

We need to ask our selves

- What is the most amount of containers you could
  ever put in one row?
    - For modern design theory this is 12 containers
    - Because it's very divisible and you can mix and
      match this container divisions

- How wide the containers should be?
  - It's up to the designer but most go with: 56px, 44px or 72px
  - This will be the maximum size of each container
  - The go to standars is usually 56px

- How much spacing do we want betwen each container?
  - You can choose between stadnard options: 24px, 32px, 40px
  - The 24px spacing is the go to standard for most websites

Once we have this values we need to add:
  - Our number of containers per row
  - Times the size of each container
  - Plus the size of spacing for each space

For 12 container per row, with each container having 72px 
width, and having spacing of 24px we would end up at
  - (72 * 12) + (24 * 11) = 1128px
  - So 1128px would be the max width of our sections

## For the spacing between components

This makes visually consistent looks that subconsiously
ties related components together and visually separates
unrealated ones

### Inner section spacing

We start with the smallest spacing for items that: 

- Are very closely related
  - Icon and text in a button: You can do 4px of spacing

- Are closely related
  - Columns in a menu: You can do 8px of spacing

- Standard components that are semi related
  - A heading and a subheading: You can do 16px of spacing

- For unrelated components in the same section
  - Like action buttons: We ca do 24px of spacing
  - Or the number you chose for the distance between
    containers
  - Usually we have 32 pixels

Notice that as we decrease the strength of relation
between elements we increase the spacing by 2x based on
the previous spacing or the inner spacing of it's elements

## Aplying 4 pixel rule to typography

We start by setting our paraghraps to 16px (usually the
smallest you can go wile still legible)

Using that as our base we can set our: 
- Large paragraph to 20px
- Small subheading to 24px
- Medium subheading to 28px
- Large subheading to 32px

And we do that all the way out to our display text that we
only use for the hero at 64px

Always use the same text sizes and weights for the same
propouses at your website

> The job of type is to create a visually consisten look
> and feal so that visitors are never confused when they
> are on your website
