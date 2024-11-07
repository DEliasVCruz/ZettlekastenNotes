---
aliases: ["How to work with fonts in the web"]
tags: ["performance", "web", "fonts"]
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

### System Fonts

For a lot of sites that you might be building, `web fonts`
might not be worth the trade-off

You can get away with using `system fonts`, since this
defaults for most user are good enough and familiar
to your users

## Sources

- A [video](https://www.youtube.com/watch?v=tO01ul1WNW8) on web fonts 
