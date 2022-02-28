# Web Component Summary

## Overview

- Below, let's look at a few different "styles" of web components that we could write


## I. "Hello World"
- The component below takes no parameters of any kind, it simply renders out the same HTML every time it is used on a page
- In the "real-world", components like this are not uncommon, and are in fact useful
- However, in this class, the project requirements state that all of your components MUST take parameters
- This means that components like the one below are NOT acceptable for Project 1

**hello-world.js**

```js
const template = document.createElement("template");
template.innerHTML = "<p>Hello World</p>";

class HelloWorld extends HTMLElement{
  constructor(){
    super();
    this.attachShadow({mode: "open"});
    this.shadowRoot.appendChild(template.content.cloneNode(true));
  }
} 

customElements.define("hello-world", HelloWorld);
```

**Usage:**

```html
<!-- Put this in HTML file-->
<hello-world></hello-world>
```

<hr>

## II. A single unnamed *slot*

**app-header.js**
```js
const template = document.createElement("template");
template.innerHTML = `
<link rel="stylesheet" href="https://cdn.jsdelivr.net/npm/bulma@0.9.3/css/bulma.min.css">
<style>
:host{
  user-select: none;
}
</style>
<header class="hero is-small is-primary is-bold">
<div class="hero-body">
  <div class="container">
    <h1 class="title"><slot></slot></h1>
  </div>
</div>
</header>
`;

class AppHeader extends HTMLElement{
  constructor(){
    super();
    this.attachShadow({mode: "open"});
    this.shadowRoot.appendChild(template.content.cloneNode(true));
  }
}

customElements.define("app-header", AppHeader);
```


**Usage:**

```html
<!-- Put this in HTML file-->
<app-header>Greeter with Slots</app-header>
```

<hr>

## III. Two named *slots*

**app-header2.js**

```js
const template = document.createElement("template");
template.innerHTML = `
<link rel="stylesheet" href="https://cdn.jsdelivr.net/npm/bulma@0.9.3/css/bulma.min.css">
<style>
:host{
  user-select: none;
}
</style>
<header class="hero is-small is-warning is-bold">
<div class="hero-body">
  <div class="container">
    <h1 class="title"><slot name="my-title"></slot></h1>
    <h2 class="subtitle"><slot name="my-subtitle"></slot></h2>
  </div>
</div>
</header>
`;

class AppHeader2 extends HTMLElement{
  constructor(){
    super();
    this.attachShadow({mode: "open"});
    this.shadowRoot.appendChild(template.content.cloneNode(true));
  }
}

customElements.define("app-header2", AppHeader2);
```


**Usage:**

```html
<!-- Put this in HTML file-->
<app-header2>
  <span slot="my-title">Greeter with Slots #2</span>	
  <span slot="my-subtitle">This is a rockin' App!</span>	
</app-header2>
```

<hr>

## IV. HTML Custom Attributes

**app-header3.js**

```js
/* Custom HTML Attributes */
const template4 = document.createElement("template");
template4.innerHTML = `
<link rel="stylesheet" href="https://cdn.jsdelivr.net/npm/bulma@0.9.3/css/bulma.min.css">
<style>
:host{
user-select: none;
}
</style>
<header class="hero is-small is-danger is-bold">
<div class="hero-body">
<div class="container">
  <h1 class="title">???</h1>
  <h2 class="subtitle">???</h2>
</div>
</div>
</header>
`;

class AppHeader3 extends HTMLElement{
  constructor(){
    super();
    this.attachShadow({mode: "open"});
    this.shadowRoot.appendChild(template4.content.cloneNode(true));
  }

  connectedCallback(){
    this.h1 = this.shadowRoot.querySelector(".title");
    this.h2 = this.shadowRoot.querySelector(".subtitle");
    this.render();
  }

  render(){
    this.h1.textContent = this.dataset.title || "No title found";
    this.h2.textContent = this.dataset.subtitle || "No subtitle found";
  }
}

customElements.define("app-header3", AppHeader3);
```

**Usage:**

```html
<!-- Put this in HTML file-->
<app-header3></app-header3>
<app-header3 data-title="Greeter with attributes" data-subtitle="Are we done yet?"></app-header3>
```

## V. JS Property

**app-result.js**

```js

```

**Usage:**

```html

```
