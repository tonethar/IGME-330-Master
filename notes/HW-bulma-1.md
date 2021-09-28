# HW - Intro to Bulma

## Overview

- https://bulma.io/
- "Bulma is a free, open source framework that provides ready-to-use frontend components that you can easily combine to build responsive web interfaces."
- Bulma is mobile friendly & responsive by default
- Bulma is modern - built with Flexbox - but with much more intuitive and easy-to-use syntax
- Bulma doesn't use any JavaScript (unlike Bootstrap) - it's up to the developer to add it. This makes it very easy to integrate with VanillaJS, web components, Vue.js, React etc
- Using Bulma is required for Project 1
- Below, we are going to take advantage of a pre-existing YouTube tutorial on Bulma:
  - the [Net Ninja Bulma Tutorial series](https://www.youtube.com/playlist?list=PL4cUxeGkcC9iXItWKbaQxcyDT1u6E7a8a)
  - but we're not just going to say "watch this and figure out Bulma on your own"
  - instead, we'll have some companion notes for you as we walk through the first several videos in the series, and some tips on how to adapt this tutorial so that you can get Bulma working with Project 1

<hr>

## I. Get Started - #1 - *Bulma Intro & Setup*

- Here is the link to the 1st tutorial - [Bulma CSS Tutorial (Product Page Build) #1 - Intro & Setup](https://www.youtube.com/watch?v=SCSAExGFK1E&list=PL4cUxeGkcC9iXItWKbaQxcyDT1u6E7a8a&index=2)
- This one you can breeze through pretty quickly, but there are a few things to note (some of this repeats what we wrote above):
  - Bulma is CSS only, no JS (unlike bootstrap)
  - Bulma is “mobile first”, so everything generally looks good on mobile by default
  - Not opinionated on how things are done, meaning it has no JS to do things like (for example) changing button states
  - Walks though/quickly demos:
    - installing VSCode’s LiveServer (which you should already have installed)
    - using Emmet (an autocomplete API that VSCode uses) - https://emmet.io/
  - Setting up the **index.html** start page:
    - Starter Template is here - https://bulma.io/documentation/overview/start/
    - note that we need the `<link>` tag to import the Bulma library
    - note that Bulma has styles that override the default browser styles - these are applied by default:
      - see the changes to the `<h1>` "Hello Bulma!!!" text in the window
      - look in the web inspector, you can see that Bulma styles `<h1>`, `<h2>`, `<h3>` through `<h6>` tags the same
      - also see how links are styled differently - there's no underline, and you have a default `:hover` affect applied
    - for your convenience, here is the starter code:

**index-1.html**

```html
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta http-equiv="X-UA-Compatible" content="IE=edge">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Ninja Coffee</title>
  <link rel="stylesheet" href="https://cdn.jsdelivr.net/npm/bulma@0.9.3/css/bulma.min.css">
</head>
<body>
  <h1>Hello Bulma!!!</h1>
</body>
</html>
```

- all of the course files are here (look for the pull-down to access the files for each video): https://github.com/iamshaunjp/bulma-ui-build
- that's it - go ahead and save the changes to **index-1.html** and move on

<hr>

## II. #2 - *Bulma Fonts & Colours*
- Here is the link to the 2nd tutorial - [Bulma Tutorial (Product Page Build) #2 - Fonts & Colours](https://www.youtube.com/watch?v=j9ijz7u_M_o&list=PL4cUxeGkcC9iXItWKbaQxcyDT1u6E7a8a&index=2)
- This tutorial will walk through how to specify different font styles and colors
- Make a copy of **index-1.html** and name it **index-2.html**
- Paste the following into the `<body>` of **index-2.html** (get rid of the `<h1>` and `<a>` tags from the previous video)
- Preview **index-2.html** in the browser, note how Bulma has styled all of the text of these elements to be the same size
- We are going to change that - follow along with the video and add the various Bulma classes to the elements below

```html
  <!-- fonts -->
  <h1>Hello, Bulma</h1>
  <h2>Hello, Bulma</h2>
  <h3>Hello, Bulma</h3>
  <h4>Hello, Bulma</h4>

  <p>Hello again</p>
  <p>Hello again</p>
  <p>Hello again</p>
  <p>Hello again</p>

  <h2>Title</h2>
  <h3>Subtitle</h3>

  <!-- colours -->
  <p>I'm primary text</p>
  <p>I'm warning text</p>
  <p>I'm danger text</p>
  <p>I'm info text</p>
  <p>I'm success text</p>
  <p>I'm dark text</p>
  <p>I'm light text</p>
```

### II-A. Summary

**Typography & Color Docs here:**
- https://bulma.io/documentation/helpers/typography-helpers/
- https://bulma.io/documentation/helpers/color-helpers/

<br>

- `is-size-1` through `is-size-7` - 1 is the largest
- `is-uppercase` & `is-italic` & `is-lowercase` - there is also  `is-capitalized` & `is-underlined`
- `has-text-weight-bold` & `has-text-weight-light` - *light* is a color qualifier, *bold* is a text weight qualifier
- `title` & `subtitle` - *title* is large and bold, *subtitle* is smaller and less bold
- BTW - I don't think it's mentioned in the video, but elements can belong to (i.e. apply) multiple CSS classes - multiple class names will need to be separated by a space

<br>

- `has-text-centered` & `has-text-right`

<br>

- `has-text-primary` - greenish text
- `has-text-warning`  - yellowish test
- `has-text-danger` - reddish text
- `has-text-info`  - blueish text
- `has-text-success` - light-green text
- `has-text-dark` - dark text
- `has-text-light` - light gray text (we can't see it on a white background)

<br>

- `has-text-danger-dark` - dark red text
- `has-text-danger-light` - light red text

<br>

- `has-background-light` - light gray background
- `has-background-danger` - reddish background
- `has-background-danger-light` - can still use color qualifiers on background
- `has-background-primary-dark` - can still use color qualifiers on background


**That's It! Be sure to save these changes to index-2.html, and look over the Typography & Color documentation pages linked above!**

<hr>

## III. #3 - *Spacing & Containers*

- Here is the link to the 3rd tutorial - [Bulma Tutorial (Product Page Build) #3 - Spacing & Containers](https://www.youtube.com/watch?v=--gQv_IXcMw&list=PL4cUxeGkcC9iXItWKbaQxcyDT1u6E7a8a&index=3)
- This tutorial will walk through how to add maring and padding to elements using Bulma, and will introduce us to the `section` and `container` classes
- Make a copy of **index-2.html** and name it **index-3.html**
- Paste the following into the `<body>` of **index-3.html** (first, get rid of the tags from the previous video)

```html
<!-- spacing -->

<h1 class="">Hello, Bulma</h1>
<h1 class="">Hello, Bulma</h1>
<h1 class="">Hello, Bulma</h1>
```

### III-A. Summary

**Spacing Docs here:**
- https://bulma.io/documentation/helpers/spacing-helpers/

<br>

- `px-6` - padding x (left AND right)
- `py-6` - padding y (top AND bottom)
- `mx-6` - margin x (left AND right)
- `my-6` - margin y (top AND bottom)
- `mt-6` - margin top
- `mb-6` - margin bottom
- `ml-6` - margin left
- `mr-6` - margin right
- `pt-6` - padding top
- `pb-6` - padding bottom
- `pl-6` - padding left
- `pr-6` - padding right

<br>

- `section` class:
  - note use of Emmet & `lorem30`
  - adds padding around the element - check the browser window and web inspector to see how much
  - `section` class can be applied to a `<div>` to, not just a `<section>` tag
  - note that the `section` class makes the element stretch across the screen

<br>

- `container` class:
  - adds centering with `margin-right: 0` & `margin-left: 0`
  - has a `max-width` of `960px`


**That's It! Be sure to save these changes to index-3.html, and look over the Spacing documentation page linked above!**

<hr>

## IV. #4 - *Navbar (desktop)*

- Here is the link to the 4th tutorial - [Bulma Tutorial (Product Page Build) #4 - Navbar (desktop)](https://www.youtube.com/watch?v=HmfQq0suMSA&list=PL4cUxeGkcC9iXItWKbaQxcyDT1u6E7a8a&index=4)
- This tutorial will walk through how to build a Bulma `Navbar`
- Make a copy of **index-3.html** and name it **index-4.html**
- Delete all of the elements in the `<body>` of **index-4.html** and start fresh


### IV-A. Summary

**Navbar Docs here:**
- https://bulma.io/documentation/components/navbar/
- Structuring these is a little confusing, so pay close attention to the video, and look at the examples in the link above

<br>

- In this video will build a simple `Navbar` with a logo and 2 links 
- `navbar` class - the **main** container
  - look in web inspector - see that it uses `position: relative`
- `navbar-brand` - the **left side**, always visible, which usually contains the logo and optionally some links or icons
- `navbar-item` -  each **single item** of the navbar, which can either be an `<a>` or a `<div>`
  - BTW - the Ninja Coffee logo is here: https://github.com/iamshaunjp/bulma-ui-build/tree/lesson-4/assets
  - `style="max-height: 70px"` increases the height of the item, and thus the entire navbar
  - `class="py-2 px-2”` added some padding for us
- `navbar-menu` - the **right side**, hidden on touch devices, visible on desktop
- `navbar-start` - the **left part** of the menu, which appears next to the navbar brand on desktop
- `navbar-end` - the **right part** of the menu, which appears at the end of the navbar
- added `has-shadow` to `<nav>` to give it a very light shadow on its border
- added `is-primary` and then `is-white` to `<nav>`

<br>

- all done - be sure to save all of the changes
- notice that when the window width is less that `1024px` the right side menu items disappear - what happens is that the `<div>` of class `navbar-menu` becomes `display: none`
- this is normal Bulma behavior, and in the next part we'll add mobile support by putting these links under a hamburger menu

<hr>

## V. #5 - *Navbar (for mobiles)*

- Here is the link to the 5th tutorial - [Bulma Tutorial (Product Page Build) #5 - Navbar (for mobiles) (04:58)](https://www.youtube.com/watch?v=qvn2SxGvyPs&list=PL4cUxeGkcC9iXItWKbaQxcyDT1u6E7a8a&index=5&pp=QAFIAw%3D%3D)
- This tutorial will walk through how to build a burger icon to show the `navbar-menu` links on smaller screened mobile devices
- Make a copy of **index-4.html** and name it **index-5.html**


### V-A. Summary

**Navbar Docs here:**
- https://bulma.io/documentation/components/navbar/
- We will need to write JavaScript to show/hide the burger icon - Bulma won't do that for us

<br>

- `navbar-burger` - the **hamburger** icon, which toggles the `navbar-menu` on touch devices
