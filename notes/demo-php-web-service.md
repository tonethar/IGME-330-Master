# Demo: PHP-driven Web Service

## Overview

- We can use the PHP scripting language to return data in the JSON and JSON-P formats - thus creating our own web service:
  - https://en.wikipedia.org/wiki/JSON
  - https://en.wikipedia.org/wiki/JSONP

## I. Simple Web Service (JSON only)

- This web service returns a random joke in the JSON format
- Here is a working version: http://igm.rit.edu/~acjvks/courses/2018-fall/330/php/get-a-joke.php

### I-A. The *server* code (in PHP)

**get-a-joke.php**

```php
<?php
/*
	Name: get-a-joke.php
	Description: Returns a single random joke in JSON format
	Author: Keyser Soze
	Last Modified: 11/5/2018
*/

// $jokes contains our data
// this is an indexed array of associative arrays
// the associative arrays are jokes -  they have an 'q' key and an 'a' key
$jokes = array(
	array("q"=>"What do you call a very small valentine?","a"=>"A valen-tiny!"),
	array("q"=>"What did the dog say when he rubbed his tail on the sandpaper?","a"=>"Ruff, Ruff!"),
	array("q"=>"Why don't sharks like to eat clowns?","a"=>"Because they taste funny!"),
	array("q"=>"What did the boy cat say to the girl cat?","a"=>"You're Purr-fect!"),
	array("q"=>"What is a frog's favorite outdoor sport?","a"=>"Fly Fishing!")
);

// get a random element of the $jokes array
// there are a bunch more PHP array functions at: http://php.net/manual/en/ref.array.php
$numJokes = count($jokes);
$randomJoke = $jokes[mt_rand(0, $numJokes - 1)];

// json_encode() turns an associative array into a string of well-formed JSON
$string = json_encode($randomJoke);

// Sends the correct HTTP header
header('content-type:application/json');
echo $string;

?>
```

### I-B. The *client* code (JavaScript)

```html
TBA
```

## II. Web Service with JSON and JSON-P

- This web service accepts a parameter for a named callback function, and if one is specified, it will wrap the JSON data inside of that callback function before returning it: http://igm.rit.edu/~acjvks/courses/2018-fall/330/php/get-a-joke-2.php?callback=jsonloaded
- JSON wrapped inside of a callback funciton is called JSON-P

### II-A. The *server* code (in PHP)

**get-a-joke-2.php**

```php
<?php
/*
	Name: get-a-joke-2.php
	Description: Returns a single random joke in JSON or JSON-P format
	Author: Keyser Soze
	Last Modified: 11/5/2018
*/
if(array_key_exists('callback', $_GET)){
	$callback = $_GET['callback'];
}else{
	$callback = NULL;
}

// $jokes contains our data
// this is an indexed array of associative arrays
// the associative arrays are jokes -  they have an 'q' key and an 'a' key
$jokes = array(
	array("q"=>"What do you call a very small valentine?","a"=>"A valen-tiny!"),
	array("q"=>"What did the dog say when he rubbed his tail on the sandpaper?","a"=>"Ruff, Ruff!"),
	array("q"=>"Why don't sharks like to eat clowns?","a"=>"Because they taste funny!"),
	array("q"=>"What did the boy cat say to the girl cat?","a"=>"You're Purr-fect!"),
	array("q"=>"What is a frog's favorite outdoor sport?","a"=>"Fly Fishing!")
);

// get a random element of the $jokes array
// there are a bunch more PHP array functions at: http://php.net/manual/en/ref.array.php
$numJokes = count($jokes);
$randomJoke = $jokes[mt_rand(0, $numJokes - 1)];

// json_encode() turns an associative array into a string of well-formed JSON
$string = json_encode($randomJoke);

if ($callback){
	// Sends the correct HTTP header
	header('content-type:application/javascript');
	$string = $callback . "(" . $string . ")";
}else{
	// Sends the correct HTTP header
	header('content-type:application/json');
}

echo $string;

?>
```

### II-B. The *client* code (JavaScript utilizing `jQuery.ajax()`)

**get-a-joke-jquery-ajax-jsonp-start.html**

```html
<!DOCTYPE html>
<html lang="en">
<head>
	<meta charset="utf-8" />
 	<title>Get a joke JSONP!</title>

 <!-- Import jQuery -->
  <script src="https://code.jquery.com/jquery-1.11.1.min.js"></script>
  
  <script>
  	"use strict";
	const URL = "http://igm.rit.edu/~acjvks/courses/2018-fall/330/php/get-a-joke-2.php";
	window.onload = init;
	
	function init(){
		document.querySelector("#search").onclick = getData;
	}
	
	// MY FUNCTIONS
	function getData(){
		let url = URL;
		console.log("loading " + url);
		
		// use jQuery
	$.ajax({
		  dataType: "jsonp",
		  url: url,
		  data: null,
		  success: jsonLoaded
		});

	
	}
	
	function jsonLoaded(obj){
		console.log("obj stringified = " + JSON.stringify(obj));

	

		//document.querySelector("#content").innerHTML = bigString;
	}

 </script>
  
</head>
<body>
 <h1>Jokes!</h1>

<button type="button" id="search">Get Joke!<br />:-O</button>

<h2>Results</h2>
 <div id="content">
 <p>No data yet!</p>
 </div>
 
</body>
</html>
```


### II-C. The *client* code (JavaScript utilizing XSS)

**get-a-joke-DOM-injection-jsonp-start.html**

```html
<!DOCTYPE html>
<html lang="en">
<head>
	<meta charset="utf-8" />
 	<title>Get Joke -  DOM Injection Version</title>
 	<link href='https://fonts.googleapis.com/css?family=Audiowide' rel='stylesheet' type='text/css'>
 	<style>
 	*{
 		font-family:sans-serif;
 	}
 	
 	header{
 		background-color: crimson;
 		margin:0;
 		padding-left:5px;
 	}
 	
 	h1{
 		font-size:4.5em;
 		font-family: "Audiowide";
 		margin-top:0;
 		margin-bottom:0;
 		color:black;
 		letter-spacing:.025em;
 	}
 	
 	h2{
 		font-size:1.5em;
 		font-family: "Audiowide";
 		margin-top:0;
 		color:#eee;
 		letter-spacing:.04em;
 		white-space: nowrap;
 	}
 	
 	section>div{
 		background-color:#ccc;
 		margin:1em;
 		padding:.5em;
 	}
 	</style>

  <script>
  	"use strict";
	const URL = "http://igm.rit.edu/~acjvks/courses/2018-fall/330/php/get-a-joke-2.php";
	
	window.onload = init;
	
	function init(){
		document.querySelector("#search").onclick = search;
	}
	
	// MY FUNCTIONS
	function search(){
		// build url
		let url = URL;
		url += "?callback=jsonLoaded";
		
		
		// create <script> element and add to page
	
		console.log("loading: " + url);
	}
	

	function jsonLoaded(obj){
		console.log("obj stringified = " + JSON.stringify(obj));
		
		// get rid of <script> tag we made for this request
		
		
		let q = obj.q;
		let a = obj.a;

		
		
		document.querySelector("#content").innerHTML = bigString;
		
	}

 </script>
  
  
</head>
<body>
<header>
 <h1>Joker Finder!</h1>
 <h2>The Joke tool you can trust&reg;</h2>
</header>
	<p id='status'><i>Status: Ready to laugh!</i></p>
	<p>
		<button id="search">Search!</button>
	</p>
	<hr>
	<h3>Results:</h3>
	<p id="content">???</p>
 
</body>
</html>
```
