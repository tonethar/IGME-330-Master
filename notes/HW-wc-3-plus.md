# Web Component 3 - enhanced

- Let's make some improvements to Web Components 3

## I. Fix the components so that they follow the spec

- The `sw-card` and `sw-header` code does not reflect a best practice for creating web components, which regards what kind of code belongs (and doesn’t belong) inside of web component class constructors:
  - "The element's attributes and children must not be inspected"
  - "The element must not gain any attributes or children"
  - "In general, work should be deferred to `connectedCallback` as much as possible"
  - The above is detailed in the web component specification here: https://html.spec.whatwg.org/multipage/custom-elements.html#custom-element-conformance
- This means that some of the code we put in the `sw-card` and `sw-header` `constructor()` method, should instead be moved to the top of their respective `connectedCallback()` methods

### I-A. Fix `sw-header`

- First, move the following code from the `SWHeader` constructor to the top of the `SWHeader` `connectedCallback()` method:

```js
this.shadowRoot.appendChild(template.content.cloneNode(true));
this.h1 = this.shadowRoot.querySelector("h1");
this.span = this.shadowRoot.querySelector("span");
this.quotes = ["I've got a bad feeling about this ...","Will someone get this big walking carpet out of my way?!","Aren’t you a little short for a stormtrooper?","I hope you know what you’re doing.","Oh, it’s not like that at all. He’s my brother.","We have powerful friends. You’re going to regret this."];
this.currentQuote = this.randomQuote();
```

- Save the file and test it. There will be an error in the console something like this:

```js

```


## II. Keep track of our Star Wars cards in an array

## III. Persisting application state

## IV. The `SWApp` component - one component to rule them all!
