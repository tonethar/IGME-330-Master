# Canvas 2D Essential Skills #4 - Adding Controls

## I. Overview
- Here we will interactivity to our screen saver:
  - Play/Pause buttons
  - The ability to click on the screen to "spray paint" on the canvas
  - A checkbox to turn this capability on and off

<hr>

## II. HTML/CSS code

- Add the following to your HTML file

### CSS
```css
body{
  font-family: sans-serif;
}
	
button{
  font-size:1.2em;
}
	
section{
  margin:.5em 0 .5em 0;
}
```

### HTML

```html
<section>
  <button id="btnPlay">Play</button>
  <button id="btnPause">Pause</button>
</section>
<section>
  <span>
    <input type="checkbox" id="cbSpraypaint" checked>
    <label for="cbSpraypaint">Create Rectangles</label>
  </span>
</section>
<section>
  <p>Click on the screen to "spraypaint" rectangles (you probably want the screensaver to be paused)</p>
</section>
```

<hr>

## III. Helper Code

```js
function canvasClicked(e){
  let rect = e.target.getBoundingClientRect();
  let mouseX = e.clientX - rect.x;
  let mouseY = e.clientY - rect.y;
  console.log(mouseX,mouseY);
}
```


<hr>

## IV. Demo/Walkthrough

- Enable the Play/Pause buttons:
  - `paused` boolean
  - `setupUI()` helper function will enable the `btnPause` and `btnPlay` buttons
  - call `setupUI()` from `init()`
  - modify `update()` loop to utilize `paused` boolean
  - test it
  - now spam the **Play** button - the animation speeds up (unintentionally!):
    - you fix it! (this is a graded part of the HW)
- Enable the "spray paint":
  - hook up `canvasClicked` to the `<canvas>` element and test it:
    - error! Let's fix it together
    - now we should see the logged coordinates when the canvas is clicked on
  - Create a helper function to draw rectanges - here's the function signature:
    - `drawRectangle(ctx,x,y,width,height,fillStyle="black",lineWidth=0,strokeStyle="black")`
    - now we'll implement the it
    - we'll use `ctx.save()` and `ctx.restore()` here
- Enable the checkbox
  - create a `spraypaint` boolean
  
  
![screenshot](_images/)

<hr>

## V. Check it off!

- ZIP & POST file in myCourses dropbox
- In comments field of dropbox, tell us what changes you made
- Rubric:
  - (-5) **Play** button still broken - i.e. *spamming the **Play** button still speeds up the animation*

<hr><hr>

| <-- Previous Unit | Home | Next Unit -->
| --- | --- | --- 
|  [**#3 - Begin making a screensaver**](3-begin-making-screensaver.md) |  [**IGME-330**](../README.md) | [**Skill #4 - TBA**]()
