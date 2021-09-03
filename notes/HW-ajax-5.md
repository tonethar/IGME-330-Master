# HW - Ajax-5 - the `fetch()` API

## Overview

- The video walkthrough for this assignment is here. You will need to be logged into RIT/myCourses before you can access it: HW - Ajax-5 (XX:XX)
- We will build on what we did last time by modifying our `XHR`/JSON loading code to instead utilize the [`window.fetch()`](https://developer.mozilla.org/en-US/docs/Web/API/Fetch_API/Using_Fetch) API


<hr>

## I. About fetch()
- The `window.fetch()` method is similar to `XHR` in that it used to make Ajax requests, such as calling a remote API or fetching a local file from a server

### I-A. A basic `fetch()` request

```js
function loadJsonFetch(){
  const promise = fetch('https://swapi.dev/api/people/1'); // get a Star Wars character
  console.log(promise); // "Promise {<pending>}"
}
```

- The `fetch()` method call above returns a [`Promise`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Guide/Using_promises) object. A Promise is a JavaScript object that "wraps" an asynchronous function.
- MDN decribes them fairly well = "A Promise is an object representing the eventual completion or failure of an asynchronous operation. Since most people are consumers of already-created promises, this guide will explain consumption of returned promises before explaining how to create them. Essentially, a promise is a returned object to which you attach callbacks, instead of passing callbacks into a function."
- The above code logs out the `Promise` object, which is incomplete because the data has not yet downloaded. So this code isn't too useful yet, let's move on

<hr>

### I-B. Hooking into `Promise.then()` and `Promise.catch()`

- We can handle this promise that `fetch` returned to us by chaining `Promise.then()` and `Promise.catch()` methods to it
- `Promise.then()` will be called when the promise "resolves" (by internally calling `resolve()`)
- `Promise.catch()` will be called when the promise "rejects" (by internally calling `reject()`)

```js
function loadJsonFetch(){
  fetch('https://swapi.dev/api/people/1')
  .then(response => {
    // success
    console.log(response); // Response {type: "cors", url: "https://swapi.dev/api/people/1", redirected: false, status: 200, ok: true, …}
    console.log(response.json()); // Promise {<pending>}	
  }).catch(error => {
    // error
    console.log(error);
  });
}
```
- When you run this code, you should note that the (arrow) function passed to `.then()` runs, which means the request was successful 
- Note though, that `response.json()` also returns a *promise*, meaning that it is an asynchronous operation that is running on another thread, just like the `response` promise
- This means that we don't yet have access to the actual response data (the JSON) because this second promise has not yet *resolved* 
- So we now have TWO promises to worry about! What's the Solution? Another `.then()`

<hr>

### I-C. Resolving the `response.json()` promise

```js
function loadJsonFetch(){
  fetch('https://swapi.dev/api/people/1')
    .then(response => response.json()) // pipe the response.json() promise to the next .then()
    .then(json => { // the second promise is resolved, and `json` is a JSON object
      console.log(json); // {name: "Luke Skywalker", height: "172", mass: "77", hair_color: "blond", skin_color: "fair", …}
      console.log(json.name) // Luke Skywalker
      console.log(json.homeworld); // https://swapi.dev/api/planets/1/
    }).catch(error => {
      // error
      console.log(error);
  });
}
```

- When you run this code, both promises should resolve, and the code should log out the JSON object, as well as the `.name` and `.homeworld` properties
- Note that unlike `XHR`, with `fetch()` the JSON object is created for us automatically, thus we don't have to call `JSON.parse(e.target.responseText)`

<hr>

### I-D. The `response.ok` property

- XXX

<hr>

## II. Start files & HW
- You might want to start by first making a copy of your **ajax-4/** folder from last time, and naming the copy **ajax-5/**
- Rename your completed HTML file from last time - from **xhr-get-json.html** to **fetch-get-json.html** 
- Go ahead and adapt your code from last time to use the `fetch()` API to download **pet-names.json** instead of `XHR`, and display the lists of pets as you did before. Be sure to use `.then()` like we did in the demos above
- See myCourses for submission instructions


<hr>

# III. More chaining

- XXX

<hr>

# IV. `asynch` and `await`

- If find the `.then()` syntax somewhat obtuse, you might be ibnterested in learning about  `asynch` and `await`, which are designed to work with promises
- XXX

<hr><hr>

| <-- Previous Unit | Home | Next Unit -->
| --- | --- | --- 
|   [**HW - Ajax IV**](HW-ajax-4.md)  |  [**IGME-330**](../README.md) | :-\
