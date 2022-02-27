# Web Component Summary


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

`<hello-world></hello-world>`

<hr>

## II. A single unnamed *slot*



