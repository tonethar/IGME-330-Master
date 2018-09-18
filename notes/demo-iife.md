# IIFE Demo

## I. Overview


## II. Start Files

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
//doStuff4(); // declared externally

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
