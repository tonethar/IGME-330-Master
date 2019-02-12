# Demo - IIFE - *Immediately Invoked Function Expression*

## I. Overview
- Up until now, we have been writing all of our JS code in the top-level of &lt;script> tags, which leads to many issues which we will demonstrate in the demo below:
  1. variables declared with `var` end up in the global scope with the entirety of the browser API, so there is a serious risk of our variable names conflicting and/or overwriting existing symbols
  2. functions declared with `function` end up in the global scope with the entirety of the browser API, so the danger is the same as above
  3. variables or functions declared with `let` or `const` end up in a "global-ish" scope called "script scope". If we have an application with multiple script files where variable names are the same, these duplicate variable declarations will cause a run-time error
  4. code in global or script scope can easily be run directly from the console by *anybody*. While this is great for teaching and debugging code, imagine how a variable like *highscore* could get abused by your players 

## II. The IIFE is a simple and effective solution
- The [JavaScript IIFE](https://developer.mozilla.org/en-US/docs/Glossary/IIFE) (*Immediately Invoked Function Expression*) pronounced "Iffy" - which is used to keep our variables and functions out of global or "script" scope, and instead make them local to the executed function. It looks like this:

```js
(function () {
    // statements
})();
```

- so what Iffy's do is to ***create scope*** separate and distinct from the global scope
- things to try:
  - the `charlie` variables in the 2 files are now separate and distinct from each other - one is in function (local) scope, the other in global scope
  - `able` and `baker` variables in the 2 files no longer interfere with each other
  - variables in the IIFE are no longer visible from the console
- IIFEs in the wild:
  - Iffy's are commonly used in JavaScript libraries - let's go check one out:
    - In this course we will soon be using the RiTa library - which utilizies an IIFE - head to this page to see where you can download it: https://rednoise.org/rita/download.php
    - look for the **rita-full.js** - the "non-minified" version - and open it in a new window or tab, which should allow you to view the full source code in a browser window
    - scroll

## III. Demo Start Files

**iife-demo.html**
```html
<!DOCTYPE html>
<html lang="en">
<head>
	<meta charset="utf-8" />
	<title>IIFE Demo</title>
</head>
<body>
<script src="external.js"></script>
<script>
"use strict";

//let able = 10;
//const baker = 20;
var charlie = 30;

function doStuff(){
	console.log("doStuff!");
}

const doStuff2 = function(){
	console.log("doStuff2!");
}

const doStuff3 = _ => {
	console.log("doStuff3!");
}

console.log("-----iife-demo.html-----");
doStuff();
doStuff2();
doStuff3();
doStuff4(); // declared externally

console.log(`able=${able}`);
console.log(`baker=${baker}`);
console.log(`charlie=${charlie}`);
debugger;

</script>
</body>
</html>

```

**external.js**

```js
console.log("-----external.js-----");
let able = 100;
const baker = 200;
var charlie = 300;

function doStuff(){
	console.log("external.js -> doStuff!");
}

function doStuff4(){
	console.log("external.js -> doStuff4!");
}

console.log(`able=${able}`);
console.log(`baker=${baker}`);
console.log(`charlie=${charlie}`);
```
