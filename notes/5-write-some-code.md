# Canvas 2D Essential Skills #5 - Write some code!

## I. Overview
- You are going to add code and functionality to **cs-canvas-5.html**
- In any of the functions that do drawing, be sure that you have a call to `ctx.save()` and `ctx.restore()`

<hr>

## II. Required Canvas Helper functions
- `drawArc(...)` will be similar to `drawRectangle(ctx,x,y,width,height,fillStyle="black",lineWidth=0,strokeStyle="black")` except:
  - it will have a `radius` parameter instead of `width` and `height`
  - it will also have *optional* parameters for `startAngle` and `endAngle`, and these withh default to `0` and `Math.PI *2` respectively
- `drawLine()` will be similar to `drawRectangle(ctx,x,y,width,height,fillStyle="black",lineWidth=0,strokeStyle="black")` except:
  - it will not need `fillStyle` or `width` or `height` parameters
  - it will have `x1`, `y1`, `x2`, and `y2` parameters (e.g. the start and end points of the line)
  - the default `lineWidth` will be `1`
- `drawRandomArc()` will function similarly to `drawRandomRect()`:
  - except that it will call `drawArc(...)`
- `drawRandomALine()` will function similarly to `drawRandomRect()`:
  - except that it will call `drawLine(...)`

<hr>

## III. Required functionality
- there will be 2 more checkboxes called "Draw Arcs" and "Draw Lines":
  - when these are checked, random arcs and lines will be drawn using the above methods
- there will be a "Clear Screen" button:
  - when clicked it will clear out all of the existing drawing (you can use `ctx.fillRect()` or just `ctx.fill()` a canvas-sized rectangle with a solid color

<hr>

## IV. Required code refactoring
- Re-write all of the drawing code in the `init()` function to use your **Canvas Helper Functions**  - `drawRectangle()`, `drawArc()` and `drawLine()`
- Change the "spraypaint" functionality so that it paints arcs, not rectangles

<hr>

## V. Submission

- ZIP and POST to the dropbox

<hr><hr>

| <-- Previous Unit | Home | Next Unit -->
| --- | --- | --- 
|  [**#4 - Adding Controls**](4-adding-controls.md) |  [**IGME-330**](../README.md) | **Skill #6 - TBA**
