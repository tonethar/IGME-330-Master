# HW - Ajax-7 - Promises

## I. What's a `Promise()`?

- A Promise is a JS object that "wraps" an asynchronous function 
- When a promise successfully completes, it runs its `resolve()` method, which will trigger `.then()`
- When a promise fails, it runs its `reject()` method, which will trigger `.catch()`

<hr>

## II. Start Code

**promise-demo-start.html**

```html
<!DOCTYPE html>
<html lang="en">
<head>
	<meta charset="utf-8" />
	<meta name="viewport" content="width=device-width, initial-scale=1, user-scalable=no">
	<title>Promise Demo</title>
	<style>
	body{
	  font-family: sans-serif;
	}
	button{
		font-size: 1.2rem;
	}
	</style>

</head>
<body>
	<h2>Promise Demo</h2>
	<hr>
	<button id="my-button">Make a Promise</button> <-- Click button
	<h3>Results</h3>
	<div id="output">???</div>

<script>
"use strict";
const output = document.querySelector("#output");
const myButton = document.querySelector("#my-button");

myButton.onclick = () => {
	output.innerHTML = "... waiting 2 seconds to resolve promise ...";
	
	// I. Make a promise
	let promise = new Promise((resolve, reject) => {
	
		// I-A. get a random letter
		const randomLetter = "ABCDEFGHIJKLNMOPQRSTUVWXYZ".split("")[Math.floor(Math.random() * 26)];

		// In 2 seconds, "resolve" the Promise
		// call resolve() and pass in the random letter we want to send when .then() runs
		window.setTimeout(() => {
			resolve(randomLetter);
			console.log("... 2 seconds later ...")
			console.log(`Promise was just resolved - randomLetter = ${randomLetter}`);
			console.log("Promise was just resolved", promise);
		}, 2000);
	}); // end new Promise
	
	console.log("Promise created ", promise);
	 
}; // end .onclick

</script>
</body>
</html>
```

<hr>

## III. `resolve()` and `promise.then()`

- Go ahead and run the code above, you will see from the console logs that the promise is originally *pending* right after it was created, and it then show as *fulfilled* after 2 seconds when the `resove()` method is fired
- However, outside of these console logs, our program is unaware that the promise has resolved and what value (a random letter) has been sent
- Add the following code to the end of the promise (where there is a `// end new Promise` comment)

```js
.then(text => { // run if "resolved"
  console.log("In promise.then()", promise);
  output.innerHTML = `Here's a letter: <b>${text}</b>`; 
});
```

- Run the code again and you will see that when the promise *resolves*, the `.then()` method is triggered, the callback function is invoked, the random letter is passed in as the `text` variable, and the page is updated by the code
- In the 3 `promise` logs, you can see the "life cycle" of this promise


### IV. `reject()` and `promise.catch()`

- Right now our promise always succeeds, which isn't very realistic. In the real world, a promise might fail if `fetch()` returned a 404 page, or if the server timed out or was offline, or if the wrong password was used to access mongo database. All of the hypotheticale examples would cause the promise to `reject()`
- Let's add a `reject()` condition to simulate an error - we'll use `Math.random()` to have our "random letter" promise arbitrarily fail about 1/3 of the time
- add this code to the `window.setTimeout()` handler, right at the top *before* the call to `resolve()`

```js
if(Math.random()<.333) reject("Nah, I don't have a letter for you this time!");
```

- Test it a few times, 



<hr><hr>

| <-- Previous Unit | Home | Next Unit -->
| --- | --- | --- 
|   [**HW - Ajax VI**](HW-ajax-6.md)  |  [**IGME-330**](../README.md) | :-\
