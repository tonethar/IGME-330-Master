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

## I. Get Started - *#1 - Bulma Intro & Setup*

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

## II. *#2 - Bulma Fonts & Colours*
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


**That's It! Be sure to save these changes to index-2.html, and look over the Typography & Color Documentation pages linked above!**

<hr>

## III. *#3 - Spacing & Containers*

- Here is the link to the 2nd tutorial - [Bulma Tutorial (Product Page Build) #3 - Spacing & Containers](https://www.youtube.com/watch?v=--gQv_IXcMw&list=PL4cUxeGkcC9iXItWKbaQxcyDT1u6E7a8a&index=3)
- This tutorial will walk through how
- Make a copy of **index-2.html** and name it **index-3.html**
- Paste the following into the `<body>` of **index-3.html** (get rid of the tags from the previous video)

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
  - note use of Emmet & `lorum30`
  - adds padding around the element - check the browser window and web inspector to see how much
- `container` class - has a max width

