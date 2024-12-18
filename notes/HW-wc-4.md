# HW - Web Components-4 - Walk through a `<my-list>` web component

## I. Overview

- This app demos how to pass array and object data to a web component, which is an issue because the values of HTML attributes must be strings:
  - https://stackoverflow.com/questions/57654383/how-to-pass-objector-associative-array-as-value-of-attribute-to-my-web-compone
- The simplest solution to this issue is to create a *property* in the component's constructor, and then set it using JavaScript. We did not end up using HTML custom attributes with this component
- Other new stuff to talk about:
  - arrays in JavaScript are passed by *reference*, but we wanted to have our component to have its own *copy* to work on
  - for that, we used the [JS spread syntax](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/Spread_syntax)
  - JS Object getter/setter syntax with a "backing" property:
    - [get](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Functions/get)
    - [set](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Functions/set)

<hr>

## II. Start Code

**list-component.html**

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="utf-8" />
  <title>&lt;my-list> Component Demo</title>
  <style>
    h1{
      font-family: sans-serif;
    }
	  
    /* https://www.w3schools.com/howto/howto_css_equal_height.asp */
    /* https://stackoverflow.com/questions/18346083/space-between-divs-display-table-cell/18346159 */
    .col-container{
      display: table;
      border-collapse: separate;
      border-spacing: 10px;
    }

    .col-container > my-list{
      display: table-cell;
      border: 1px solid black;
      width: 150px;
      max-width: 150px;
      overflow: auto;
     }	
  </style>
  <!-- Web Components Polyfill for older browsers -->
  <script defer src="https://cdnjs.cloudflare.com/ajax/libs/webcomponentsjs/2.6.0/webcomponents-loader.min.js"></script>
  <script>
  // I. <my-list> web component stuff
  const template = document.createElement("template");
	template.innerHTML = `
	<style>
		:host{
			background-color: #dfdfdf;
			display: inline-block;
			padding: .25rem;
			width: 100px;
			font-family: sans-serif;
			color: black;
		}
		h2{
			font-size: .8rem;
			text-align: center;
			margin: 0 auto .2rem auto;
		}
		ul{
			margin: 0 auto auto 16px;
			padding-left: 0;
		}
		ul li{
			font-size: .7rem;
		}
	</style>
	<div>
	<h2>???</h2>
	<ul></ul>
	<div>
	`;

    class MyList extends HTMLElement{
		constructor(){
			super();
			this.attachShadow({mode: "open"});
			this.shadowRoot.appendChild(template.content.cloneNode(true));
			this._title = "unknown title";
			this._items = ["one","two","three"];
			this.h2 = this.shadowRoot.querySelector("h2");
			this.ul = this.shadowRoot.querySelector("ul");
		}
		
		// 3 - called when the component is added to the page
		connectedCallback(){
			this.render();
		}

		render(){
			// only re-render the <h1> if we need to
			if (this.h2.innerHTML != this._title) this.h2.innerHTML = this._title; 
			// we *should* do the same thing here for the _items array - write that code if you want to
			// https://stackoverflow.com/questions/7837456/how-to-compare-arrays-in-javascript
			// https://gomakethings.com/dom-diffing-with-vanilla-js/
			this.ul.innerHTML = this._items.map(item => `<li>${item}</li>`).join("");
		}

		// Property setter/getter code
		// Good stuff here, for all of your JS objects, not just web components
		set title(val) {
			console.log(`title setter called with val = ${val}`);
			this._title = val;
			this.render();
		}

		get title(){
			console.log("title getter called");
			return this._title;
		}

		set items(val) {
			console.log(`items setter called with val = ${val}`);
			this._items = [...val]; // copy the array
			this.render();
		}
	
		get items() {
			console.log("items getter called");
			return [...this._items]; // returns a copy
		}

		add(val){
			if (val.length > 0){
				this._items.push(val);
				this.render();
			}
		}
		// ...
		// for practice, you should implement addAtIndex(), removeAtIndex(), clear() etc
	} 

	customElements.define('my-list', MyList);

	// II. Use the <my-list> component
	let	colorList,movieList;
	window.onload = () =>{
		colorList = document.querySelector("#color-list");
		movieList = document.querySelector("#movie-list");
		
		colorList.title = "Colors";
		colorList.items = ["Cyan","Magenta"];
		colorList.add("purple")
		colorList.title = "Primary Colors";

		movieList.title = "Movies";
		movieList.items = ["Citizen Kaine","Casablanca","Kind Hearts and Coronets"];
		movieList.add("Village of the Damned")
	}
  </script>
</head>
<body>
	<h1><kbd>&lt;my-list></kbd> component demo</h1>
	<main class="col-container">
		<my-list id="color-list"></my-list>
		<my-list id="movie-list"></my-list>
	</main>
</body>
</html>
```

<hr>

## III. Homework
- There is nothing you need to submit to myCourses, but the above file is the start file for [**HW - Web Components V**](HW-wc-5.md)

<hr><hr>

| <-- Previous Unit | Home | Next Unit -->
| --- | --- | --- 
|  [**HW - Web Components III**](HW-wc-3.md)  |  [**IGME-330**](../README.md) | [**HW - Web Components V**](HW-wc-5.md)
