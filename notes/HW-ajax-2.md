# HW - Ajax-2 - loading and parsing CSV files

## Overview

- The video walkthrough for this assignment is here --> 
- We will build on what we did last time by modifying our plain-text loading code to instead download and parse a CSV ("**C**omma **S**eparated **V**alues") file
- CSV is a very popular data format that is easily exported from spreadsheet applications such as Excel. CSV is the primary data format for sharing scientific data that will analyzed and/or visualized

<hr>

## I. Start files
- Rename your completed HTML file from last time - from **xhr-get-text.html** to **xhr-get-csv.html** (you might just want to start by making a copy of your **ajax-1/** folder and name the copy **ajax-2/**
- Below is your plain-text data file **pet-names.csv** - it consists of the top-20 most popular pet dog names, followed by the 20-most popular pet cat names
- **pet-names.csv** contains popular dog and cat pet names on *separate lines*. The pet names are separated by commas
- go ahead and create a **data** folder and place the **pet-names.csv** file into it:

<hr>

**data/pet-names.csv**

```text
Bella,Luna,Charlie,Lucy,Cooper,Max,Bailey,Daisy,Sadie,Lola,Buddy,Molly,Stella,Tucker,Bear,Zoey,Duke,Harley,Maggie,Jax
Oliver,Leo,Milo,Charlie,Simba,Max,Jack,Loki,Tiger,Jasper,Ollie,Oscar,George,Buddy,Toby,Smokey,Finn,Felix,Simon,Shadow
```

<hr>

## II. Get the CSV parsing working

- We will walk through this together on the video

<hr>

## III. Completed Version (so far)

![screenshot](_images/_ajax-images/HW-ajax-3.png)

<hr>

## IV. Your turn
- Go ahead and modify the code so that it displays a list of pet bird names:
  - use the google to get 20 popular names for pet birds, and add them as a new row to the **pet-names.csv** file
  - write code that will display those bird names as an ordered list underneath another `<h3>` subheading (as was done with the dog and cat names)

<hr>

## V. Reference

- again we use [`xhr.responseText`](https://developer.mozilla.org/en-US/docs/Web/API/XMLHttpRequest/responseText) - contains either the textual data received using `XHR`, or `null` if the request failed
- We will also look at [array destructuring](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/Destructuring_assignment) assignment - this syntax is a JavaScript expression that makes it possible to unpack values from arrays

<hr>

## VI. Submission

- Putting your files in a containing folder named  **ajax-1/** probably makes sense
- See the dropbox for submission instructions


<hr><hr>

| <-- Previous Unit | Home | Next Unit -->
| --- | --- | --- 
|   [**HW - Ajax I**](HW-ajax-1.md)  |  [**IGME-330**](../README.md) | [**HW - Ajax III**](HW-ajax-3.md)
