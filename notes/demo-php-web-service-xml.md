# Demo: PHP-driven XML Web Service

- We can use the PHP scripting language to return data in the XML format - thus creating our own web service:
  - https://en.wikipedia.org/wiki/XML

## I. Simple Web Service in XML

- This web service returns a random joke in the XML format

### I-A. The *server* code (in PHP)
I. XML Web Service

- This service is online here: http://igm.rit.edu/~acjvks/courses/2018-fall/330/php/get-a-joke-xml.php 

**get-a-joke-xml.php**

```php
<?php
/*
	Name: get-a-joke-xml.php
	Description: Returns a single random joke in XML format
	Author: Keyser Soze
	Last Modified: 11/12/2018
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

$string = "<joke>\n";
$string .= "<q>{$randomJoke['q']}</q>\n";
$string .= "<a>{$randomJoke['a']}</a>";
$string .= "</joke>";

// Sends the correct HTTP header
header("Access-Control-Allow-Origin: *");
header('content-type:application/xml');
echo $string;

?>
```

## II. XHR client code for downloading XML

- Here we will use the [XMLHttpRequest](https://developer.mozilla.org/en-US/docs/Web/API/XMLHttpRequest) (XHR) object to download the XML data
- Because CORS is turned on for our random jokes web service, XHR *will* be able to download this XML cross-domain


**get-joke-xhr-xml.html**

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="utf-8" />
  <title>Get a joke XHR/XML</title>
  <script>
  //https://developer.mozilla.org/en-US/docs/Web/API/XMLHttpRequest/Using_XMLHttpRequest
  
  	"use strict";
	const URL = "http://igm.rit.edu/~acjvks/courses/2018-fall/330/php/get-a-joke-xml.php";
	window.onload = init;
	
	function init(){
		document.querySelector("#search").onclick = getData;
	}
	
	// MY FUNCTIONS
	function getData(){
		let url = URL;
		console.log("loading " + url);
		
		// https://developer.mozilla.org/en-US/docs/Web/API/XMLHttpRequest
		let xhr = new XMLHttpRequest();
		xhr.onload = xmlLoaded;
		xhr.onprogress = e => console.log(`PROGRESS: ${e}`); 
		xhr.onerror = e => console.log(`ERROR: ${e}`); 
		
		// xhr.open(method, url, async, user, password)
		xhr.open("GET", url, true);
		xhr.send();	
	}
	

	function xmlLoaded(e){
			console.log(`LOADED: ${e}`);
			let xml = e.target.responseXML;
			console.log(`xml: ${xml}`);
			let q = xml.querySelector("q").textContent;
			let a = xml.querySelector("a").textContent;
			

		/*
			Write code to display the .q and .a properties of the joke
		*/

		let bigString = `<p><i>${q}</i></p>`;
		bigString += `<p><b>${a}</b></p>`;
		document.querySelector("#content").innerHTML = bigString;
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
