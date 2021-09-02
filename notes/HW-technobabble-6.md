# HW - Technobabble Generator VI - JSON


## I. Goal

- You will load your name data from an external JSON file using `XHR`
- In this exercise, you will delete the contents of the `words1`, `words2` and `words3` arrays, and instead load the words from an external file named **babble-data.json**

<hr>

## II. Requirements & Hints

- Use [HW - Technobabble Generator V](HW-technobabble-5.md) as your starting point by making a copy of it that you can modify
- [HW - Ajax-4 - loading and parsing JSON files](https://github.com/tonethar/IGME-330-Master/blob/master/notes/HW-ajax-4.md) will come in handy
- YOU are creating **babble-data.json**
- YOU will need to encode the three word data arrays as *well-formed* JSON - be sure to come up with JSON property names that make sense, and don't just reuse what we did in **HW Ajax-4**
- Be sure to encode the JSON with key names like `words1`, `words2` etc - you might also want to encode other information in your JSON file and utilize it - i.e. the contents of the `<h1>` that appears the page
- Here are some JSON validator tools that might come in handy - https://jsonlint.com/
- You must load the **babble-data.json** file using `XHR`
- You must load the **babble-data.json** file ONCE, at app startup. DO NOT (for example) load the data every time the user clicks a button
- Make sure that there is some default babble that is displayed to the user when the app first starts up (DO NOT do this in your `window.onload` function, instead, display the babble AFTER the `XHR` has loaded)

<hr>

## III. Submission
- See dropbox for submission instructions


<hr><hr>

| <-- Previous Unit | Home | Next Unit -->
| --- | --- | --- 
|  [**HW - Technobabble Generator V**](HW-technobabble-5.md) |  [**IGME-330**](../README.md) | :-/
