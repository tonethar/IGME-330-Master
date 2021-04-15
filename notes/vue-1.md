# Vue Part I - Introduction to Vue.js

[Vue.js](https://vuejs.org) is a JavaScript framework for building user interfaces.

 - it is a *reactive* framework that binds the data model and the view. Models are JavaScript objects, and when you modify them, the view (eg. the HTML) updates automatically.
 - *declarative* (see [Wikipedia - Declarative_programming](https://en.wikipedia.org/wiki/Declarative_programming)) *templates* are used to update the view - for example the handlebar syntax `<h1>{{ message }}</h1>`will display the contents of a variable named `message` inside of the &lt;h1>
 - it uses two-way *data binding* (see [Wikipedia - UI_data_binding](https://en.wikipedia.org/wiki/UI_data_binding)) to *bind* (for example) &lt;input> values to backing variables, and the value of the backing variable to the &lt;input> value - if one value changes then the other value does too
 - it also supports UI toolkits like [Bootstrap-Vue](https://bootstrap-vue.js.org)
 - Here is fantastic set of videos that cover basic and intermediate Vue.js - we are going to walk through the first few together: https://laracasts.com/series/learn-vue-2-step-by-step/episodes/1

  

  
## 0. Start File

First, we will try to demonstrate one of the problems that Vue and (other reactive frameworks) solves.

**data-binding-hard-start.html**

```html
<!DOCTYPE html>
<html lang="en">
<head>
	<meta charset="utf-8" />
	<title>Data Binding - Hard</title>
</head>
<body>
<div id="root">
	<input type="text" id="input">
	<p id="output">???</p>
</div>

<script>
let data = {
	message: "Hello world"
};

</script>
</body>
</html>
```

  
### Instructions (you try this!)
1. Use JavaScript to make the value of `data.message` appear in the form field
2. When the form field changes value, have it update `data.message`
3. When the form field changes value, the value of `data.message` should appear in the paragraph
4. Try changing the value of `data.message` in the console - what happens? FAIL!
5. Can you get the "view" to update when console changes our data model? How can you make `data.message` a "single source of truth" for the UI? (Hint: "getters" and "setters")
6. This is a lot of code to write, for just one variable!



<hr><hr>

## I. Now use Vue.js to do the same thing, with a whole lot less code.

### Demo Instructions
1. Rename **data-binding-hard-start.html** to **data-binding-vue.html**
1. import the Vue library from a CDN
1. create `Vue()` instance:
1. give it `data` property
1. give it an element
1. create input field binding with the `v-model` *directive* (which is a custom attribute)
1. test it - see the reactivity?
1. create paragraph binding with handlebar-like syntax `{{ }}` or the `v-html` or `v-text` attributes
1. test it - more reactivity
1. show binding (2 way reactivity) to `data.message` in Vue Devtools console
1. we can also access in console through `app.message`
1. the `data` object is a "single source of truth" in that it always reflects the true value
1. Take a look in the web inspector and see what the DOM looks like. Then do a "view source" and compare

#### Summary
- Create a new `Vue()` instance
- Specify data
- Bind it to an element
- add a property to `data` that you want to display in your view
- add a directive to a UI element that you want to bind to your data

<hr><hr>

## II. Vue Dev Tools
- install Vue Dev Tools for Chrome: https://chrome.google.com/webstore/detail/vuejs-devtools/nhdogjmejiglipccpnnnanhbledajbpd?hl=en
- for the Vue Dev Tools extension, turn on "Allow access to file URLs"
- look for Vue tab in Web Inspector
- change values in *Root*
- can access and change data in console through `app.message`, `$vm0` or `data.message`

<hr><hr>

## III. Vue `v-for` loops
**vue-v-for-start.html**

```html
<!DOCTYPE html>
<html lang="en">
<head>
	<meta charset="utf-8" />
	<title>v-for</title>
	<!-- development version, includes helpful console warnings -->
	<script src="https://cdn.jsdelivr.net/npm/vue@2/dist/vue.js"></script>
</head>
<body>
<div id="root">
	<p>{{name}}</p>
	<input type="text">
	<button>Add Name</button>
</div>

<script>

let app = new Vue({
	el: '#root',
	data: {
		name: 'Fred'
	}
});

</script>
</body>
</html>
```

  
### Demo Instructions
1. add an array called `names` to your data object, and populate it with 3 names 
1. use the `v-for` directive to loop through an array and display the contents, then either use the handlebars or the `v-text` directive
1. add and remove array elements in console
1. create an input field and button, and add new names to the list using an event handler (i.e. do it "old school")

  
<hr><hr>

  
## IV. Vue `v-for` loops with better button handling code

### Demo Instructions
1. rename **vue-v-for.html** to **vue-v-for-2.html**
1. now switch code to use the `v-on:click` directive (`@click` is a shortcut) instead of DOM event listeners
1. add a `methods` key to `app`, and add a `addName()` method to `app.methods`
1. we need to use `v-model` on the input field, and create a new property on our `data` model

  
<hr><hr>
  
## V. Bootstrap Vue Demo
Let's see how we can get nice looking Bootstrap components into our Vue app.

### Demo Instructions
1. rename **vue-v-for-2.html** to **vue-v-for-3.html**
1. head here to get Bootstrap-Vue CDN links: https://bootstrap-vue.org/docs/#browser
1. note how default styles of page will improve
1. we will add a badge to the page: https://bootstrap-vue.js.org/docs/components/badge
1. use a *computed property* to keep the badge updated with the number of names in our list


<hr><hr>

**[Next Chapter -> Vue Part II - Ajax and Vue.js](vue-2.md)**
