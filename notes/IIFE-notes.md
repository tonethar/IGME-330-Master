# The IIFE - "Immediately Invoked Function Expression"

## I. Overview
- Let's talk about IIFEs and what they are good for!
- Let's head right to this page:
  - https://developer.mozilla.org/en-US/docs/Glossary/IIFE
- ... which has a nice explanation of how an IIFE works, and what it is for, which is primarily:
  - to create a private scope for a module (of code)
  - to avoid "polluting" the browser's global scope
- They used to be called "Self-executing anonymous functions"
- With ES5 in a web browser, the only way to create truly *private* scope is by declaring variables and functions *inside* of an enclosing function
- IIFEs are still used by many (most?) of the popular JS libraries such as jQuery and RiTa.js


## II. Sample Code


**IIFE-0.html**

- We'll start off by putting 2 variables  - `playerName` & `highScore` - into global browser scope
- Imagine that this is a part of a game you made, and you wanted to keep track of and store the name and high score of the player

```html
<!DOCTYPE html>
<html lang="en">
<head>
	<meta charset="utf-8" />
	<title></title>
</head>
<body>
<script>
	// Imagine that you have a game, with a `playerName` and a `highScore` you are keeping track of
	// `playerName` is in "global scope" with all of the built-in browser symbols,
	// and is thus visible on this entire script, and from any other script.
	// `highScore` is in "script scope", and thus visible on this entire script, and
	// from any other script. 
	// Go ahead and change these values from the console - not too secure, eh?
	// The players can raise their high score to anything they want to!
	var playerName = "Mario";
  let highScore = 1000;
	console.log(playerName,highScore);
</script>

<p>
  No IIFE! Everything is public and visible! Go ahead and try modifying both `playerName` and `highScore` in the console!
</p>
</body>
</html>
```
