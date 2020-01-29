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
- You might hear someone say (even here at RIT) "no one uses IIFE's!". This is untrue:
  - IIFEs are still used by many (most?) of the popular JS libraries such as [jQuery](https://jquery.com) and [RiTa.js](https://rednoise.org/rita/)
  - When node packages such as [webpack](https://www.npmjs.com/package/webpack) (which we will learn about later in the semester) *transpile* (which we will learn about later in the semester) code from ES6 to ES5, the resulting code is wrapped in an IIFE
- BTW: When you are done with this page, you can get more IIFE review here --> [IIFE-review.md](./IIFE-review.md)


## II. Sample Code

- A ZIP file of these 4 examples is linked here --> [IIFE-examples.zip](./_files/IIFE-examples.zip)

**IIFE-0.html**

- We'll start off by putting 2 variables  - `playerName` & `highScore` - into global browser scope
- Imagine that this is a part of a game you made, and you wanted to keep track of and store the name and high score of the player
- Go ahead and load this example into a browser, and then change the values of these variables in the console - NOT good!
- *But how can we get our code out of the global namespace so that the user can't mess with these values?*

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

<hr>

**IIFE-1.html**

- Below we made an IIFE and declared the variables inside of it
- Now `highScore` and `playerName` are now variables of the IIFE, and thus NOT accessible from this outside scope
- This is a quick and easy technique to get your code out of the global namespace and safe from malicious users
- *But what if we have code that needs access to these values, without being able to modify them?*

```html
<!DOCTYPE html>
<html lang="en">
<head>
	<meta charset="utf-8" />
	<title></title>
</head>
<body>
<script>
(function(){
  let playerName = "Mario";
  let highScore = 1000;
})();

// `highScore` and `playerName` are now local variables of the IIFE, and thus NOT 
// accessible from this outside scope
// (but what if we have code that needs access to these, without being to modify them?)
console.log(playerName,highScore);
</script>

<p>
  Use an IIFE - everything is private
</p>
</body>
</html>
```

<hr>

**IIFE-2.html**

- Below, we use an IIFE for data privacy - but `return` everything that needs to be public to a variable named `scoreTracker`


```html
<!DOCTYPE html>
<html lang="en">
<head>
	<meta charset="utf-8" />
	<title></title>
</head>
<body>
<script>
  let scoreTracker = (function(){
  	let playerName = "Mario"; // this is still "private"
    let highScore = 1000; 		// this is still "private"
	 
	  function privateSecretMethod(){
		  // do secret stuff
	  }
	
	  // public stuff
	  function incrementHighScore(){
		 highScore++;
	  }
	
	  function resetHighScore(){
		  highScore = 0;
	  }
	
	  function getHighScore(){
		  return highScore;
	  }
	
	// return the "public" interface
	  return {
		  incrementHighScore,
		  resetHighScore,
		  getHighScore
	  };
	
  })();

// `highScore` is NOT accessible from the outside scope
//console.log(highScore);

// what will happen here?
console.log("scoreTracker.highScore=" + scoreTracker.highScore); // ERROR or ??
scoreTracker.highScore = 2000; // ERROR or ??
console.log("scoreTracker.highScore=" + scoreTracker.highScore); // ERROR or ??
scoreTracker.incrementHighScore();
console.log("scoreTracker.highScore=" + scoreTracker.highScore); // ERROR or ??
console.log("scoreTracker.getHighScore()=" + scoreTracker.getHighScore()); 

console.log("---------------------------------------------------------------");

// let's use the "public" interface of `scoreTracker`
scoreTracker.incrementHighScore();
console.log("scoreTracker.getHighScore()=" + scoreTracker.getHighScore()); 
scoreTracker.resetHighScore(); 
scoreTracker.incrementHighScore();
console.log("scoreTracker.getHighScore()=" + scoreTracker.getHighScore()); 

</script>
<p>
Use an IIFE for privacy - but `return` everything that needs to be public to a variable named `scoreTracker`
</p>
</body>
</html>
```

<hr>

**IIFE-3.html**

- Instead of exporting the "public interface" to a variable, we are instead going to export a single variable named `scoreLIB` to the browser's global scope. This code will otherwise behave the same as the previous example.
- Exporting a single variable to the global namespace and attaching all of the desired functionality to it, is how many of the popular JS libraries such as jQuery and RiTa.js work.


```html
<!DOCTYPE html>
<html lang="en">
<head>
	<meta charset="utf-8" />
	<title></title>
</head>
<body>
<script>
(function(){
	let playerName = "Mario"; // this is still "private"
	let highScore = 1000; 	 // this is still "private"
 
	function privateSecretMethod(){
		// do secret stuff
	}

	// public stuff
	function incrementHighScore(){
	 highScore++;
	}

	function resetHighScore(){
		highScore = 0;
	}

	function getHighScore(){
		return highScore;
	}

	// expose the "public" interface
	window["scoreLIB"] = {
		incrementHighScore,
		resetHighScore,
		getHighScore
	};

})();


// `highScore` is NOT accessible from the outside scope
//console.log(highScore);

// what will happen here?
console.log("scoreLIB.highScore=" + scoreLIB.highScore); // ERROR or ??
scoreLIB.highScore = 2000; // ERROR or ??
console.log("scoreLIB.highScore=" + scoreLIB.highScore); // ERROR or ??
scoreLIB.incrementHighScore();
console.log("scoreLIB.highScore=" + scoreLIB.highScore); // ERROR or ??
console.log("scoreLIB.getHighScore()=" + scoreLIB.getHighScore()); 

console.log("---------------------------------------------------------------");

// let's use the "public" interface of `scoreTracker`
scoreLIB.incrementHighScore();
console.log("scoreLIB.getHighScore()=" + scoreLIB.getHighScore()); 
scoreLIB.resetHighScore(); 
scoreLIB.incrementHighScore();
console.log("scoreLIB.getHighScore()=" + scoreLIB.getHighScore()); 

</script>
<p>
Here we will export an object - `scoreLIB` - into the global (window) namespace. This will work in a similar fashion to the previous example. This is how many of the popular JS libraries such as jQuery and RiTa.js work.
</p>
</body>
</html>
```

## III. Resources
- https://medium.com/@vvkchandra/essential-javascript-mastering-immediately-invoked-function-expressions-67791338ddc6
- https://flaviocopes.com/javascript-iife/

