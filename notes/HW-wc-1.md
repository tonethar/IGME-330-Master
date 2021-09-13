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

## II. Start file

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
	window.onload = () => {
	 
	};
	</script>
	
	
</head>
<body>
<h1>Web Component - with attributes and <code>connectedCallback()</code></h1>
<p>Here we have a new component, <code>&lt;igm-footer></code> that has <ode>data-year</code> and <ode>data-text</code> attributes</p>
<p>We are also utilizing the <code>connectedCallback()</code> lifecycle method, which is invoked each time the custom element is appended into a document-connected element</p>

<h2>Sub-heading I</h2>

<h2>Sub-heading II</h2>

<h2>Sub-heading III</h2>

<h2>Sub-heading IV</h2>

</body>
</html>
```

<hr>

## III. Get Started by creating a custom HTML element - `<igm-footer>`

- to create our first custom HTML element, we first need to extend the `HTMLElement` class

```js
<script>
// #1 - create a class and extend HTMLElement
class IGMFooter extends HTMLElement{
 // need some other stuff here
}
// #2 - define our new custom element so that we can use it on the page
customElements.define('igm-footer', IGMFooter);
</script>
<body>
...
<!-- #3 - use it! -->
<igm-footer></igm-footer>
...
```

<hr>

## XX. Wrap Up

- This might seem like we've done a lot of work above, for not much capability, but as we add more capabilities to these web components you will hopefully see the benefits!

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
