# Canvas 2D Essential Skills #5 - Write some code!

## I. Overview

- You are going to add code and functionality to **cs-canvas-5.html**
- In any of the functions that do drawing, be sure that you have a call to `ctx.save()` and `ctx.restore()`

## II. Canvas Helper functions

- `drawArc(...)` will be similar to `drawRectangle(ctx,x,y,width,height,fillStyle="black",lineWidth=0,strokeStyle="black")` except:
  - it will have a `radius` parameters instead of `width` and `height`
  - it will also have *optional* parameters for `startAngle` and `endAngle`, and these withh default to `0` and `Math.PI *2` respectively
- `drawLine()` 
