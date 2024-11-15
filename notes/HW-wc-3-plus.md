# Web Component 3 - enhanced

- Let's make some improvements to Web Components 3

## Navigation

- [I. Fix the components so that they follow the spec](#I)

- [II. Keep track of our Star Wars cards in an array](#II)

- [III. Persisting application state](#III)

- [IV. The `SWApp` component - one component to rule them all!](#IV)

<a id="I"></a>

<hr><hr>

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
this.h1 = this.shadowRoot.querySelector("h1");
this.span = this.shadowRoot.querySelector("span");
this.quotes = ["I've got a bad feeling about this ...","Will someone get this big walking carpet out of my way?!","Aren’t you a little short for a stormtrooper?","I hope you know what you’re doing.","Oh, it’s not like that at all. He’s my brother.","We have powerful friends. You’re going to regret this."];
this.currentQuote = this.randomQuote();
```

- Save the file and test it. There will be an error in the console something like this:

```js
Uncaught TypeError: Cannot set properties of undefined (setting 'innerHTML')
at SWHeader.render (sw-header.js:70:23)
at SWHeader.attributeChangedCallback (sw-header.js:57:10)
```
- Line #70 is - `this.h1.innerHTML = title;`
- The stack trace above should provide a hint of what the problem is - `SWHeader.attributeChangedCallback()` is now being called *prior* to `SWHeader.render()`, which means that our `h1` property has not yet been initialized, and we get an error when we try to set `undefined.innerHTML`
- The fix is pretty straightforward - just write some guard code in `render()` that ensures that we don't attempt to set any properties of `this.h1` and `this.span` while they are undefined - it looks something like this:

```js
if (this.h1) this.h1.innerHTML = `${title}`;
// now do the same for this.span
```

- Test the app. It should run without errors
- Note: another way to fix this would be to get ride of the `this.h1` and `this.span` properties all together, and move the `querySelector()` calls into `render()` like this:

```js
render(){
  // ...
  const h1 = this.shadowRoot.querySelector("h1");
  if (h1) h1.innerHTML = title;
  // do same for span
}
```

### II-B. Fix `sw-card`

- As above, move the following code from the `SWCard` constructor to the top of the `SWCard` `connectedCallback()` method:

```js
this.h2 = this.shadowRoot.querySelector("h2");
this.img = this.shadowRoot.querySelector("img");
this.p1 = this.shadowRoot.querySelector("#swcHeight");
this.p2 = this.shadowRoot.querySelector("#swcMass");
this.button = this.shadowRoot.querySelector("button");
```

- Save the file and test it. There will be multiple errors in the console, complaining about `Cannot set properties of undefined` like our previous experience with `sw-header`.
- Head to `render()` and fix the code as we did about for `sw-header`

```js
render(){
  // ...
  if (this.h2) this.h2.innerHTML = name;
  // and do the same for this.p1 etc
```

<a id="II"></a>

<hr>

## II. Keep track of our Star Wars cards in an array

<a id="III"></a>

<hr>

## III. Persisting application state

<hr>

<a id="IV"></a>

## IV. The `SWApp` component - one component to rule them all!
