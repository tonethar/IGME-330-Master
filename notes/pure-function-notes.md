# Notes - What's a "Pure" function?

## I. Overview

**Some of your projects may require you to create a library or unit of "utility" functions:**
  - these are usually also defined as "pure functions", which lack "dependencies" and "side effects"
  - here's a definition --> [Wikipedia - Pure Function](https://en.wikipedia.org/wiki/Pure_function) - see #1 and #2 in the entry

## II. IGME-330 Examples

### 1) Here's a "Pure Function", it does something, and returns a value:

```js
// function flipACoinAndGetHeads()
// It doesn't have any dependencies other than the built-in Math object
// It doesn't modify any other program *state* (i.e. variables or properties of objects) in the program
function flipACoinAndGetHeads(){
  return Math.random() < 0.5; // 50% chance of returning true, 50% chance of returning false
}
```	
	
### 2) For our purposes, when we're using the canvas API, we'll call this a "Pure Function":

```js
// function drawRectangle(ctx,...)
// It doesn't have any dependencies other than the built-in Canvas API
// It DOES draw to the canvas, but ...
// it DOES NOT permanently modify any other program *state* (i.e. variables or properties of objects) in the program
function drawRectangle(ctx,...){
  ctx.save(); // save the drawing state
  // change a bunch of ctx state properties
  // do a bunch of translating, scaling, rotating
  ctx.restore(); // restore the old drawing state
}
```

### 3) This is NOT a "Pure Function":

```js
// function drawRectangle()
// it is relying on the existence of a `ctx` variable in either global or script scope
// It permanently modifies properties of `ctx`
function drawRectangle(){
  // change a bunch of ctx state properties
  ctx.fillStyle = "magenta";
  ctx.translate(100,100);
  ...
  // when the function returns, the `ctx` has been altered
}
```

### 4) This is NOT a "Pure Function" - but it IS acceptable code if it's located in index.js or main.js
	
  
```js
// function updateMainH1(text)
// it depends on a DOM element of id="titleElement"
// It permanently modifies properties of `#titleElement`
function updateMainH1(text){
  let h1 = document.querySelector("#titleElement")
  h1.innerHTML = text;
}
```
