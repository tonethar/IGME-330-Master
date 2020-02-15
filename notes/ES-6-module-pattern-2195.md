# ES6 Module Pattern

## Contents
<!--- Local Navigation --->
I. [Why do we need modularized code?](#section1)

II. [ES6 Module Syntax](#section2)

III. [Try it out!](#section3)

IV. [In-class Demo](#section4)

V. [Homework](#section5)

VI. [Reference](#section6)

VII. [Review Questions](#section7)

<hr>

<a id="section1">

## I. Why do we need modularized code?
Applications that are written in a **modular** fashion are [loosely coupled](https://en.wikipedia.org/wiki/Loose_coupling), with minimal [dependencies](https://en.wikipedia.org/wiki/Dependency_hell) between modules, which makes the process of designing and maintaining them much easier and less error prone. 

**Modular programming** is the process of subdividing a computer program into separate sub-programs. Modules have the following characteristics:
- enforce logical boundaries between components and improve maintainability
- are implemented through *interfaces* (i.e. publicly available methods or properties)
- are designed in such a way as to minimize *dependencies* between different modules

Writing modular code has many benefits:
- it allows many programmers to collaborate on the same application because a small team deals with only a small part of the entire code
- the same code can be used in many applications
- errors can easily be identified, as they are localized to a file, class or function
- the scoping of variables can be easily controlled

The above is adapted from https://www.techopedia.com/definition/25972/modular-programming

We have been getting away with writing "non modular" JavaScript code so far because our programs have been fairly small. But as the size of the program increases, and if more than one developer works on an application, a modular programming architecture becomes essential.

**Today we will apply ES6 module syntax to an application and see these benefits in action.**



<hr>

 <a id="section2">

## II. ES6 Module Syntax

[Exploring ES6](http://exploringjs.com/es6/ch_modules.html#sec_overview-modules) has a nice overview of ES6 modules:

- JavaScript has had modules for a long time - however, they were implemented via libraries, not built into the language
- ES6 is the first time that JavaScript has built-in modules
- ES6 modules are stored in files
- ***There is exactly one module per file and one file per module***

### II-A. `export` and `import`
[export](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements/export) is used when creating JavaScript modules to export functions, objects, or primitive values from the module so they can be used by other programs with the import statement.

[import](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements/import) is used to import *bindings* (to functions, objects or primitive values) which are exported by another module.

<a id="important-restrictions"/>

### II-B. \*\* Important Restrictions \*\*

ES6 modules have 2 restrictions:
- as of Spring 2020, they are supported only by recent versions of all major browsers - see this compatibility chart: https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements/import#Browser_compatibility)
- they need be hosted on a web server to function, and thus won't work if opened from the desktop of your computer. How can you deal with this restriction?
  - Most IDEs have a "Live Preview" or "Live Server" mode that launches a web server. Figure out how to get than working for your preferred tool
  - Put all of your files on banjo and test them from there (kinda a pain to do all the time)
  - Use Python and the `SimpleHTTPServer` module to launch a web server locally - installation and usage instructions are here (the lab machines already have Python installed) -->  https://developer.mozilla.org/en-US/docs/Learn/Common_questions/set_up_a_local_testing_server
  - If you are familair with node and npm, check out the `http-server` module (but be sure to turn off caching with `http-server -c-1`) --> https://www.npmjs.com/package/http-server


<hr>

<a id="section3">
	
## III. Try it out!
	
### III-A. Working example
Here is our first module - we are exporting (i.e. making public and visible) the `addTextToBody()` function, but not the `myPrivateFunction()` function.

**js/utilities.js**

```javascript
export function addTextToBody(text) {
  const div = document.createElement('div');
  div.textContent = text;
  document.body.appendChild(div);
}

function myPrivateFunction(){
  console.log("privateFunction() is not visible outside of utilities.js!");
}
```

We could also write the `export` this way:

```javascript
function addTextToBody(text) {
  const div = document.createElement('div');
  div.textContent = text;
  document.body.appendChild(div);
}

function myPrivateFunction(){
	console.log("privateFunction() is not visible outside of utilities.js!");
}

export {addTextToBody};
```

To use this module from an HTML page, we do the following:

**test.html**
```html
<!DOCTYPE html>
<html lang="en">
<head>
	<meta charset="utf-8" />
	<title>ES6 Module Tester</title>
</head>
<body>
<script type='module'>
  import {addTextToBody} from './js/utilities.js';
  addTextToBody('ES6 modules are functioning!');
</script>
</body>
</html>
```

Be sure to note the following in *test.html*:
- Note we have added an attribute  of `type='module'` --> `<script type='module'>`
- it is not necessary to "import" the *utilities.js* JS file with a &lt;script> tag - as the `import` statement is doing that for us
- we have to explicitly import the `addTextToBody()` function to use it

Try it out:
- here - https://igm.rit.edu/~acjvks/courses/shared/330/es6-modules/es6-module-tester/test.html
- test it: You should see - "ES6 modules are functioning!" - in the browser window (if you don't, check the console)
- note: the above example was adapted from here: https://jakearchibald.com/2017/es-modules-in-browsers/
- for your convenience, here are the completed files in a ZIP --> [ES-6-module-tester.zip](./_files/ES-6-module-tester.zip) --> recall that these need a web server to run, [see above](#important-restrictions)

<hr>

### III-B. Checking the web inspector

If we add two breakpoints and step through the code, we can see that we now have "Module" scope and privacy:

**test.html**

Here in *test.html*, the `myPrivateFunction()` is not visible:

![Screenshot](_images/canvas-sprites-ES-6-modules-3.jpg)


**js/utilities.js**

But here in *utilities.js*, both functions are visible:

![Screenshot](_images/canvas-sprites-ES-6-modules-4.jpg)


<hr>

### ** *Try This* **
In *test.html*:
- attempt to call `myPrivateFunction()` - what error message do we get?

<hr>

<a id="section4">

## IV. In-class Demo

- Here is our decidedly "not modular" start code
- Go ahead and download, save it, and open in in Chrome
- The walkthough instructions will then be right in front of you!

**greeter-app-globals.html**
```html
<html>
<head>
	<title>Greeter App with Globals</title>
	<style>
		body{
			font-family:sans-serif;
		}
		
		button,input{
			font-size:1.2em;
		}
		
		li{
			margin-bottom:1em;
		}
		
		code{
			font-size:1.3em;
			color:green;
		}
	</style>
</head>
<body>
	<h1>???</h1>
	<input id="firstName" placeholder="Type in your first name">
	<input id="lastName" placeholder="Type in your last name">
	<p>
		<button id="greetButton">Greet Me</button>
		<button id="shoutButton">Shout at Me!!!</button>
	</p>
	<p id="output">???</p>
	<hr>
	<h2 id="instructionsHeading">???</h2>
	<p id="instructions">???</p>
	
	<h3>Step #1 - What does the start code look like?</h3>
	<ol type="A">
		<li>In a web browser, test this app, and then look over the HTML/CSS and JS code.</li>
		<li>In the console, test the <code>greetify()</code> and <code>shoutify()</code> functions with <code>greetify("Fred Jones")</code> and <code>shoutify("Norville Rogers")</code></li>
		<li>Open up the debugger, put in a breakpoint near the bottom of the &lt;script> tag:
			<ul>
				<li>What is the <i>scope</i> of <code>appData</code>?</li>
				<li>What is the <i>scope</i> of all 5 functions?</li>
			</ul>
		</li>
	</ol>
	
	
	<h3>Step #2 - Let's move the JS to external files</h3>
	<ol type="A">
		<li>Create a new folder named <b>greeter-app-modular</b></li>
		<li>Rename this HTML file to <b>index.html</b> and move it into the <b>greeter-app-modular</b> folder</li>
		<li>Change the &lt;title> of <b>index.html</b> to "Greeter App ES6 Modular"
		<li>In the <b>greeter-app-modular</b> folder, create a new folder named <b>src</b> and put the following 3 text files, with the designated content, into it: 
			<ul>
				<li><b>loader.js</b> - this file is where the <code>window.onload = init</code> loading code goes. This is also a good place to load fonts, images, and so on.</li>
				<li><b>main.js</b> - this is where the "main" functionality that is specific to this app goes. That means <code>appData</code>, <code>init()</code>, <code>greetButtonClicked()</code> and <code>shoutButtonClicked()</code></li>
				<li><b>utils.js</b> - this is where we put more generalized code, usually "pure functions", that can be re-used from project to project. That means that the <code>greetify()</code> and <code>shoutify()</code> functions go here. </li>
			</ul>
		</li>
	</ol>
	
	<h3>Step #3 - Hook up the external files</h3>
	<ol type="A">
		<li>Create 3 &lt;script> elements that will point at these 3 JavaScript files. Put these &lt;script> elements in the &lt;head> section of <b>index.html</b>:
			<ul>
				<li>Note: Loading order matters here - the &lt;script> elements must appear in the HTML in the correct order: <b>utils.js</b>, <b>main.js</b>, then <b>loader.js</b></li>
			</ul>
		</li>
		<li>While we are at it, create a folder named <b>styles</b>, and move all of the style information from the HTML file into an external style sheet named <b>default-styles.css</b>. Put <b>default-styles.css</b> into the folder we just created.  Now &lt;link> to it from <b>index.html</b></li>
		<li>Delete all the &lt;script> and &lt;style> tags from the HTML file.
		<li>Reload the page. Everything should work as before: 
			<ul>
				<li>But ... if we check the debugger, we'll see that all of the functions and variables are still kludged together in global or script scope</li>
			</ul>
		</li>
	</ol>
	
	<h3>Step #4 - Turn the JS files into ES6 modules</h3>
	<ol type="A">
		<li>Delete the <b>utils.js</b> and <b>main.js</b> &lt;script> tags from <b>index.html</b></li>
		<li>Add <code>type="module"</code> to the <b>loader.js</b> &lt;script> tag</li>
		<li>Add the following code to the <i>bottom</i> of <b>utils.js</b>: <code>export {greetify,shoutify};</code>
			<ul>
				<li>Now these 2 functions are "public" because they are being exported</li>
			</ul>
		</li>
		<li>Add the following code to the <i>top</i> of <b>main.js</b>: <code>import * as utils from "./utils.js";</code>
			<ul>
				<li><code>utils</code> is now the <i>namespace</i> we need to use when we call <code>greetify()</code> and <code>shoutify()</code> from this module (ex. <code>utils.greetify()</code>)</li>
				<li>Go ahead and change the code in the button event handlers to use the <code>utils</code> namespace</li>
			</ul>
		</li>
		<li>Add the following code to the <i>bottom</i> of <b>main.js</b>: <code>export {init};</code>
			<ul>
				<li>Now the <code>init</code> function is "public" because it it being exported</li>
			</ul>
		</li>
		
		<li>Add the following code to the <i>top</i> of <b>loader.js</b>: <code>import * as main from "./main.js";</code>
			<ul>
				<li>Now modify the code to use the <code>main</code> namespace</li>
			</ul>
		</li>
		<li>Go back and check your typing. Also, get rid of any <code>"use strict;"</code> declarations, you don't need them anymore as ES6 module code runs in strict mode by default</li>
		<li>Now load <b>index.html</b> into Chrome - make sure this is running on a web server - and the app should work as before. If not, check the console and your typing</li>
	</ol>
	
	<h3>Step #5 - Head to the console</h3>
	<ol type="A">
		<li>Open the console, and see how the scope of the variables and functions has changed.</li>
		<li>Place a breakpoint in <b>loader.js</b> and check out the <code>main</code> module - what functions are visible in the debugger?</li>
		<li>Test the <code>greetify()</code> and <code>shoutify()</code> in the console - <code>greetify("Fred Jones")</code> & <code>utils.greetify("Fred Jones")</code> - FAIL!  - which is what it's supposed to do</li>
	</ol>
	
	<hr>
	<p><b><i>Going forward, this is how we are writing code in this class for the rest of the semester. This is how Project 2 and Project 3 must be structured!</i></b></li>
	<hr>
	
	<script>
	"use strict";
	
	window.onload = init;
	
	const appData = {
		appHeadingText: "Greeter App",
		appInstructionsHeading: "Instructions for this exercise",
		appInstructionsText: "We are going to refactor the code in this example so that all the JS is placed in multiple ES6 modules, and has been moved to external files:"
	};
	
	function init(){
		document.querySelector("h1").innerHTML = appData.appHeadingText;
		document.querySelector("#instructionsHeading").innerHTML = appData.appInstructionsHeading;
		document.querySelector("#instructions").innerHTML = appData.appInstructionsText;
		
		document.querySelector("#greetButton").onclick = greetButtonClicked;
		document.querySelector("#shoutButton").onclick = shoutButtonClicked;
	}

	function greetButtonClicked(){
		let firstName = document.querySelector("#firstName").value;
		let lastName = document.querySelector("#lastName").value;
		output.innerHTML = greetify( `${firstName} ${lastName}` );
	}
	
	function shoutButtonClicked(){
		let firstName = document.querySelector("#firstName").value;
		let lastName = document.querySelector("#lastName").value;
		output.innerHTML = shoutify( `${firstName} ${lastName}` );
	}
	
	function greetify(fullName){
		let greetings = ["Hello", "Hi", "Bonjour", "Guten tag", "Hola", "Shalom", "Salve"];
		let randomGreeting = greetings[Math.floor(Math.random() * greetings.length)];
		return `${randomGreeting} ${fullName}`;
	}
	
	function shoutify(fullName){
		let exclamations = ["!", "!!", "!?!", "?!!", "@#$%!", "???", "!!!"];
		let randomExclamation = exclamations[Math.floor(Math.random() * exclamations.length)];
		return `Hey ${fullName} ${randomExclamation}`.toUpperCase();
	}
	
	</script>
</body>
</html>
```

<hr>

<a id="section5">

## V. Homework

 - Now it's your turn:
   - take the ["Sprity" HW](https://github.com/tonethar/IGME-330-Master/blob/master/notes/canvas-6.md#homework) and refactor it to use ES6 modules
   - create the following modules: **classes.js**, **utils.js**, **main.js** and **loader.js**
   - see myCourses for submission instructions

<hr>

<a id="section6" />
	
## VI. Reference
- What's a *namespace*?
  - https://en.wikipedia.org/wiki/Namespace
- ES6 Module resources
  - https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements/import
  - https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements/export
  - http://exploringjs.com/es6/ch_modules.html#sec_mixing-named-and-default-exports
  - http://2ality.com/2014/09/es6-modules-final.html
  - https://jakearchibald.com/2017/es-modules-in-browsers/\
  - https://hacks.mozilla.org/2015/08/es6-in-depth-modules/
  - https://blogs.windows.com/msedgedev/2016/05/17/es6-modules-and-beyond/
  - https://www.ecma-international.org/ecma-262/6.0/#sec-imports


<a id="section7" />

## VII. Review Questions
1. Define the software development term *loosely coupled*.
2. Give 3 advantages of using modules when coding substantial JavaScript applications.
3. Give 3 things that could go wrong if you don't use modularized code.
4. Is the `"use strict"` declaration necessary for ES6 modules to run in strict mode?

### VII-A. \*\* Hey, what about all the IIFE stuff? \*\*

- Is the IIFE stuff we just did for Project 1 *useless*?
- Not at all! Many JavaScript libraries still use the exact same technique that we did with **abcLIB.js** (i.e. *IIFE and a single global variable*)
  - And you will continue to use JS libraries (either written by you or otherwise) in your JS projects
- Wrapping **index.js** into an IIFE is also still useful, but if we have multiple modules (files) of code, this approach doesn't work so well - use the ES6 module pattern instead!
- But what about supporting older browsers? The ES6 module pattern only works on recent browsers?
  - we can address this issue by using *transpiling*, which translates code from ES6 back into ES5 for the older browsers
  - later on in the semester we'll use a node package called [webpack](https://www.npmjs.com/package/webpack) to do this
