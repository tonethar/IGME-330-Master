# Final exam review

## When
- Thursday 4/26 - the end of week 14, the last day of class.
- What is covered: Everything we've covered this semester so far, either in the Study Guides, in-class exercises, or lectures/demos is fair game.

## What else?
- No make up's allowed without prior permission.
- The exam may fill up the entire class time. If you have accommodations for extra test time, I recommend you contact the testing center and have them send me an envelope so that you can take the exam at their testing location.

## Format
- True/False
- Multiple Choice
- Short Answer
- "Write some code"

## Topics

<hr>

**Before Midterm**

<hr>

### I. Canvas 
- Transformations & CTM
- Drawing State Variables
- `ctx.save()` and `ctx.restore()`
- Commonly used methods for drawing rectangles, ovals, lines, curves, etc
- pixel data/typed arrays/writing filters

### II. Web Audio
- Frequency Data
- Time Domain Data
- JS Typed Arrays

### III. DOM
- `querySelector(`) & `querySelectorAll()`
- event handlers and listeners
- working with buttons & form fields
- creating HTML:
  - `.innerHTML`
  - `document.createElement()`, `element.appendChild()`, ...
  - string concatenation & ES6 string templates 

### IV. JavaScript Concepts
- see sample questions [here - Section III-B and onward](https://github.com/tonethar/IGME-230-GDD-2018-Spring/blob/master/notes/final-exam-review.md)
- variables - `var`, `let`, `const`
- scope - function,block, global, script, module
- "hoisting" - when are variables available?
- "use strict"
- reference types v. value types
- function declarations
- function expressions
- anonymous functions
- ES6 arrow functions
- looping through arrays
- interview questions

### V. ES5 Objects
 - ES5 - Object literals 
   - `Object.seal()`
   - `Object.freeze()`
 - ES5 - Prototype-based inheritance
   - `Object.create()`
   - `Object.assign()`
 - ES5 - Revealing Module Pattern and IIFEs

### VI. JavaScript Classes and Modules
  - ES6 Classes - constructors, properties, methods, inheritance
  - ES6 - `import` and `export` and `<script type="module"></script>`
  - transpiling with Webpack
  
### VII. Canvas Sprites HW Assignments
[Canvas Sprites-0](https://github.com/tonethar/IGME-230-GDD-2018-Spring/blob/master/notes/canvas-sprites-0.md) links to more of our notes
  
<hr>

**After Midterm**

<hr>


### I. Web Services
  - How do we use and pass parameters to these web services:
    - CoinMarketCap
    - iTunes Search
    - USGS Earthquake
    - Google Maps (plus Markers and InfoWindows)
  - How does our "Random Joke" service work?
  - HTTP content-types
  
### II. Ajax
  - What is Ajax?
  - XHR API
    - strengths & limitations
  - `jQuery.ajax()`
    - strengths & limitations
    - how does it work?
    - why do we need a *callback function*?
  - XSS/DOM Injection/"Script Tag Hack"
    - strengths & limitations
    - how does it work?
  - Fetch API
    - strengths & limitations
  - CORS
    - what is it?
    - how do we configure a server to share a resource cross-domain?
    - how can we know if a web service is cross-domain?
 - Data Formats
   - Know the differences between these formats, and know how to parse them:
     - Plain Text
     - CSV
     - XML
     - JSON
     - JSON-P
    
### III. Reactive Web Frameworks
  - Data-binding the hard way:
    - DOM event listeners
    - Object property getters and setters
    - what else would we need to do to create something like Vue ouselves?
  - Vue.js
    - importing the library: development v. production mode
    - "view source" v. Web Inspector - what's the difference?
    - `Vue()` Object
      - **MVVM** pattern - "Model-View-View Model" - the `Vue()` object is the "VM" of this pattern
      - the "view model" handles the *binding* between the model and the view. It is a *value converter* that is responsible for converting the data objects from the model in such a way that objects are easily managed and presented - and it handles most of the view's display logic.
      - https://en.wikipedia.org/wiki/Model–view–viewmodel
    - `Vue()` options
      - https://vuejs.org/v2/api/#Options-Data
        - `data` - The data object for the Vue instance. Vue will recursively convert its properties into getter/setters to make it *reactive*
        - `computed` - computed properties to be mixed into the Vue instance.
        - `methods` - methods to be mixed into the Vue instance. 
      - https://vuejs.org/v2/api/#Options-DOM
        - `el`
      - https://vuejs.org/v2/api/#Options-Lifecycle-Hooks
        - `created`
      - https://vuejs.org/v2/api/#Options-Assets
      - https://vuejs.org/v2/api/#Options-Composition
      - https://vuejs.org/v2/api/#Options-Misc
    - Directives:
      - `v-model`
      - `v-for`
      - `v-text`
      - `{{ }}`
      - `v-on:click` / `@click`
      - attribute binding
      - class binding
      - all other directives - https://vuejs.org/v2/api/#Directives
    - Components:
      - `Vue.component('tag-name',{...});`
      - `props`
      - `template`
      - "hoisted" elements and the `is` solution
      - `data` - https://vuejs.org/v2/guide/components.html#data-Must-Be-a-Function
      - `methods`
      
 ### IV. A little more JavaScript
 - [Closures](./js-notes.md)
