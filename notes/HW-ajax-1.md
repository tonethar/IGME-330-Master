# HW - Ajax-1 - loading and parsing text files

## Overview

- In this series, we are going to walk through using the browser [XMLHttpRequest (aka "XHR")](https://developer.mozilla.org/en-US/docs/Web/API/XMLHttpRequest/Using_XMLHttpRequest) and fetch(https://developer.mozilla.org/en-US/docs/Web/API/Fetch_API/Using_Fetch) APIs to download data and display it to the user
- We will download and parse data in multiple formats - plain text, CSV, XML  and JSON
- Note: In 230/235 you have already had some experience with some of this - specifically XHR and JSON - go review those notes now if you wish:
  - https://github.com/tonethar/IGME-230-Master/blob/master/notes/web-apps-10.md
  - https://github.com/tonethar/IGME-230-Master/blob/master/notes/HW-gif-finder.md

## I. Start files

- Below is your plain-text data file **pet-names.txt** - it consists of the top-20 most popular pet dog names, followed by the 20-most popular pet cat names
- These names are *comma-separated*, and both dog and cat names appear in the one line of text in the file (not a very good structure, and we'll rectify that in **Ajax-2**)
- go ahead and create a **data** fodler and place the **pet-names.txt** file into it:

<hr>

**data/pet-names.txt**

```text
Bella,Luna,Charlie,Lucy,Cooper,Max,Bailey,Daisy,Sadie,Lola,Buddy,Molly,Stella,Tucker,Bear,Zoey,Duke,Harley,Maggie,Jax,Oliver,Leo,Milo,Charlie,Simba,Max,Jack,Loki,Tiger,Jasper,Ollie,Oscar,George,Buddy,Toby,Smokey,Finn,Felix,Simon,Shadow
```

<hr>

- Here is our HTML file that has the HTML/CSS/JS to get us started"

**xhr-get-text.html**

```html

```

<hr>

## II. Get XHR working

<hr>

## III. 

<hr>

## IV. Reference

### APIs Used
- [`XMLHttpRequest`](https://developer.mozilla.org/en-US/docs/Web/API/XMLHttpRequest/Using_XMLHttpRequest) - <code>XHR</code> objects are used to interact with servers. You can retrieve data from a URL without having to do a full page refresh. This enables a Web page to update just part of a page without disrupting what the user is doing
- [`xhr.responseText`](https://developer.mozilla.org/en-US/docs/Web/API/XMLHttpRequest/responseText) - contains either the textual data received from the `XHR`, or `null` if the request failed
- [String.split()](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/String/split) - turns a string into an array
- [`Array.map()`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/map) - creates a new array populated with the results of calling a provided function on every element in the calling array
- [`Array.join()`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/join) - returns a new string by concatenating all of the elements in an array

### ES6
- [ES6 Arrow Functions](https://www.w3schools.com/js/js_arrow_function.asp)


<hr><hr>

| <-- Previous Unit | Home | Next Unit -->
| --- | --- | --- 
|   :-\  |  [**IGME-330**](../README.md) | [**HW - Ajax II**](HW-ajax-2.md)
