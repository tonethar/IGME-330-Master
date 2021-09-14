# HW - Web Components-2 - another lifecycle method

## Overview
- This time we will add the `attributeChangedCallback()` lifecycle method to our `<igm-footer>`
- The video walkthrough for this assignment is here. You will need to be logged into RIT/myCourses before you can access it:
  - HW - Web Components-2 (XX:XX)

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

<hr>

## XX. Completed Version

![screenshot](_images/_web-components/HW-wc-XX.png)

<hr>

## XX. Submission

- Putting your files in a containing folder named  **wc-2/** probably makes sense
- See the dropbox for submission instructions

<hr><hr>

| <-- Previous Unit | Home | Next Unit -->
| --- | --- | --- 
|  [**HW - Web Components I**](HW-wc-1.md)  |  [**IGME-330**](../README.md) | :-\
