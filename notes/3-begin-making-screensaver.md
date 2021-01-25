# Canvas 2D Essential Skills #2 - Begin making screensaver

## I. Overview


## II. Handy Helper Functions

These will be useful as we build our screen saver.

```js
// handy helper functions!
function getRandomColor(){
  function getByte(){
    return 55 + Math.round(Math.random() * 200);
  }
  return "rgba(" + getByte() + "," + getByte() + "," + getByte() + ",.8)";
}

function getRandomInt(min, max) {
  return Math.floor(Math.random() * (max - min + 1)) + min;
}
```

<hr>

## III. Demo

<hr>

## IV. Completed versions

We will demo how to draw a variety of shapes in class. Below are a couple possibile outcomes:

![screenshot](./_images/screen-saver-1.gif)

![screenshot](./_images/screen-saver-2.gif)

![screenshot](./_images/screen-saver-3.gif)

![screenshot](./_images/screen-saver-4.gif)

<hr>

## V. Homework

- Modify the above "screen saver" in some significant ways (so that it draws differently/looks different) - see myCourses for the due date and submission requirements

 
 
 
 <hr><hr>

| <-- Previous Unit | Home | Next Unit -->
| --- | --- | --- 
|  [**#2 - Paths & Lines & Arcs**](2-canvas-paths-lines-arcs.md) |  [**IGME-330**](../README.md) | [**Skill #4 - TBA**]()
