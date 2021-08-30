# HW - Ajax-3 - loading and parsing XML files

## Overview

- The video walkthrough for this assignment is here --> 
- We will build on what we did last time by modifying our CSV loading code to instead download and parse an XML ("E**x**tensible **M**arkup **L**anguage") file


<hr>

## I. Start files
- You might want to start by first making a copy of your **ajax-2/** folder from last time, and naming the copy **ajax-3/**
- Go ahead and rename your completed HTML file from last time - from **xhr-get-csv.html** to **xhr-get-xml.html** 
- Below is the plain-text data file **pet-names.xml** that we will use this time
- **pet-names.xml** contains popular dog and cat pet names "marked up"
- go ahead and create the **pet-names.xml** file and put it in your **data/** folder

<hr>

**data/pet-names.xml**

```text
<petnames>
	<namelist id="dognames">Bella,Luna,Charlie,Lucy,Cooper,Max,Bailey,Daisy,Sadie,Lola,Buddy,Molly,Stella,Tucker,Bear,Zoey,Duke,Harley,Maggie,Jax</namelist>
	<namelist id="catnames">Oliver,Leo,Milo,Charlie,Simba,Max,Jack,Loki,Tiger,Jasper,Ollie,Oscar,George,Buddy,Toby,Smokey,Finn,Felix,Simon,Shadow</namelist>
</petnames>
```

<hr>

## II. About XML

- **pet-names.xml** contains the dog and cat pet names in a structured XML format. The element names that were used in the file are not part of any standard and chosen because they made sense to the developer
- XML - Extensible Markup Language - is a set of rules for defining your own markup language
- The top 5 rules for writing XML (from here https://www.ibm.com/docs/en/scbn?topic=syntax-xml-rules - are:
  - All XML elements must have a closing tag
  - XML tags are case sensitive
  - All XML elements must be properly nested
  - All XML documents must have a root element
  - Attribute values must always be quoted
- When authoring your XML, make sure that you strictly follow these rules. Making even the slightest mistake, such as forgetting to close a tag, will mean that the file is not valid XML and will therefore not be able to be parsed by `XHR`
- We will be using the [xhr.responseXML](https://developer.mozilla.org/en-US/docs/Web/API/XMLHttpRequest/responseXML) property this time - which returns a `Document` containing the HTML or XML retrieved by the request; or `null` if the request was unsuccessful
	
<hr>

## III.

<hr><hr>

| <-- Previous Unit | Home | Next Unit -->
| --- | --- | --- 
|   [**HW - Ajax II**](HW-ajax-2.md)  |  [**IGME-330**](../README.md) | [**HW - Ajax IV**](HW-ajax-4.md)
