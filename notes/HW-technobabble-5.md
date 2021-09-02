# HW - Technobabble Generator V - XML


## I. Goal

- You will load your name data from an external XML file using `XHR`
- In this exercise, you will delete the contents of the `words1`, `words2` and `words3` arrays, and instead load the words from an external file named **babble-data.xml**

<hr>

## II. Requirements & Hints

- Use [HW - Technobabble Generator IV](HW-technobabble-4.md) as your starting point by making a copy of it that you can modify
- [HW - Ajax-3 - loading and parsing XML files](https://github.com/tonethar/IGME-330-Master/blob/master/notes/HW-ajax-3.md) will come in handy
- YOU are creating **babble-data.xml**
- YOU will need to encode the three word data arrays as *well-formed* XML - be sure to come up with element and attribute names that make sense, and don't just reuse what we did in **HW Ajax-3** 
- You must load the **babble-data.xml** file using `XHR`
- You must load the **babble-data.xml** file ONCE, at app startup. DO NOT (for example) load the data every time the user clicks a button
- Make sure that there is some default babble that is displayed to the user when the app first starts up (DO NOT do this in your `window.onload` function, instead, display the babble AFTER the `XHR` has loaded)

<hr>

## III. Submission
- See dropbox for submission instructions


<hr><hr>

| <-- Previous Unit | Home | Next Unit -->
| --- | --- | --- 
|  [**HW - Technobabble Generator IV**](HW-technobabble-4.md) |  [**IGME-330**](../README.md) | [**HW - Technobabble Generator VI**](HW-technobabble-6.md)
