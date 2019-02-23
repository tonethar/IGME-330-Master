# 1 - Loading plain text

- Today we will first look at a number of ways for our users to load unstructured (plain) text
- We will then look at some ways to analyze and manipulate the text


## I. Loading Text

We will look at five ways to do this:


### I-A. Using &lt;input>

- Just a text input field

![screenshot]()

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
	output.innerHTML = input.value;
}

function doChange(e){
	output.innerHTML = "The input field no longer has focus, or you hit `return`!";
}

</script>
</body>
</html>
```

### I-B. Using &lt;textarea>

- Use a &lt;textarea> element for multi-line text

![screenshot]()

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
	output.innerHTML = input.value;
}

function doChange(e){
	output.innerHTML = "The input field no longer has focus!";
}

</script>
</body>
</html>

```

### I-C. Using &lt;file> input

- This example loads text files from the users hard drive

![screenshot]()

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

### I-D. Using Drag & Drop

- This example loads text files from the users hard drive, but in this case they can drag a file onto the drop target

![screenshot]()

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

### I-F. Using Drag & Drop with an HTML element

- This example loads text files that users drag from elsewhere on the page

![screenshot]()

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

### I-F. Using `XMLHttpRequest`

- `XMLHttpRequest` (XHR) is used to load files from a web server. This example will only work if deployed to a web server.

![screenshot]()

[The data files are here]()

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

## II. Demo

## III. Homework
