# HW - Technobabble Generator IV - CSV

## I. Goal

- Rather than hard-code your Technobabble data, you will instead load it from an external CSV file using `XHR`
- In this exercise, you will delete the contents of the `words1`, `words2` and `words3` arrays, and instead load the words from an external file named **babble-data.csv**

<hr>

## II. Requirements & Hints

- Use [HW - Technobabble Generator III](HW-technobabble-3.md) as your starting point by making a copy of it that you can modify
- [HW - Ajax-2 - loading and parsing CSV files](https://github.com/tonethar/IGME-330-Master/blob/master/notes/HW-ajax-2.md) will come in handy
- YOU are creating **babble-data.csv**
- Each line of **babble-data.csv** will contain the words from one of the arrays
- You must load the **babble-data.csv** file using `XHR`
- You must load the **babble-data.csv** file ONCE, at app startup. DO NOT (for example) load the data every time the user clicks a button
- Make sure that there is some default babble that is displayed to the user when the app first starts up (DO NOT do this in your `window.onload` function, instead, display this initial babble AFTER the `XHR` has loaded)
- Finally, both of the "babble" buttons from TB-3 will still function as before when they are clicked on
- Hints:
  - The individual "babble" words in the XML file will not have quotes around them - you will need to strip those off

<hr>

## III. Submission
- See dropbox for submission instructions



<hr><hr>

| <-- Previous Unit | Home | Next Unit -->
| --- | --- | --- 
|  [**HW - Technobabble Generator III**](HW-technobabble-3.md) |  [**IGME-330**](../README.md) | [**HW - Technobabble Generator V**](HW-technobabble-5.md) 
