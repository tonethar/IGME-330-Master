# Dogfinder App - Part III

- Overview: Let's improve the app page by creating "cards" for our results, and improving the styling


## I. Improve the `XHR` Error handling

- Problem: If the dog API server is down, or the user's browser is offline, the `xhr.onerror` handler will fire:
  - right now, that error handler is updating the UI with a message, but it's not turning off the button "spinner" 
  - to see this issue in action, change the beginning of the `baseURL` constant (in **app.js**) from `https` to `htt` - then do a search. Check the console to see the error message, and also note that the button spinner never turns off.
  - let's fix that!
  - Head to **ajax.js** and make the `xhr.onerror` handler look like this:
  
  <hr>
  
  ```js
  xhr.onerror = (evt) => {
    console.log(`ERROR: ${evt}`);
    callback(evt);
  };
  ``` 
  
  <hr>
  
  - also, head to **app.js**, and at the end of the `showResults()` `catch{}` block, add a `return` statement so that we bail out of the function after catching the error (can't believe I forgot that one)
  - click the button (keeping `baseURL` malformed) and you should now see "There was some kind of error!" on the page, and that the button "spinner" effect has been removed
  - make sure the app still works! Change the beginning of `baseURL` back to `https` and then click the search button - the app should function correctly as before
  
 <hr>
    
## II. Get the "limit" control working

- Most APIs have a `limit` parameter that indicates the maximum number of results you want returned
  - **Fun Fact**: why not name this `max` or `num` or ? Because of existing convention. The word "limit" actually comes from SQL - in this case the `LIMIT` clause - https://www.w3schools.com/mysql/mysql_limit.asp
  - **Another Fun Fact**: most APIs accept the "limit" parameter in the URLs' *query string* like this:
    -  `music-service.php?band=rush&limit=5`
    - but the Dog API we have chosen uses a style called [RESTful](https://www.tutorialspoint.com/restful/restful_introduction.htm) - where the parameters like `term` and `limit` are part of the URL. After doing a search, take a look in the console at the URL we are downloading, note how the `breed` and `limit` are part of the URL, and that there isn't a query string
  - Now let's get to it!
  
1) Make sure that `limitParam` is set to a value of `"1"`
  
 <hr>
    
  ```js
  let limitParam = "1";
  ```
  
 <hr>
    
2) We need to initialize the `onchange` event for the "limit" control. Add the following code to the **app.js** `init()` function:
  
 <hr>
    
  ```js
  fieldLimit.onchange = (evt) => {
    limitParam = evt.target.value;
  };
  ```
  
 <hr>
   
3) Now choose 5 on the limit control and click search - you should get 5 results back.
  
  - BTW - this was so easy to do because the `dogURL()` function handles the updating of the url with the new limit value for us

4) Go ahead and get the `fieldBreed` & `breedParam` code working if you want to, and populate the `fieldBreed` `<select>` with more dog breed HTML


  <hr>
  
 ## III. Improving the look of our results with some *card* HTML and styles
  
 ### III-A. Refactor the code
   
 - In **app.js**, put this "helper" function right before `showResults()`. Eventually, this fucntion will create a nice looking "card" for each result (dog picture) that was found:

```js
const createResultCards = (array) => {
  const html = array.map(url => `<div><img src="${url}" alt="dog"></div>`).join("");
  elementCardHolder.innerHTML = `<div class="box">${html}</div>`;
};
```

- Now head to `showResults()` and modify the code in the `if( urlArray && Array.isArray(...` statement to instead call `createResultCards()`

```js
if( urlArray && Array.isArray(urlArray) && urlArray.length > 0 ){
  // DELETE THIS LINE -> const html = json.message.map(url => `<div><img src="${url}" alt="dog"></div>`).join("");
  // DELETE THIS LINE TOO -> elementCardHolder.innerHTML = `<div class="box">${html}</div>`;
  createResultCards(json.message);
} else {
...
```
 
- Run the app - it should run as before (with our "meh" styles)

### III-B. Improve the HTML/CSS

- Below we'll be uing some Bulma card styles to radically improve the look of our results:
  - https://bulma.io/documentation/components/card/
- Let's get started ... make some changes in `createResultCards()`

1) Comment out the two lines of code

2) Write code that clears the results `<div>`, and then loops through the array of urls and extracts the breed name

```js
elementCardHolder.innerHTML = "";
for(let url of array){
  const arr = url.split("/");
  const breed = arr[arr.length - 2];
  console.log(breed);
  
}
```
 - Test it by searching for 5 dogs, you should see the breed name logged to the console 5 times
   - Recall that most APIs will have a lot more info to parse that this - but this API only gives one piece of info to work with, the url of the image!

3) Now let's create the "card" and its HTML (put this in the `for` loop) - here it is for your copy/paste pleasure:

```js
const resultDiv = document.createElement("div");
resultDiv.className = "card";
resultDiv.style = `height:300px;overflow: auto;`;
resultDiv.innerHTML = `
  <div class="card-header-title is-size-4">
    <i class="fas fa-dog mr-3"></i>
    <span style="text-transform: capitalize" id="title"></span>
  </div>
  <div class="card-content">
    <div class="card-image">
      <figure class="image">
        <img style="border:1px solid black; background-color:white; padding:7px;box-shadow: 1px 1px 2px #333; margin:.1rem; width:300px" id="image-main" src="" alt="dog">
      </figure>
    </div>
  </div>`;
elementCardHolder.appendChild(resultDiv);
```

<hr>

- Go ahead and do another search for 5 dogs, you should see 5 "empty" cards (it's a little hard to see the borders of the cards right now):

![screenshot 13](_images/_df-images/dogfinder-13.png)

<hr>

- To improve that layout, let's add a little more CSS, this time in the **app.html** file, right up in the `<style>` tag:

```css
#element-card-holder{
  display: grid;
  grid-template-columns: repeat(auto-fill, minmax(250px,1fr));
  grid-gap: 0.5em;
}
```

<hr>

- Much better!

![screenshot 14](_images/_df-images/dogfinder-14.png)

<hr>

- I imagine you'd like to see the dog image and the title on each card?
- Go ahead and do that - you can see that there's `url` and `breed` variables already initialized for you, and that all of the HTML is already inside of a template string, so all you need to do is to add a couple `${}` to the correct places

![screenshot 15](_images/_df-images/dogfinder-15.png)

<hr>

## IV. Creating a `df-resultcard` web component

### IV-A. Get started

- While the above code works fine, it's already cluttered with a lot of inline CSS styles, and if we start adding controls such as a favorites button or a close button, and a bunch of JavaScript that goes with it, the `createResultCards()` method is going to start getting pretty bloated
- So let's instead move this "card" code over to a web component!

1) Create **src/df-resultcard.js** and import it at the top of **app.js** - `import "./df-resultcard.js";`

2) In **app.js**, comment out all of the for loop code in our `createResultCards()` method, except for the first two lines that take care of initializing `breed` for us

<hr>

3) In **df-resultcard.js** - stub in a skeleton of the web component code

![screenshot 16](_images/_df-images/dogfinder-16.png)

<hr>

4) Head back to **app.js** and make `createResultCards()` look like this:

![screenshot 17](_images/_df-images/dogfinder-17.png)

<hr>

5) When you are done it should look like this - a title but no image - note that our flexbox code that make the cards tile left-to-right still functions

![screenshot 18](_images/_df-images/dogfinder-18.png)

<hr>

- That's a lot less code in `createResultCards()` - isn't it?
- Let's move on and add more to this component

<hr>

### IV-B. Add the rest of the `df-resultcard` CSS and HTML

- Head back to **df-resultcard.js**

1) Here are the CSS rules your component needs - put these in the `<style>` tag:

```css
#image-main{
  border:1px solid black;
  background-color:white;
  padding:7px;
  box-shadow: 1px 1px 2px #333;
  margin:.1rem;
  width:300px;
}
#title::first-letter {
  text-transform:capitalize;
}
.card{
  height:500px;
  overflow: auto;
}
```

- Do another dog search in the browser, the card title should now be capitalized, and the card will be 500px tall

<hr>

2) Here's the HTML for your component - yes it's a lot of typing - but a lot easier than having to figure it out yourself :-)

![screenshot 19](_images/_df-images/dogfinder-19.png)

<hr>

- Now do another dog search - what a difference - and note that "Favorite button" - something that will come in handy soon!

![screenshot 20](_images/_df-images/dogfinder-20.png)

<hr>

### IV-C. Displaying the image

- Pretty easy - just add the following to `connectedCallback()` 
- The code will look for `dataset.src` (or a `data-src` attribute) and assign that value to the image's `src` attribute if one is found, or the placeholder image if it's not

```js
this.shadowRoot.querySelector("#image-main").src = this.dataset.src || DogfinderResultsCard.defaultImage;
```

- Do another dog search, the dog images should now be visible

<hr>

### IV-D. Enabling the "Favorite" button

- Now let's get this "Favorite"  button working

<hr>

1) Here's the code that will get the Favorite button working:

![screenshot 21](_images/_df-images/dogfinder-21.png)

- Do a dog search and then click the favorite button, you will see a log to the console of the `title` and `src` of that component's image. Here is an example:

```
Breed: affenpinscher, src: https://images.dog.ceo/breeds/affenpinscher/n02110627_11853.jpg
```

- Also note above how we remove the button event handler when the component is removed from the window (which is when `disconnectedCallback()` is called)

<hr>

### IV-E. Getting the "Favorite" button working in **app.js**

- Right now when the user clicks a result card's favorite button, we get a log to the console
- But how could we get the component to actually add itself to a favorites list?
  - there are a lot of potential "clunky" solutions to get this working, and most of them involve adding a bunch of favoriting code (such as accessing `localStorage` directly, or a `storage` library) by adding a lot more of this "business logic" code to the component.
  - this would make this component a lot more complicated, and it would likely duplicate code that is probably going to be needed in **app.js** anyway
  - so a better way would be to instead put this "add me to favorites" code into **app.js** and call it from the component
  - but how should we set up this connection between the result component so that it can "call up" to **app.js**?


1) Head to **app.js** and implement the following function, right before `createResultCards()`:

```js
const addToFavorites = (dogObj) => {
  console.log("** In app.js - Now we can call any method we want to here");
  console.log("dogObj=", dogObj);
  // TODO: now add this dog to favorites
};
```

2) Now add the following line to `createResultCards()`, right in the `for` loop:

```js
newCard.callback = addToFavorites; // change the card's callback to point at `addToFavorites()`
```

3) One issue though - our current `connectedCallback()` code in the component will replace the `.callback` property we just assigned with its default
- To fix this, head to the component `connectedCallback()` code and make a small change:

```js
// Change this
this.callback = (obj) => console.log(`Breed: ${obj.title}, src: ${obj.src}`);

// To this
// if app.js doesn't assign a callback, use the default
this.callback = this.callback || ((obj) => console.log(`Breed: ${obj.title}, src: ${obj.src}`));
```

- Test it. You should see the new logs to the console
- You are now successfully "calling up" from the card component to **app.js** - here is an example::

```
** In app.js - Now we can call any method we want to here
dogObj= {title: 'affenpinscher', src: 'https://images.dog.ceo/breeds/affenpinscher/n02110627_12272.jpg'}
```

<hr><hr>

[**Previous Chapter <- Dogfinder App (part 2)**](dogfinder-2.md)
