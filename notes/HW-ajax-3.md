# HW - Ajax-3 - loading and parsing XML files

## Overview

- The video walkthrough for this assignment is here. You will need to be logged into RIT/myCourses before you can access it:
[HW - Ajax-3 (15:43)](https://rit.hosted.panopto.com/Panopto/Pages/Viewer.aspx?id=ebb703bf-1e83-47c4-b8c1-ad9500ed6204&start=0)
- We will build on what we did last time by modifying our CSV loading code to instead download and parse an XML ("E**x**tensible **M**arkup **L**anguage") file


<hr>

## I. Start files
- You might want to start by first making a copy of your **ajax-2/** folder from last time, and naming the copy **ajax-3/**
- Go ahead and rename your completed HTML file from last time - from **xhr-get-csv.html** to **xhr-get-xml.html** 
- Below is the plain-text data file **pet-names.xml** that we will use this time
- **pet-names.xml** contains popular dog and cat pet names that are "marked up"
- note that the dog and cat names can now be distinguished by looking at the `cid` attribute (which stands for "category ID", something we made up) 
- go ahead and create the **pet-names.xml** file and put it in your **data/** folder

<hr>

**data/pet-names.xml**

```xml
<?xml version="1.0" encoding="UTF-8"?>
<petnames>
  <namelist cid="dognames">Bella,Luna,Charlie,Lucy,Cooper,Max,Bailey,Daisy,Sadie,Lola,Buddy,Molly,Stella,Tucker,Bear,Zoey,Duke,Harley,Maggie,Jax</namelist>
  <namelist cid="catnames">Oliver,Leo,Milo,Charlie,Simba,Max,Jack,Loki,Tiger,Jasper,Ollie,Oscar,George,Buddy,Toby,Smokey,Finn,Felix,Simon,Shadow</namelist>
</petnames>
```

- N.B. - the XML declaration at the top of an XML file is optional as long at the encoding is in UTF-8 or UTF-16

<hr>

## II. About XML

- ***Extensible Markup Language (XML)** is a markup language and file format for storing, transmitting, and reconstructing arbitrary data. It defines a set of rules for encoding documents in a format that is both human-readable and machine-readable.* - https://en.wikipedia.org/wiki/XML
- **pet-names.xml** contains the dog and cat pet names in a structured XML format. The element names that were used in the file are not part of any standard and were chosen because they made sense to the developer
- XML - Extensible Markup Language - is a set of rules for defining your own markup language
- The top 5 rules for writing *well-formed* XML (from here https://www.ibm.com/docs/en/scbn?topic=syntax-xml-rules - are:
  - All XML elements must have a closing tag
  - XML tags are case sensitive
  - All XML elements must be properly nested
  - All XML documents must have a root element
  - Attribute values must always be quoted
- When authoring your XML, make sure that you strictly follow these rules. Making even the slightest mistake, such as forgetting to close a tag, will mean that the file is not valid XML and will therefore not be able to be parsed by `XHR`
- N.B. - if we wanted our XML format to be more robust, we would also design an [XML *schema*](https://www.w3schools.com/xml/schema_intro.asp) - which is a set of rules about allowable tag names and attributes, legal values, required and optional attributes and so on. These rules allow an XML *validator* to check the *semantics* of your XML (similar to what HTML and CSS validators do). We are not going to worry about XML *validation*  in this simple example.
	
<hr>

## III. Get the XML parsing working
- We will walk through this together:
  - We will be using the [`xhr.responseXML`](https://developer.mozilla.org/en-US/docs/Web/API/XMLHttpRequest/responseXML) property this time (instead of `xhr.responseText`) - which returns a `Document` containing the HTML or XML retrieved by the request; or `null` if the request was unsuccessful
  - `document.querySelector()` will come in handy when parsing the loaded XML
  - [CSS Attribute Selectors](https://developer.mozilla.org/en-US/docs/Web/CSS/Attribute_selectors) will make it easy to select the desired XML element
  - We will also "break" the XML and see how our code responds
  - We will write "guard" code that displays a message if the XML is "bad" (e.g. not *well-formed*)

<hr>

## IV. Your Turn

- Add the pet bird names you used last time to **pet-names.xml**
- Write code so that the pet bird names are loaded from the XML file, and will display on the screen the same as they did in Ajax-2
- IMPORTANT: You can double-check that **pet-names.xml** is still *well-formed* XML by opening the file in Chrome

<hr>

## V. Submission
- We are not collecting this!
- Instead, use it as a resource to complete [HW - Technobabble Generator V - XML](HW-technobabble-5.md)

<!--
- Putting your files in a containing folder named **ajax-3/** probably makes sense
- See the dropbox for submission instructions
-->

<hr><hr>

| <-- Previous Unit | Home | Next Unit -->
| --- | --- | --- 
|   [**HW - Ajax II**](HW-ajax-2.md)  |  [**IGME-330**](../README.md) | [**HW - Ajax IV**](HW-ajax-4.md)
