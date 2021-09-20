# HW - Web Components-4 - Walk through a `<my-list>` web component

## I. Overview

- Let's make a useful app that consists mostly of *web components* - notes and video links are below

<hr>

## II. Start Code

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
		// for practice, you should implement add(), addAtIndex(), removeAtIndex(), clear() etc
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

- None, because right now we want you to focus on Project 1 
- Consider working on this on your own, and implementing some of the operation that were suggested in the code comments

<hr><hr>

| <-- Previous Unit | Home | Next Unit -->
| --- | --- | --- 
|  [**HW - Web Components III**](HW-wc-3.md)  |  [**IGME-330**](../README.md) | :-\
