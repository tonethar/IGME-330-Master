# HW - Intro to Bulma

## I. Overview

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

## II. Get Started

- Here is the link to the first tutorial - [Bulma CSS Tutorial (Product Page Build) #1 - Intro & Setup](https://www.youtube.com/watch?v=SCSAExGFK1E&list=PL4cUxeGkcC9iXItWKbaQxcyDT1u6E7a8a&index=2)
- This one you can breeze through pretty quickly, but there are a few things to note (some of this repeats what we wrote above):
  - Bulma is CSS only, no JS (unlike bootstrap)
  - Bulma is “mobile first”, so everything generally looks good on mobile by default
  - Not opinionated on how things are done, meaning it has no JS to do things like (for example) changing button states
  - Walks though/quickly demos:
    - installing VSCode’s LiveServer (which you should already have installed)
    - using Emmet (an autocomplete API that VSCode uses)
  - Setting up the **index.html** start page:
    - Starter Template is here - https://bulma.io/documentation/overview/start/
    - note that we need the `<link>` tag to import the Bulma library
    - note that Bulma has built-in styles that are applied by default - see the changes to the "Hello Bulma!!!" text in the window, and in the web inspector as well
    - for your convenience, here is the starter code

**index.html**

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







