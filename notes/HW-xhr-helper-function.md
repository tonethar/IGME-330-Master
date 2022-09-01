# XHR Helper Function Exercise

## Video
- There is a video of this lecture here: [IGME-330 - Create XHR Helper Function (14:07)](https://rit.hosted.panopto.com/Panopto/Pages/Viewer.aspx?id=ecbf4388-569e-4bfc-ace6-af0300cc0d9c)

## I. Overview

- Your first mission is to write code that follows the **DRY** software development principle:
  - clicking the "Load Taffy Info" button in the screenshot below will load and display the contents of the **taffy-facts.txt** file
  - clicking the "Load Viking Info" button will load and display the contents of the **viking-facts.txt** file
  - you will create a `loadTextXHR()` helper function named that accepts 2 parameters - `url` and `callback`
    - `url` is the path to the file you want to download with `XHR`
    - `callback` is the function you want to have called when the file has downloaded. This callback function will update the appropriate part of the page with the downloaded HTML fragment
  - the two buttons in the screenshot below are both calling the same `loadTextXHR()` function, but passing in different values for the 2 parameters
  - hint: [HW - Ajax-1 - loading and parsing text files](HW-ajax-1.md) should give you some decent starter code for `loadTextXHR()`
- Your second mission:
  - convert the code to utilize ES6 modules - **main.js** & **utils.js**
  - move `loadTextXHR()` to **utils.js** and `export` it

<hr>

### II. Screenshot of completed version

- Here we are using the Bulma CSS framework - https://bulma.io/documentation/

<hr>

![screenshot](_images/HW-xhr-helper-function.png)

<hr>

### III. Start Files

- [XHR-helper-breakout-start.zip](_files/XHR-helper-breakout-start.zip)
