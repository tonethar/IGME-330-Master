# HW - Web Components-1 - Intro to Web Components

## Overview

- The video walkthrough for this assignment is here. You will need to be logged into RIT/myCourses before you can access it:
  - HW - Web Components-1 (XX:XX)


## I. About Web Components

- Modern web developers often utilize front-end frameworks like [React](https://reactjs.org/), [Angular](https://angular.io/) or [Vue.js](https://vuejs.org/) to develop rich user interfaces
- These 3rd party frameworks allow developers to break their user interfaces (written in HTML/CSS/JS) into reusable *components* such as search boxes, interactive product lists, site headers/footers/naviation systems, and so on. These component contain (encapsulate) the HTML tags, CSS and JS that the component needs to function
- The major disadvantage of using 3rd party frameworks to design web sites is that your framework specific code will likely go obsolete fairly quickly, which makes ongoing maintenance of a site time-consuming and expensive. Additionally, most of these framework are dependant on 3rd party tooling to transform the HTMK/CSS/JS from the framework's proprietary syntax into a form that the browser can understand
- Web Components have been standardized for all of the major browsers, and will function "out of the box" without any required third--party tooling:
  - https://developer.mozilla.org/en-US/docs/Web/Web_Components
  - https://www.webcomponents.org/introduction
  - https://css-tricks.com/an-introduction-to-web-components/
 - Web Components consist of 3 major technologies that are used together:
   - ***Custom Elements*** - a way that we can define our own custom DOM elements (tags), and to also extend built-in elements
     - *"Custom elements provide a way for authors to build their own fully-featured DOM elements. Although authors could always use non-standard elements in their documents, with application-specific behavior added after the fact by scripting or similar ..."* - https://html.spec.whatwg.org/multipage/custom-elements.html#custom-elements
    - ***Shadow DOM*** - encapsulates CSS (style rules, class names etc are scoped to the component) and HTML (a component's DOM is self-contained and not detectable by `document.querySelector()`
      - https://developers.google.com/web/fundamentals/web-components/shadowdom
    - ***HTML Templates***
      - *"The `<template>` element is used to declare fragments of HTML that can be cloned and inserted in the document by script."* - https://html.spec.whatwg.org/multipage/scripting.html#the-template-element
 - Web Components are supported natively on all modern browsers, and can be used on older browsers with a [*polyfill*](https://developer.mozilla.org/en-US/docs/Glossary/Polyfill):
   - https://www.webcomponents.org/polyfills
   - https://github.com/webcomponents/polyfills/tree/master/packages/webcomponentsjs
   - https://cdnjs.cloudflare.com/ajax/libs/webcomponentsjs/2.6.0/webcomponents-bundle.js

<hr>

## II. An overview of a web component

- to create a custom HTML element, you first need to extend the `HTMLElement` class
- we then add in some or all of these component *lifecycle* methods
  - `connectedCallback()` - called when the component is inserted into the DOM
  - `disconnectedCallback()` - called when the component is removed from the DOM
  - `attributeChangedCallback()` - called each time one of the component's "watched" attributes changes
  - `static get observedAttributes()` - specifes which attributes we want to be notified when their values change


```html
<script>
// Create a class and extend HTMLElement
class MyElement extends HTMLElement{
  // #1 - constructor called when instance of this class is created
  constructor(){
   // setup
  }
  
  // #2 - called when the component is inserted into the DOM
  connectedCallback(){
    // draw page
    this.render();
    // we could also hookup some JavaScript to DOM events
  }
  
  // #3 - called when the component is removed from the DOM
  disconnectedCallback(){
    // a good place to clean up, remove event listeners, etc ...
  }
  
  // #4 - this lifecycle method is invoked each time one of the component's "watched" attributes changes
  attributeChangedCallback(attributeName, oldVal, newVal){
    console.log(attributeName, oldVal, newVal);
    this.render();
  }
  
  // #5 - here were specify for which attributes we want to be notified when their values change
  static get observedAttributes(){
    return ["data-year", "data-text"];
  }
		
  // #6 - a helper method (could be named anything) to display the values of the attributes
  render(){
    // update the DOM in some way based on the value of the attributes
  }
  
} // end class

// #7 - define our new custom element with `customElements.define()` so that we can use it on the page
customElements.define('my-element', MyElement);
</script>
...
<body>
  <!-- Use it! -->
  <my-element></my-element>
  ...
</body>
```

<hr>

## III. Start file

**footer-component-start.html**

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="utf-8" />
  <title>igm-footer Component 1</title>
  <!-- Web Components Polyfill for older browsers -->
  <script defer src="https://cdnjs.cloudflare.com/ajax/libs/webcomponentsjs/2.6.0/webcomponents-loader.min.js"></script>
 
  <script>
  // YOUR CODE GOES HERE
  class IGMFooter extends HTMLElement{
    constructor(){
      super();
    }
  } 
	
  customElements.define('igm-footer', IGMFooter);
	
  window.onload = () => {
	 
  };
</script>
</head>
<body>
<h1>Web Component - with attributes and <code>connectedCallback()</code></h1>
<p>Here we have a new component, <code>&lt;igm-footer></code> that has <ode>data-year</code> and <ode>data-text</code> attributes</p>
<p>We are also utilizing the <code>connectedCallback()</code> lifecycle method, which is invoked each time the custom element is appended into a document-connected element</p>

<h2>1st footer</h2>
<igm-footer></igm-footer>

<h2>2nd footer</h2>
<igm-footer></igm-footer>

<h2>3rd footer</h2>
<igm-footer></igm-footer>

<h2>4th footer</h2>
<igm-footer></igm-footer>
	
</body>
</html>
```

<hr>

- Go ahead and preview this in a browser. There are 4 `<igm-footer>`s  in the browser web inspector, but they are not drawn to the browser window yet, so we need to do that next

<hr>

## IV. The Shadow DOM
- Althought the *Shadow DOM* sounds kind of mysterious, it is simply a "scoped" DOM that components have that is separate from the main DOM of the document
- For example, if our component had an `<h1>` in it,  and we wrote a `document.querySelector("h1")` call, or wrote a style rule like this `h1{color:red}` - our component's `<h1>` would be uneffected

<hr>

## IV-A. Creating a Shadow DOM

- Add the following to the `constructor()` above, right after the call to `super()`:

```js
// 1 - attach a shadow DOM tree to this instance - this creates `.shadowRoot` for us
this.attachShadow({mode: "open"});
			
// 2 - create the <span> element and add to shadow DOM
this.shadowRoot.appendChild(document.createElement('span'));
			
// 3 - (for illustrative purposes) we will create and add an <hr> to the shadow DOM
this.shadowRoot.appendChild(document.createElement('hr'));
```

- Now preview this in the browser:
  - you should be able to see the `<hr>`s in the browser's window
  - because we specified `mode: "open"`, some of the internal structure of the component is visible. Go ahead and look in the web inspector for `#shadow-root` to see this
  - change the `mode` to `"closed"` and then head back to the inspector to see the change

<hr>

## IV-B. Adding style

- Here we're going to add some style for the component, and a `<span>` (for use in the next part)
- Update your constructor with these changes (note that the numbering has changed) 

```js
// 1 - attach a shadow DOM tree to this instance - this creates `.shadowRoot` for us
this.attachShadow({mode: "open"});

// 2 - NEW - create the <span> element and add to shadow DOM
this.shadowRoot.appendChild(document.createElement('span'));

// 3 - (for illustrative purposes) we will create and add an <hr> to the shadow DOM
this.shadowRoot.appendChild(document.createElement('hr'));

// 4 - NEW - create the <style> element and add to shadow DOM
const style = document.createElement('style');
style.textContent = `
	:host{
		color: #F76902;
		display: block;
		font-variant: small-caps;
		font-weight: bolder;
		font-family: sans-serif;
	}
`;
this.shadowRoot.append(style);
```

- preview this in the browser, it shouldn't look different
- if you look in the inspector, under the `#shadow-root` you'll see the `<span>`, but no `<style>` tag
- the `host:` CSS pseudo-class is documented here - https://developer.mozilla.org/en-US/docs/Web/CSS/:host

<hr>

## IV-C. Adding attributes

- Here we are going to utilize the `connectedCallback()` lifecycle method to render the values of 2 attributes into our `<igm-footer>`
- Add this code to the `class` definition AFTER (not inside) the `constructor()`

```js
// 5 - called when the component is added to the page
connectedCallback(){
  this.render();
}

// 6 - a helper method to display the values of the attributes
render(){
  // grab the attribute values, and assign a default value if necessary
  const year = this.getAttribute('data-year') ? this.getAttribute('data-year') : "1995";
  const text = this.getAttribute('data-text') ? this.getAttribute('data-text') : "Nobody";
	
  this.shadowRoot.querySelector("span").innerHTML = `&copy; Copyright ${year}, ${text}`;
}
```

- reload the page, and you will now see an updated version of the `<igm-footer>` with default values for `year` & `text`

<hr>

## IV-D. Passing attribute values to components

- Easy! Our code is looking for `data-year` and 'data-text'
- Note: here we are following the [custom data attributes](https://developer.mozilla.org/en-US/docs/Learn/HTML/Howto/Use_data_attributes) naming conventions, even though we don't have to, so that our attribute names don't collide with existing ones
- Go ahead and pass in unique values to your 4 `<igm-footer>` elements for `data-year` and `data-text`

```html
<h2>1st footer</h2>
<igm-footer data-year="2019" data-text="Ace Amway"></igm-footer>

<h2>2nd footer</h2>
<igm-footer data-year="2020" data-text="Babs Babcock"></igm-footer>

<h2>3rd footer</h2>
<igm-footer data-year="2021" data-text="Chris Crinkle"></igm-footer>

<h2>4th footer</h2>
<igm-footer></igm-footer>
```

## IV-E. Show that the Shadow DOM is in fact encapsulated from the regular DOM

- To prove that the CSS we write in the main document will NOT be able to effect the component Shadow DOM do the following:
  - add this HTML to the top of the `<body>` tag - `<span>I am a span</span>`
  - add this CSS to the `<head>`section of the document:

```html
<style>
span{
  color:red;
}
</style>
```


## XX. Wrap Up

- This might seem like we've done a lot of work above for this simple component, but as we add more capabilities to these web components you will hopefully see the benefits!

<hr>

## XX. Completed Version

![screenshot](_images/_web-components/HW-wc-XX.png)

<hr>

## XX. Submission

- Putting your files in a containing folder named  **wc-1/** probably makes sense
- See the dropbox for submission instructions


<hr><hr>

| <-- Previous Unit | Home | Next Unit -->
| --- | --- | --- 
|   :-\  |  [**IGME-330**](../README.md) |  [**HW - Web Components II**](HW-wc-2.md)
