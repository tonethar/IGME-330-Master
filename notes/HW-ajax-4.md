# HW - Ajax-4 - loading and parsing JSON files

## Overview

- The video walkthrough for this assignment is here. You will need to be logged into RIT/myCourses before you can access it:
[HW - Ajax-4 (22:37)](https://rit.hosted.panopto.com/Panopto/Pages/Viewer.aspx?id=06b77b54-e15f-47e8-85c0-ad9601210369&start=0)
- We will build on what we did last time by modifying our XML loading code to instead download and parse a JSON ("**J**ava**S**cript **O**bject **N**otation") file


<hr>

## I. About JSON

- *JSON (JavaScript Object Notation) is a lightweight data-interchange format. It is easy for humans to read and write. It is easy for machines to parse and generate... JSON is a text format that is completely language independent but uses conventions that are familiar to programmers of the C-family of languages, including C, C++, C#, Java, JavaScript, Perl, Python, and many others. These properties make JSON an ideal data-interchange language.*
  - https://www.json.org/json-en.html
- JSON *keys* must be double-quoted strings, but JSON values can be any of these 6 types:
  - `string`
  - `number`
  - `object` (JSON object, no methods allowed)
  - `array`
  - `boolean`
  - `null`
 - You have worked with `XHR` and JSON before, back in 230/235, check out the notes again if you wish:
   - https://github.com/tonethar/IGME-230-Master/blob/master/notes/web-apps-10.md
   - https://github.com/tonethar/IGME-230-Master/blob/master/notes/HW-gif-finder.md
	
<hr>

## II. Start files
- You might want to start by first making a copy of your **ajax-3/** folder from last time, and naming the copy **ajax-4/**
- Go ahead and rename your completed HTML file from last time - from **xhr-get-xml.html** to **xhr-get-json.html** 
- Below is the plain-text data file **pet-names.json** that we will use this time
- **pet-names.json** contains popular dog and cat pet names, stored as values to keys
- note that the dog and cat names can now be distinguished by looking at the top-level object keys of `"dognames"` and `"catnames"`
- go ahead and create the **pet-names.json** file and put it in your **data/** folder

<hr>

- Here is our first attempt at encoding the pet names - not bad, but let's move on and see if we can do better
- *DO NOT USE THIS ONE:*

```json
{
  "dognames" : ["Bella","Luna","Charlie","Lucy","Cooper","Max","Bailey","Daisy","Sadie","Lola","Buddy","Molly","Stella","Tucker","Bear","Zoey","Duke","Harley","Maggie","Jax"],
  "catnames" : ["Oliver","Leo","Milo","Charlie","Simba","Max","Jack","Loki","Tiger","Jasper","Ollie","Oscar","George","Buddy","Toby","Smokey","Finn","Felix","Simon","Shadow"]
}
```

<hr>

- Here in an improved version, which has more information in it, for example, a `type`, a `popularity`, and a `title` for each set of names
- Note that below we are using 4 of JSON's 6 data types: `object`, `string`, `number` and `array`
- N.B. - I generated a random key (unique identifier) with this - and I shortened them to make the file easier to read -  https://www.guidgenerator.com/online-guid-generator.aspx
- **USE THIS ONE:**

**data/pet-names.json**

```json
{
  "c9532dc9": {
		"type": "dognames",
		"popularity": 5,
		"title": "Dog Names",
		"namelist": ["Bella", "Luna", "Charlie", "Lucy", "Cooper", "Max", "Bailey", "Daisy", "Sadie", "Lola", "Buddy", "Molly", "Stella", "Tucker", "Bear", "Zoey", "Duke", "Harley", "Maggie", "Jax"]
  },
  "69bab900": {
		"type": "catnames",
		"popularity": 4,
		"title": "Cat Names",
		"namelist": ["Oliver", "Leo", "Milo", "Charlie", "Simba", "Max", "Jack", "Loki", "Tiger", "Jasper", "Ollie", "Oscar", "George", "Buddy", "Toby", "Smokey", "Finn", "Felix", "Simon", "Shadow"]
  }
}
```

<hr>



## III. Get the JSON parsing working
- We will walk through this together:
  - We will be using the [`xhr.responseText`](https://developer.mozilla.org/en-US/docs/Web/API/XMLHttpRequest/responseText) property again
  - We will also use [`JSON.parse()`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/JSON/parse) method will parse a JSON string and turn it into a JavaScript value for us
  - We will use [`Object.keys()`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Object/keys) to obtain the *keys* of the returned object so that we can iterate over its properties
  - We will also "break" the JSON and see how our code responds
    - [`try/catch`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements/try...catch) will come in handy here!
  - We will write "guard" code that displays a message if the JSON is "bad" (e.g. not *well-formed*) or not *valid* (it's missing a key we were expecting to be there)
  - Here is a nice tool for making sure that your JSON is *well-formed* - https://jsonlint.com

<hr>

## IV. Your Turn

- Add the pet bird names you used previously to **pet-names.json**
- Write code so that the pet bird names are loaded from the JSON file, and will display on the screen the same as they did in Ajax-3
- IMPORTANT: You can double-check that **pet-names.json** is still *well-formed* with this tool - https://jsonlint.com

<hr>

## V. Submission
- Putting your files in a containing folder named **ajax-4/** probably makes sense
- See the dropbox for submission instructions

<hr>

## VI. Extra Credit Opportunity

1) Near the top of the HTML page, when it first loads, show the user the "types" and "titles" of the available pet name lists. Do this by loading the JSON file and pulling those values out.

2) Give the user either a drop-down list (i.e. a `<select>`) or a text input field and a button, where they can search for and display (solely) the chosen list of pet names. (There are a lot of ways to accomplish this! Let's see what you come up with!)

- Worth 1 HW assignment
- Post this version to the **Ajax-4 - Extra Credit** dropbox
- Partial credit may be awarded for partially correct solutions

<hr><hr>

| <-- Previous Unit | Home | Next Unit -->
| --- | --- | --- 
|   [**HW - Ajax III**](HW-ajax-3.md)  |  [**IGME-330**](../README.md) | :-\
