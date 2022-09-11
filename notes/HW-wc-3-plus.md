# Web Component 3 - enhanced

- Let's make some improvements to Web Components 3

## I. Fix the components so that they follow the spec

- The `sw-card` and `sw-header` code does not reflect a best practice for creating web components, which regards what kind of code belongs (and doesn’t belong) inside of web component class constructors:
  - "The element’s attributes and children must not be inspected"
  - "The element must not gain any attributes or children"
  - "In general, work should be deferred to `connectedCallback` as much as possible"
  - The above is detailed in the web component specification here: https://html.spec.whatwg.org/multipage/custom-elements.html#custom-element-conformance
- This means that some of the code we put in the `sw-card` and `sw-header` `constructor()` method, should instead be moved to the top of their respective `connectedCallback()` methods

### I-A. Fix `sw-header`



## II. Keep track of our Star Wars cards in an array

## III. Persisting application state

## IV. The `SWApp` component - one component to rule them all!
