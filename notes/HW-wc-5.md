# HW - Web Components-5 - Dispatching Custom Events

## I. Overview

- So far we have seen that web components are an effective way to encapsulate a user interface (via HTML/CSS) & functionality (extending the `HTMLElement` class):
  - they can easily be reused on the same page - for example `<sw-card>` or between multiple pages/projects `<sw-header>`, `<my-header>`, `<my-footer>` etc
  - parameters can be passed in via HTML custom `data-` attributes, or via stanard JS object properties
- One issue that you will run into with web components (and also in other web frameworks) is how to pass information *out* of a web component:
  - how can a web component "communicate" with the rest of your app? how can it pass values to other components?
- One solution to this issue is to have a components emit a *custom event*, and then another part of your program can listen for and respond to these events:
  - the concept is the same as listening for `window.onload` or `btnSend.onclick` events, but in this case we are going to listen for `colorList.onlengthchanged` (but we'll have to use the more modern syntax istead - `colorList.addEventListener("lengthchanged", e => doStuff(e)`)
`)
  - you can get an overview of this here - [MDN-Creating and triggering events](https://developer.mozilla.org/en-US/docs/Web/Events/Creating_and_triggering_events)
- What we are trying to promote here is *loose coupling* of our software components, with minimal dependencies, which makes it easier to reuse and maintain our code
- BTW - Below we are going to demonstrate the *custom event* technique, but here are other ways to accomplish the same thing, possibly by hard coding global references in the component (BAD), or passing in function references that can be called back later when the array length changes (BETTER)

<hr>

## II. Goal

- We are going to take the `<my-list>` component from [last time](HW-wc-4.md) and give it the ability to emit a `lengthchanged` event, this event will be broadcast by the component whenever the length of the `items` array changes. We can then write code (outside of the component) that will *listen* for this event, and then update the UI with the new length

![screenshot](_images/_wc/HW-wc-12.png)

<hr>

## III. Get Started

1) Make a copy of **list-component.html** and name it **list-component-with-event.html**

2) Add a `clear()` method to the `MyList` class - it empties out the `_items` array - you can test it from the console:

```js
// type this in the browser console to test the code you wrote!
colorList.clear() // empties the `_items` array, which will be visible on the page
colorList.items // shows an empty array `[]`
```

3) Add a `length()` getter method to the `MyList` class - it returns the length of `_items` - you can test it from the console:

```js
// type this in the browser console to test the code you wrote!
colorList.length // returns number of items in list
```

4) Add some HTML to the bottom of the page:

![screenshot](_images/_wc/HW-wc-13.png)

5) Initialize the `inputText` and `outputText` variables (you won't be using the latter variable until the end of this)

![screenshot](_images/_wc/HW-wc-14.png)

<hr><hr>

| <-- Previous Unit | Home | Next Unit -->
| --- | --- | --- 
|  [**HW - Web Components IV**](HW-wc-4.md)  |  [**IGME-330**](../README.md) | :-\
