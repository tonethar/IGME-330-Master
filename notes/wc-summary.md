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
const template = document.createElement("template");
template.innerHTML = `
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
    this.shadowRoot.appendChild(template.content.cloneNode(true));
  }

  connectedCallback(){
    this.h1 = this.shadowRoot.querySelector(".title");
    this.h2 = this.shadowRoot.querySelector(".subtitle");
    this.render();
  }

  render(){
    this.h1.textContent = this.dataset.mytitle || "No title found";
    this.h2.textContent = this.dataset.mysubtitle || "No subtitle found";
  }
}

customElements.define("app-header3", AppHeader3);
```

**Usage:**

```html
<!-- Put this in HTML file-->
<app-header3></app-header3>
<app-header3 data-mytitle="Greeter with attributes" data-mysubtitle="Are we done yet?"></app-header3>
```

## V. Component with JS Property

**app-result.js**

```js
const template = document.createElement("template");
  template.innerHTML = `
  <link rel="stylesheet" href="https://cdn.jsdelivr.net/npm/bulma@0.9.3/css/bulma.min.css">
  <style>
  .card{
    width: 200px;
    height: 300px;
    display: inline-block;
    border: 1px solid black;
    overflow: auto;
  }
  </style>
  <div class="card has-background-info-light">
    <div class="card-header">
      <div class="card-header-title is-size-5">
        <span id="title">???</span>
      </div>
    </div>
    <div class="card-content is-size-6">
      <span id="age">???</span>
    </div>
    <div class="card-content">
      <p><i>A dragon is a snake-like legendary creature that appears in the folklore of many cultures worldwide. The earliest attested reports of draconic creatures resemble giant snakes. Draconic creatures are first described in the mythologies of the ancient Near East and appear in ancient Mesopotamian art and literature.</i></p>
    </div>
  </div>
  `;

  class AppResult extends HTMLElement{
    constructor(){
      super();
      this.attachShadow({mode: "open"});
      this.shadowRoot.appendChild(template.content.cloneNode(true));
      this.dragon = {"type": "Ethereal", "age": 40};
    }

    connectedCallback(){
      this.titleElement = this.shadowRoot.querySelector("#title");
      this.ageElement = this.shadowRoot.querySelector("#age");
      this.render();
    }

    render(){
      this.titleElement.textContent = `${this.dragon.type} Dragon`;
      this.ageElement.textContent = `${this.dragon.age} years old`;
    }
  }

  customElements.define("app-result", AppResult);

  window.onload = () => {
    const newCard = document.createElement("app-result");
    newCard.dragon = {"type": "Smoke", "age": 80};
    document.body.appendChild(newCard);
  };
```

**Usage:**

```html
<app-result></app-result>
```
