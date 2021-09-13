# HW - Ajax-6 - `async` & `await` with the `fetch()` API

## Overview
- The video walkthrough for this assignment is here. You will need to be logged into RIT/myCourses before you can access it: [HW - Ajax-6 (09:30)](https://rit.hosted.panopto.com/Panopto/Pages/Viewer.aspx?id=48c38f6f-9ce8-4f08-9016-ad9e00f5c88d&start=0)
- If you find the `.then()` and `.catch()` syntax of JS promises somewhat obtuse, you might be interested in learning about `async` and `await`, which are also designed to work with promises, and can enable a developer to write much clearer code

<hr>

## I. `async` and `await`

- The `async` and `await` operators allow you to treat asynchronous code like synchronous code - let's walk through the beginning of this MDN article - https://developer.mozilla.org/en-US/docs/Learn/JavaScript/Asynchronous/Async_await - th highlights are:
  - An `async` function is a function that knows how to expect the possibility of the `await` keyword being used to invoke asynchronous code
  - An `async` function function always returns a *promise* (which is a function that wraps asynchronous code)
  - The advantage of an `async` function only becomes apparent when you combine it with the `await` keyword
  - Inside an `async` function, you can use the `await` operator in front of asynchronous code (like a `fetch()` call) to tell the function to wait for that operation to complete before executing the next line of code

<hr>

## II. An example

**Below is the final version from last time - `.then()` & `.catch()` code (don't type this in!)**

<hr>

![screenshot](_images/_ajax-images/HW-ajax-6.png)

<hr>

### II-A. Simple `async/await` example (no error handling)
- Now we will convert some of the code from last time from `.then()` syntax, to `async/await`
- In thus example we aren't doing any error handling
- After you get it working, you should test what happens when there are errors:
  - go ahead and change part of the url from "people" to "peep" and see the result
  - you will see that an uncaught exception is thrown, which crashes the program

<hr>

![screenshot](_images/_ajax-images/HW-ajax-7.png)

<hr>

### II-B. `async/await` example with `try/catch` for error handling

- Below we use the traditional `try/catch` block for error handling
- After you get it working, you should test what happens when there are errors:
  - go ahead and change part of the url from "people" to "peep" and see the result
  - you will see that an uncaught exception is thrown, but it is caught (in the `catch`), so the program will continue to run normally

<hr>

![screenshot](_images/_ajax-images/HW-ajax-8.png)

<hr>

### II-C. `async/await` example with `.catch()` for error handling

- Below we create a promise with `async` and add a `catch()` to it
- This version will catch thrown errors the same as the preceding version

<hr>

![screenshot](_images/_ajax-images/HW-ajax-9.png)

<hr>

## III. Reference

- https://developer.mozilla.org/en-US/docs/Web/API/Fetch_API/Using_Fetch
- https://developer.mozilla.org/en-US/docs/Web/API/fetch
- https://developer.mozilla.org/en-US/docs/Learn/JavaScript/Asynchronous/Async_await#the_basics_of_asyncawait
- https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements/async_function
- https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/await
- [JavaScript: Async on LinkedIn Learning](https://www.linkedin.com/learning/javascript-async/building-code-using-promises?u=42272537)

<hr>

## IV. Start files & HW
- You might want to start by first making a copy of your **ajax-5/** folder from last time, and naming the copy **ajax-6/**
- Rename your completed HTML file from last time - from **fetch-get-json.html** to **async-fetch-get-json.html** 
- Go ahead and adapt your code from last time to use the `fetch()` API to download **pet-names.json** instead of `XHR`, and display the lists of pets as you did before. Be sure to use `async` and `await` and some kind or error handling, like we did in the last 2 demos above
- See myCourses for submission instructions

<hr><hr>

| <-- Previous Unit | Home | Next Unit -->
| --- | --- | --- 
|   [**HW - Ajax V**](HW-ajax-5.md)  |  [**IGME-330**](../README.md) | [**HW - Ajax VII**](HW-ajax-7.md) 
