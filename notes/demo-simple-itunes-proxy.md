# Demo - Simple iTunes Proxy

## I. Overview

- [PHP Web Service Part V - creating a proxy server](HW-php-web-service-5.md) showed you how to write a proxy server for a ***really difficult*** to work with web service - SHOUTCLOUD!
- Most web services aren't as hard to work with as SHOUTCLOUD was - so here is an example of more typical (and simpler) proxy server below

<hr>

## II. A simple proxy server


**get-rush-songs.html** (run this locally off of your hard drive, AND off of web server. It will usually FAIL at one of these)

```html
<!DOCTYPE html>
<html lang="en">
<head>
	<meta charset="utf-8" />
	<title>Get Rush Songs</title>
	<script>
	window.onload = ()=>{
		const content = document.querySelector("#content");
	
		searchBtn.onclick = (e)=>{
			
			// 1. Clear UI
			content.innerHTML = "";

			
			// 2. Create an XHR object to download the web service
			// https://developer.mozilla.org/en-US/docs/Web/API/XMLHttpRequest/
			const xhr = new XMLHttpRequest();
			// this URL will fail
			const url = "https://itunes.apple.com/search?media=music&entity=song&term=rush";
		
			// but a PHP proxy server will succeed!
			//const url = "...../itunes-proxy.php";
			
			// 3. set `onerror` handler
			xhr.onerror = (e) => console.log(`error=${e}`);
			
			// 4. set `onload` handler
			xhr.onload = (e) => {
				const headers = e.target.getAllResponseHeaders();
				const jsonString = e.target.response;
				console.log(`headers = ${headers}`);
				console.log(`jsonString = ${jsonString}`);
				
				// update the UI by showing the joke
				const json = JSON.parse(jsonString);
				const results = json.results;
				let s = "";
				for(let r of results){
					s += `<p>${r.trackName} (${r.collectionName}) - <audio src='${r.previewUrl}' controls></p>`;
					s += "<hr>";
				}
				content.innerHTML = s;
			}; // end xhr.onload
			
			// 5. open the connection using the HTTP GET method
			xhr.open("GET",url);
			
			// 6. we could send request headers here if we wanted to
			// https://developer.mozilla.org/en-US/docs/Web/API/XMLHttpRequest/setRequestHeader
			
			// 7. finally, send the request
			xhr.send();
			
		}; // end onclick
		
	}; // end window.onload
	
	</script>
</head>
<body>
	<h1>Get Rush Songs</h1>
	<p>Try running this from your desktop AND from a web server - it will fail at at least one of these as it tries to access the iTunes web service directly because iTunes does not have CORS turned on!</p>
	<p>But if you instead utilize a PHP proxy server to download iTunes for you, it will succeed!</p>
	<button id="searchBtn">Make it so!</button>
	<hr>
	<section id="content">Click the button to do a search!</section>
</body>
</html>
```

<hr>

**itunes-proxy.php** (post this to banjo)

```php
<?php
	$term="rush"; // you will need to grab the value of $term from $_GET rather than hard-coding like we did here
	$URL = "https://itunes.apple.com/search?media=music&entity=song&term=$term";
	header('content-type:application/json');      // tell the requestor that this is JSON
	header("Access-Control-Allow-Origin: *");     // turn on CORS
	echo file_get_contents($URL);
?>
```
