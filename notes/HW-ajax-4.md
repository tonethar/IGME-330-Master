# HW - Ajax-4 - loading and parsing JSON files

## Overview

- The video walkthrough for this assignment is here. You will need to be logged into RIT/myCourses before you can access it:
HW - Ajax-4 (XX:XX)
- We will build on what we did last time by modifying our XML loading code to instead download and parse a JSON ("**J**ava**S**cript **O**bject **N**otation") file


<hr>

## I. Start files
- You might want to start by first making a copy of your **ajax-3/** folder from last time, and naming the copy **ajax-4/**
- Go ahead and rename your completed HTML file from last time - from **xhr-get-xml.html** to **xhr-get-json.html** 
- Below is the plain-text data file **pet-names.json** that we will use this time
- **pet-names.json** contains popular dog and cat pet names, stored as values to keys
- note that the dog and cat names can now be distinguished by looking at the top-level object keys of `"dognames"` and `"catnames"`
- go ahead and create the **pet-names.json** file and put it in your **data/** folder

<hr>

**data/pet-names.json**

```json
{
	"dognames" : ["Bella","Luna","Charlie","Lucy","Cooper","Max","Bailey","Daisy","Sadie","Lola","Buddy","Molly","Stella","Tucker","Bear","Zoey","Duke","Harley","Maggie","Jax"],
	"catnames" : ["Oliver","Leo","Milo","Charlie","Simba","Max","Jack","Loki","Tiger","Jasper","Ollie","Oscar","George","Buddy","Toby","Smokey","Finn","Felix","Simon","Shadow"]
}
```

<hr>

## II. About JSON

- "JSON (JavaScript Object Notation) is a lightweight data-interchange format. It is easy for humans to read and write. It is easy for machines to parse and generate... JSON is a text format that is completely language independent but uses conventions that are familiar to programmers of the C-family of languages, including C, C++, C#, Java, JavaScript, Perl, Python, and many others. These properties make JSON an ideal data-interchange language."
  - https://www.json.org/json-en.html
- JSON *keys* must be double-quoted strings, but JSON values can be any of these 6 types:
  - `string`
  - `number`
  - `object` (JSON object, no methods allowed)
  - `array`
  - `boolean`
  - `null`
	
<hr>

## III. Get the JSON parsing working
- We will walk through this together:
  - We will be using the [`xhr.responseText`](https://developer.mozilla.org/en-US/docs/Web/API/XMLHttpRequest/responseText) property again
  - We will also use [`JSON.parse()`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/JSON/parse) method will parse a JSON string and turn it into a JavaScript value for us
  - We will also "break" the JSON and see how our code responds
  - We will write "guard" code that displays a message if the JSON is "bad" (e.g. not *well-formed*) or not *valid* (it's missing a key we were expectung to be there)
  - Here is a nice tool for making sure that your JOSN is *well-formed* - https://jsonlint.com

<hr>

## IV. Your Turn

- Add the pet bird names you used previously to **pet-names.json**
- Write code so that the pet bird names are loaded from the JSON file, and will display on the screen the same as they did in Ajax-3
- IMPORTANT: You can double-check that **pet-names.json** is still *well-formed* with this tool - https://jsonlint.com

<hr>

## V. Submission
- Putting your files in a containing folder named **ajax-4/** probably makes sense
- See the dropbox for submission instructions
-
<hr><hr>

| <-- Previous Unit | Home | Next Unit -->
| --- | --- | --- 
|   [**HW - Ajax III**](HW-ajax-3.md)  |  [**IGME-330**](../README.md) | :-\
