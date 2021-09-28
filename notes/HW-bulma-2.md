# HW - Bulma II - Bulma & Web Components

## Overview

- We are going to run through how to add a Web Component to **home.html** from last time

## I. Create a Bulma `footer`

- Let's add a `footer` to our P1 Bulma Template
- The Bulma **footer** is a simple container, with lots of bottom padding, making it great as the last element of any webpage.
- Make a copy of **home.html** and name it **home-wc.html**

### Step #1 - get the HTML

- We will make it easy for ourselves and grab the `footer` code from the Bulma web site:
  - https://bulma.io/documentation/layout/footer/
  - grab the example, and paste it into **home-wc.html**, AFTER the closing `<div>` of `columns`
  - and here it is, just in case the docs get changed anytime soon:

```html
<footer class="footer">
  <div class="content has-text-centered">
    <p>
      <strong>Bulma</strong> by <a href="https://jgthms.com">Jeremy Thomas</a>. The source code is licensed
      <a href="http://opensource.org/licenses/mit-license.php">MIT</a>. The website content
      is licensed <a href="http://creativecommons.org/licenses/by-nc-sa/4.0/">CC BY NC SA 4.0</a>.
    </p>
  </div>
</footer>
```

- go ahead and preview it - you should see the following - note how the text is centered and that there is a large amount of white space at the bottom of the page:

![screenshot](_images/_bulma/HW-bulma-5.png)

### Step #2 - Add some Bulma classes

- let's tighten this up and get rid of some of that white space
- add `pt-0 pb-0` to the `<footer>` element's `class=`
- look for `has-text-centered` and change it to `has-text-left`
- it should look like this:

![screenshot](_images/_bulma/HW-bulma-6.png)

<hr>

## II. Convert it to a Web Component

<hr><hr>

[**&lt;-- Previous - Bulma I - Intro to Bulma**](HW-bulma-1.md)
