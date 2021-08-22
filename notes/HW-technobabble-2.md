# HW - Technobabble Generator II

## Overview

- Let's make some changes the Technobabble app and review some commonly used web technologies

## I. Stop Page Zooming

First, let's modify the viewport meta tag to more reliably turn off page zooming on mobile devices - we'll do this by adding a `maximum-scale` directive. Change the `<meta>` tag from this:

`<meta name="viewport" content="width=device-width, initial-scale=1, user-scalable=no">`

To this:

`<meta name="viewport" content="width=device-width, initial-scale=1, maximum-scale=1.0, user-scalable=no">`

<hr>

## II. Improve the experience for mobile and tablet devices

Let's go ahead and modify the CSS to improve the use experience on mobile devices. What we're going to do is to center the text and the button both horizontally *and* vertically on the page for both mobile and tablet devices, while leaving the desktop experience with horizontal alignment only

- There are a lot of ways to do the vertical centering - see this Stack Overflow post --> https://stackoverflow.com/questions/19461521/how-to-center-an-element-horizontally-and-vertically
- Let's pick one of these approaches and use it - the second one - **Approach 2 - Flexbox method** works well
- In this exercise you will make create CSS breakpoints for 3 different screen sizes - mobile, tablet, and dektop/large tablet
- We will be using the same `max-width` breakpoints that bulma does - https://bulma.io/documentation/overview/responsiveness/
- First, here is your HTML for the new centered layout we are doing (replace the old HTML with this):

```html
<div class="container">
  <p id="output">Loading...</p>
  <button id="myButton">More Technobabble!</button>
</div>
```

## II-A. 
