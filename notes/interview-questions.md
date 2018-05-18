# Interview-style Questions


1. Selecting and modifying DOM elements

**interview-questions-1.html**
```html
<!DOCTYPE html>
<html lang="en">
<head>
	<meta charset="utf-8" />
	<title></title>
</head>
<body>
  <p id="content">???</p>

  <script>
  // Give at least 5 different ways to change the text of the above paragraph to 'Hello!'
  // Hint: use a variety of DOM methods, properties, and CSS selectors
  </script>
</body>
</html>
```

<hr>

2. Selecting and changing the style of DOM elements

**interview-questions-2.html**
```html
<!DOCTYPE html>
<html lang="en">
<head>
	<meta charset="utf-8" />
	<title></title>
	<style>
		.hilite{
			color: red;
		}
	</style>
</head>
<body>
  <h1>Selecting DOM Elements</h1>
  <p id="content">???</p>
  <p>Copyright 2018 Ace Coder</p>

  <script>
  // give at least 5 different ways to change the text color of the <h1> above to red
  // Hint: use a variety of DOM methods, properties, and CSS selectors, and use the `hilite` class.
  </script>
</body>
</html>
```

<hr>

3. Write functions

```html
<!DOCTYPE html>
<html lang="en">
<head>
	<meta charset="utf-8" />
	<title></title>
</head>
<body>
<script>
	
  // write code for a function named `addThem` that accepts 2 Number arguments and returns their sum
  // if no value is passed in for an argument, give it a default value of 0
	
  // 1 - ES6 function declaration style
	
  // 2 - ES6 function expression style
	
  // 3 - ES6 arrow function style
	
  // 4 - ES5 function declaration (i.e. do default arguments the hard way
	
</script>
</body>
</html>
```

<hr>

4. Search an array

**interview-questions-3.html**
```html
<!DOCTYPE html>
<html lang="en">
<head>
	<meta charset="utf-8" />
	<title></title>
</head>
<body>
<script>
	let colors = ["red","green","blue","red","green","blue"];
	
	// write code that loops through the `colors` array, looks for all instances of the string "red", 
	//  and stores them in a new array named `colors2`
	
	// 1 - use a regular `for` loop
	
	// 2 - use a `for...of`
	
	// 3 - use `array.forEach()`
	
	// 4 - use `array.find()`
	
	// 5 - use `array.filter()`
	
	// 6 - use `array.map()`

</script>
</body>
</html>

```
