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

<hr><hr>

| <-- Previous Unit | Home | Next Unit -->
| --- | --- | --- 
|   [**HW - Ajax II**](HW-ajax-2.md)  |  [**IGME-330**](../README.md) | [**HW - Ajax IV**](HW-ajax-4.md)
