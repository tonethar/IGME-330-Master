# 5 - Context Free Grammars

## I. Overview

<hr><hr>


## II. Demo

### II-A. Start File

- Here is is:

**rita-3.html**

```js
<!DOCTYPE html>
<html lang="en">
<head>
	<meta charset="utf-8" />
	<title>RiTa - 3</title>
	<script src="https://cdnjs.cloudflare.com/ajax/libs/rita/1.3.89/rita-full.js"></script>
	<style>
		body{font-family:sans-serif;}
	</style>
</head>
<body>
<h1>RiTa - 3</h1>
<p>Context-free grammars</p>
<section>
	<button>Expand Grammar from &lt;start> symbol!</button>
	<p id="output">It was a dark and stormy night.</p>
</section>
<script>

let output = document.querySelector("#output");
document.querySelector("button").onclick = doClick;

function doClick(){
	let grammar = new RiGrammar();
	grammar.addRule("<start>", "It was a <adj1> and <adj2> <noun>.");
	grammar.addRule("<adj1>", "bright | cold | cloudy | dark | overcast | sunny");
	grammar.addRule("<adj2>", "cold | dry | hot | stormy | wet");
	grammar.addRule("<noun>", "afternoon | day | mid-day | morning | night | twilight");

	let story = grammar.expand();
	output.innerHTML = story;
}

</script>
</body>
</html>
```




<hr><hr>

**[Previous Chapter <-  The RiTa.js Computational Text Library (Part IV)](text-4.md)**
