# HW - Web Components-5 - Dispatching Custom Events

## I. Overview

- So far we have seen that web components are an effecive way to encapsulate a user interface (via HTML/CSS) & functionality (extending the `HTMLElement` class):
  - they can easily be reused on the same page - for example `<sw-card>` or between multiple pages/projects `<sw-header>`, `<my-header>`, `<my-footer>` etc
  - parameters can be passed in via HTML custom `data-` attributes, or via stanard JS object properties
- One issue that you will run into with web components (and also in other web frameworks) is how to pass information *out* of a web component:
  - how can a web component "communicate" with the rest of your app? how can it pass values to other components?
- One solution to this issue is to have a components emit a *custom event*, and then another part of your program can listen for and respond to these events:
  - the concept is the same as listening for `window.onload` or `btnSend.onclick` events, but in this case we are going to listen for `colorList.onlengthchanged` (but we'll have to use the more modern syntax istead - `colorList.addEventListener("lengthchanged", e => doStuff(e)`)
`)
  - you can get an overview of this here - [MDN-Creating and triggering events](https://developer.mozilla.org/en-US/docs/Web/Events/Creating_and_triggering_events)

<hr>

## II. Goal

- We are going to take the `<my-list>` component from last time and give it the ability to emit a `lengthchanged` event, this event will be broadcast by the component whenever the length of the `items` array changes. We can then write code (outside of the component) that will *listen* for this event, and then update the UI with the new length

![screenshot](_images/_wc/HW-wc-12.png)

<hr>

## III.



<hr><hr>

| <-- Previous Unit | Home | Next Unit -->
| --- | --- | --- 
|  [**HW - Web Components IX**](HW-wc-4.md)  |  [**IGME-330**](../README.md) | :-\
