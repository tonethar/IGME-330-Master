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
  fetch('https://swapi.dev/api/people/1'); // get a random Star Wars character
}
```





## II. Start files
- You might want to start by first making a copy of your **ajax-4/** folder from last time, and naming the copy **ajax-5/**
- Go ahead and rename your completed HTML file from last time - from **xhr-get-json.html** to **fetch-get-json.html** 



<hr><hr>

| <-- Previous Unit | Home | Next Unit -->
| --- | --- | --- 
|   [**HW - Ajax IV**](HW-ajax-4.md)  |  [**IGME-330**](../README.md) | :-\
