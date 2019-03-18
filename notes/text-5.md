# 5 - Context-free Grammars

## I. Overview

- Today we will look at creating generative text using the RiTa library
- Creating text that isn't just random gibberish requires specifying a *grammar*
- What's a grammar? 
  - *In formal language theory, a grammar is a set of production rules for strings in a formal language. The rules describe how to form strings from the language's alphabet that are valid according to the language's syntax. A grammar does not describe the meaning of the strings or what can be done with them in whatever context — only their form.* - https://en.wikipedia.org/wiki/Formal_grammar
  - Grammar is the “language of languages”. Behind every language, there is a grammar that determines its structure
  - A language could be a human language, or a computing language like JavaScript
  - A *Context-Free Grammar* is a set of rules that define the syntax of a language — what is and is not a valid sequence of *tokens*
  - Natural languages can be described using [Context-sensitive grammars](https://en.wikipedia.org/wiki/Context-sensitive_grammar), a concept introduced by Noam Chomsky in the 50s.

<hr><hr>

## II. Demo Start File


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
	<button>Expand Grammar from &lt;start> symbol !</button>
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

- load the page - the text will be "It was a dark and stormy night."
- click the button. You will get rsults like "It was a bright and dry twilight." and "It was a cloudy and wet afternoon."

## III. Discussion

- Grammars consist of an alphabet of *terminal* and *non-terminal* characters

<hr><hr>

**[Previous Chapter <-  The RiTa.js Computational Text Library (Part IV)](text-4.md)**
