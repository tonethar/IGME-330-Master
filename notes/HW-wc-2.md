# HW - Web Components-2 - more lifecycle methods

## Overview
- This time we will add the `attributeChangedCallback()` `disconnectedCallback()` lifecycle methods to our `<igm-footer>`

<hr>

## I. Changing attribute values

- Starting with one of the example files where we built `<igm-footer>` last time, add the following to HTML document's `<script>` tag:

```js
window.onload = () =>{
  // get rid of the border of the first <igm-footer> - works!
  document.querySelector("igm-footer:first-of-type").style.border = "none";
  // change an attribute of the first <igm-footer> - fails!
  document.querySelector("igm-footer:first-of-type").setAttribute("data-year",1066);
}
```

- The first line of code succeeds in getting rid of the border that we previously added with the document-level `<style>`
- The second line of code that attempts to change the value of the `data-year` FAILS - why?
  - Because when attribute values are changed from their starting values, we need to write code that detects that change, and then re-renders the DOM
- How do we do this? Easy! The `attributeChangedCallback()` lifecycle method!

<hr>

## II. Implementing `attributeChangedCallback()`

- This is easy - first, tell the component to "watch" both the `data-year` and the `data-text` attributes

```js
static get observedAttributes(){
  return ["data-year", "data-text"];
}
```

- Then, implement `attributeChangedCallback()`
- Below, we are ignoring *which* attribute has changed, and to what value. We will instead simply re-render the component's DOM whenever one of the specified attributes values changes

```js
attributeChangedCallback(attributeName, oldVal, newVal){
  console.log(attributeName, oldVal, newVal);
  this.render();
}
```

- Test the code, now the JS should work and allow the component's attributes to be changed, and those changes will be reflected in the visible values of the component
- Let's pop some breakpoints into the code so that we can see what methods are getting called, and when
- One more thing - add this to the `window.onload` handler

```js
// BTW - the `dataset` property is easier to use than `.setAttribute()`
// Add this to the `window.onload` handler
document.querySelector("igm-footer:first-of-type").dataset.text= "William the Conquerer";
```

<hr>

## III. JS in our components

- We can easily add JS to our components
- How about, everytime we click on the `<span>` that contains the year, we increase the value of the year?
- First, let's give the component default values for `data-year` and `data-text`

```js
// put this at the end of the constructor
if(!this.dataset.year) this.dataset.year = 1989;
if(!this.dataset.text) this.dataset.text = "Bill & Ted";

// This line of code will create an property named `span` for us, so that we don't have to keep calling this.shadowRoot.querySelector("span");
this.span = this.shadowRoot.querySelector("span");
```

- Add the following to the top of  `connectedCallback()`

```js
this.span.onclick = () => {
  let year = +this.dataset.year + 1;
  this.dataset.year = year;
}
```

- Implement  `disconnectedCallback()`

```js
disconnectedCallback(){
  this.span.onclick = null;
}
```

- Test it!
- PS - you can get rid of the annoying habit of the `<igm-footer>` text to keep being selected, with this CSS rule - put it in the `IGMFooter` component:

```css
user-select: none;
```

<hr>

## IV. Breakout Activity



<hr>



<hr><hr>

| <-- Previous Unit | Home | Next Unit -->
| --- | --- | --- 
|  [**HW - Web Components I**](HW-wc-1.md)  |  [**IGME-330**](../README.md) | :-\
