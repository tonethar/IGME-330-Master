# HW - Ajax-7 - JavaScript Promises

## I. What's a `Promise()`?

- A [Promise](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Promise) is a JS object that "wraps" an asynchronous function 
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

<hr>

## IV. `reject()` and `promise.catch()`

- Right now our promise always succeeds, which isn't very realistic. In the real world, a promise might fail if `fetch()` returned a `404` page, or if the server timed out or was offline, or if the wrong password was used to access mongo database. All of the hypothetical examples would cause the promise to `reject()`
- Let's add a `reject()` condition to simulate an error - we'll use `Math.random()` to have our "random letter" promise arbitrarily fail about 1/3 of the time
- add this code to the `window.setTimeout()` handler, right at the top *before* the call to `resolve()`

```js
if(Math.random()<.333) reject("Nah, I don't have a letter for you this time!");
```

- Test it a few times, at some point the code will trigger a promise `reject()`, and an *uncaught* exception will be thrown - something like `Uncaught (in promise) Nah, I don't have a letter for you this time!`
- Let's fix the code so that the exception gets caught! Add the following, right the end of your `.then()`

```js
.catch(error => { // run if "rejected"
  output.innerHTML = error;
  console.log("In promise.catch()", promise);
});
```

- run the code a few times - errors should now be caught - and the UI should be updated with the "Nah, I don't have a letter for you this time!" message

<hr>

## V. Wrap up

- Now that you have created your own promises, go back to the previous 2 Ajax units where we used `then()`, `catch()`, and `await` - do these make a little more sense now?

<hr>

## VI. Optional Extra Credit Checkoff

- This is optional
- `XHR` uses callbacks, not promises, but could you possibly wrap `XHR` code into a custom promise (written by you)?
- You betcha! 
- Your mission: Rewrite **Ajax-5** or **Ajax-6** (your choice) to use `XHR` instead of `fetch()`, and keep your promise handling code the same. This means you will need to write code that calls `resolve()` when `XHR` succeeds, and `reject()` when it fails
- There are a lot of solutions to this problem out on the interwebs, and you are allowed to utilize them for this assignment, with the following three caveats:
  - don't just copy code "whole cloth" from the web, but instead adapt it to your needs
  - make sure that you reuse most of the `XHR` code that we wrote in class, and don't just copy/paste code that you found online
  - if you end up using any of these interwebs sources to figure out this assignment, be sure to cite them in the comments files of the dropbox

<hr><hr>

| <-- Previous Unit | Home | Next Unit -->
| --- | --- | --- 
|   [**HW - Ajax VI**](HW-ajax-6.md)  |  [**IGME-330**](../README.md) | :-\
