# HW - Technobabble Generator II

## Overview

Let's make some changes the Technobabble app and review some commonly used web technologies

## I. Stop Page Zooming

First, let's modify the viewport meta tag to more reliably turn off page zooming on mobile devices - we'll do this by adding a `maximum-scale` directive. Change the `<meta>` tag from this:

`<meta name="viewport" content="width=device-width, initial-scale=1, userscalable=no">`

To this:

`<meta name="viewport" content="width=device-width, initial-scale=1, maximum-scale=1.0, userscalable=no">`

<hr>

# II. Improve the mobile experience

Let's go ahead and modify the CSS to improve the use experience on mobile devices. What we're going to do is to center the text and the button both horizontally *and* vertically on the page. There are a lot of ways to do the vertical centering - see this Stack Overflow post --> https://stackoverflow.com/questions/19461521/how-to-center-an-element-horizontally-and-vertically

- Pick one of these approaches and make it so - the first one - **Approach 1 - transform translateX/translateY** works well
- These new CSS rules will be added to your mobile media query:
- While you are at it, change the `max-width:` value for your media query from `600px` to `768px` which will support larger screened smart phones. This "CSS breakpoint" value better aligns with mpst of the CSS frameworks are doing:  
