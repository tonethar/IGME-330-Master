# HW - Fix The Code #1

## I. Overview
- Can you find and fix the 4 (or more) mistakes in this code? Have at it!

## II. The code

**fix-the-code-1.html**

```html
<!DOCTYPE html>
<html lang="en">
<head>
	<meta charset="utf-8" />
	<title>Fix The Code - #1</title>
	<style>
		*{font-size:1.3em;}
	</style>
	<script>
	"use strict";

	window.onload = init();
	
	function init(){
		let button = document.querySelector("myButton");
		button.onClick = showRandomNumber;
	}

	function showRandomNumber(){
		let paragraph = document.querySelector("myOutput");
		paragraph.innerHtml = "Your random number is: " + Math.random();
	}

	</script>
</head>
<body>
<button id="myButton">Click Me to see a random number between 0 and 1!</button>
<p id="myOutput">???</p>
<p>But first you'll have to fix the errors! There are at least 4 mistakes in this code - can you find and fix them all - without modifying the HTML?</p>

</body>
</html>
```
