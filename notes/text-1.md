# 1 - Loading plain text

- Today we will first look at a number of ways for our users to load *unstructured* (plain) text
- We will then look at some ways to analyze and manipulate the text
- We won't need to use all of these text loading methods today - this code is a resource - "start code" - that we will come back to over the next few weeks
- N.B. - in a few weeks we will be looking at *structured* text in formats such as CSV, XML, and JSON

I. [Six ways to Load Text](#I)
  
  - A. [Using &lt;input type="text">](#I-A) for single-line text
  - B. [Using &lt;textarea>](#I-B) for multi-line text
  - C. [Using &lt;file> input](#I-C) to load local files
  - D. [Using Drag & Drop](#I-D) to load local files
  - E. [Using Drag & Drop another way](#I-E) to load text contained HTML elements
  - F. [Using XMLHttpRequest](#I-F) - (aka XHR) to load files from a web server
  
II. [Demo](#II)

III. [Homework](#III)

<hr><hr>

<a id="I"></a>

## I. Six ways to load text

- Let's look at multiple ways the user can load text into our app 

<a id="I-A"></a>

### I-A. Using &lt;input>

- a text input field for a single line of text

![screenshot](_images/text-1.png)

**load-text-input.html**

```html
<!DOCTYPE html>
<html lang="en">
<head>
	<meta charset="utf-8" />
	<title>Load Text - &lt;input></title>
	<style>
		body{font-family:sans-serif;}
	</style>
</head>
<body>
<h1>Load Text - <code>&lt;input></code> element</h1>
<section>
	<p><input id="input" type="text" size="50" maxlength="50" autofocus value="It was a dark and stormy night ..." /></p>
	<p id="output"></p>
</section>
<script>
let input = document.querySelector("#input");
let output = document.querySelector("#output");

input.oninput = doInput; // called whenever the content of the field changes
input.onchange = doChange; // called when the field loses focus or when the return key is pressed
input.dispatchEvent(new Event("input")); // calls doInput() when the page first loads

function doInput(e){
	let text = e.target.value;
	output.innerHTML = text;
}

function doChange(e){
	output.innerHTML = "The input field no longer has focus, or you hit `return`!";
}

</script>
</body>
</html>
```

<hr>

<a id="I-B"></a>

### I-B. Using &lt;textarea>

- Use a &lt;textarea> element for multi-line text

![screenshot](_images/text-2.png)

**load-text-textarea.html**

```html
<!DOCTYPE html>
<html lang="en">
<head>
	<meta charset="utf-8" />
	<title>Load Text - &lt;textarea></title>
	<style>
		body{font-family:sans-serif;}
	</style>
</head>
<body>
<h1>Load Text - <code>&lt;textarea></code> element</h1>
<section>
	<p><textarea cols="40" rows="7">It was a dark and stormy night ...</textarea></p>
	<p id="output"></p>
</section>
<script>
let input = document.querySelector("textarea");
let output = document.querySelector("#output");

input.oninput = doInput; // called whenever the content of the field changes
input.onchange = doChange; // called when the field loses focus or when the return key is pressed
input.dispatchEvent(new Event("input")); // calls doInput() when the page first loads

function doInput(e){
	let text = e.target.value;
	output.innerHTML = text;
}

function doChange(e){
	output.innerHTML = "The input field no longer has focus!";
}

</script>
</body>
</html>

```

<hr>

<a id="I-C"></a>

### I-C. Using &lt;file> input

- This example loads text files from the users hard drive

![screenshot](_images/text-3.png)

**load-text-file-input.html**

```html
<!DOCTYPE html>
<html lang="en">
<head>
	<meta charset="utf-8" />
	<title>Load Text - &lt;file></title>
	<style>
		body{font-family:sans-serif;}
	</style>
</head>
<body>
<h1>Load Text - <code>&lt;file></code></h1>
<section>
	<input type="file" id="fileChooser">
	<p id="output"></p>
</section>
<script>
let output = document.querySelector("#output");
document.querySelector("#fileChooser").onchange = doChange;


function doChange(e){
	let file = e.target.files[0]; // we are only allowing 1 file to be chosen
	let reader = new FileReader();
	reader.onload = dataLoaded;
	reader.readAsText(file);
}

function dataLoaded(e){
		let s = e.target.result;
		output.innerHTML = s;
}

</script>
</body>
</html>
```

<hr>

<a id="I-D"></a>

### I-D. Using Drag & Drop

- This example loads text files from the users hard drive, but in this case they do this by dragging and dropping a file onto the "drop target"

![screenshot](_images/text-4.png)

**load-text-drag-drop.html**

```html
<!DOCTYPE html>
<html lang="en">
<head>
	<meta charset="utf-8" />
	<title>Load Text - Drag & Drop</title>
	<style>
		body{font-family:sans-serif;}
		#dropbox{
			width:70%;
			min-height:300px;
			border:5px groove gray;
		}
		.hover{
    	background-color: rgba(0,191,165,.04);
		}
	</style>
</head>
<body>
<h1>Load Text - Drag & Drop</h1>
<section>
	<p id="dropbox">Drag a text file onto me!</p>
</section>
<script>

let dropbox = document.querySelector("#dropbox");
dropbox.ondragenter = onDragenter;
dropbox.ondragover = onDragover;
dropbox.ondrop = onDrop;


function onDragenter(e){
	e.stopPropagation();
  e.preventDefault();
 	e.target.classList.add("hover");
}

function onDragover(e){
	e.stopPropagation();
  e.preventDefault();
}

function onDrop(e){
	e.stopPropagation();
  e.preventDefault();
  e.target.classList.remove("hover");
	let file = e.dataTransfer.files[0];
	if(file){
		let reader = new FileReader();
		reader.onload = dataLoaded;
		reader.readAsText(file);
	}
}

function dataLoaded(e){
		let s = e.target.result;
		dropbox.innerHTML = s;
}

</script>
</body>
</html>
```

<hr>

<a id="I-E"></a>

### I-E. Using Drag & Drop with an HTML element

- This example loads text from elements that users drag from elsewhere on the HTML page

![screenshot](_images/text-5.png)

**load-text-drag-drop-2.html**

```html
<!DOCTYPE html>
<html lang="en">
<head>
	<meta charset="utf-8" />
	<title>Load Text - Drag & Drop 2</title>
	<style>
		body{font-family:sans-serif;}
		#dropbox{
			width:70%;
			height:300px;
			border:5px groove gray;
		}
		.draggableBox{
			width:100px;
			height:100px;
			border:3px groove red;
			padding:.2em;
		}
		.hover{
    	background-color: rgba(0,191,165,.04);
		}
		.dragging{
			opacity: .25;
		}
	</style>
</head>
<body>
<h1>Load Text - Drag & Drop 2</h1>
<section>
	<p id="dropbox">Drag some text onto me!</p>
	<p class="draggableBox" draggable="true">No good deed goes unpunished!</p>
	<p class="draggableBox" draggable="true">Tis easier to beg forgiveness than to ask permission!</p>
</section>
<script>
let draggedBox; // one of the .draggableBox above
let dropbox = document.querySelector("#dropbox");
dropbox.ondragenter = onDragenter;
dropbox.ondragover = onDragover;
dropbox.ondrop = onDrop;

document.querySelectorAll(".draggableBox").forEach(element => element.ondragstart = onDragstart);

// event for the draggableBox(es)
function onDragstart(e){
	e.dataTransfer.setData("text/plain", e.target.innerText);
	draggedBox = e.target;
	draggedBox.classList.add("dragging");
}

// events for the dropbox
function onDragenter(e){
	e.stopPropagation();
  e.preventDefault();
  e.target.classList.add("hover");
}

function onDragover(e){
	e.stopPropagation();
  e.preventDefault();
}

function onDrop(e){
	e.stopPropagation();
  e.preventDefault();
  e.target.classList.remove("hover");
  draggedBox.classList.remove("dragging");
	dropbox.innerHTML = e.dataTransfer.getData("text/plain");
}
</script>
</body>
</html>
```

<hr>

<a id="I-F"></a>

### I-F. Using `XMLHttpRequest`

- `XMLHttpRequest` (XHR) is used to load files from a web server
- This example will only work if deployed to a web server
- P.S. The data files you will need for this demo are [here](_files/data.zip)

![screenshot](_images/text-6.png)

**load-text-xhr.html**

```html
<!DOCTYPE html>
<html lang="en">
<head>
	<meta charset="utf-8" />
	<title>Load Text - XHR</title>
	<style>
		body{font-family:sans-serif;}
	</style>
</head>
<body>
<h1>Load Text - <code>XMLHttpRequest</code> - aka XHR</h1>
<section>
	<select>
		<option value="">&lt;Choose a file></option>
		<option value="data/gettysburg-address.txt">Gettysburg Address</option>
		<option value="data/call-of-cthulhu.txt">Call of Cthulhu</option>
	</select>
	<p id="output"></p>
</section>
<script>
let output = document.querySelector("#output");
document.querySelector("select").onchange = doChange;

function doChange(e){
	let xhr = new XMLHttpRequest();
	let url = e.target.value;
	if (!url) return;
	xhr.onload = dataLoaded;
	xhr.onerror = _ => "There was an error loading the file.";
	xhr.open("GET",url);
	xhr.send();
}

function dataLoaded(e){
  let s = e.target.responseText;
  output.innerHTML = s;
}

</script>
</body>
</html>
```

<hr>

<a id="II"></a>

## II. Demo

- JS String docs --> https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/String
- properties and methods we'll look at:
  - `.length`
  - `.indexOf()` - finds the first occurence of a string
  - `.substring()` - extracts a string 
  - `.replace()` - replaces part of a string
  - `.split()` - turns a string into an array
  - `.reverse()` - actually is a method of array, and it does what you think it does
  - `.join()` - turns an array into a string


<hr>

<a id="III"></a>

## III. Homework

