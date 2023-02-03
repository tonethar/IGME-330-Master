# Canvas 2D Essential Skills #2 - Paths & Lines & Arcs

## 0. Video & HW

- The video for this lecture, which walks through the notes and adds a few details, is here --> [Essential Skills - Part II (10:26)](https://video.rit.edu/Watch/330-essential-skills-2)
- See the HW assignment at the bottom of the page (Part III.)

<hr>

## I. Overview

- A canvas *path* is a mathematical representation of a shape that can be filled with the current `fillStyle`, and/or stroked with the current `strokeStyle`
- Last time we use the `fillRect()` and `strokeRect()` *convenience methods* that created a path and then immediately filled or stroked it
- This time, we will first describe a path, and then `.fill()` or `.stroke()` it.

### Paths

- [`ctx.beginPath()`](https://developer.mozilla.org/en-US/docs/Web/API/CanvasRenderingContext2D/beginPath)
- [`ctx.closePath()`](https://developer.mozilla.org/en-US/docs/Web/API/CanvasRenderingContext2D/closePath)
- [`ctx.rect()`](https://developer.mozilla.org/en-US/docs/Web/API/CanvasRenderingContext2D/rect)
- [`ctx.fill()`](https://developer.mozilla.org/en-US/docs/Web/API/CanvasRenderingContext2D/fill)
- [`ctx.stroke()`](https://developer.mozilla.org/en-US/docs/Web/API/CanvasRenderingContext2D/stroke)

### Lines
- [`ctx.moveTo()`](https://developer.mozilla.org/en-US/docs/Web/API/CanvasRenderingContext2D/moveTo)
- [`ctx.lineTo()`](https://developer.mozilla.org/en-US/docs/Web/API/CanvasRenderingContext2D/lineTo)

### Arcs
- [`ctx.arc()`](https://developer.mozilla.org/en-US/docs/Web/API/CanvasRenderingContext2D/arc)


- Or, we can always look in the Canvas2D spec: https://dev.w3.org/html5/2dcontext-LC/#conformance-requirements

<hr>

## II. Demo
- Build on the "done" code from last time
- create a rectangle path the hard way - with `ctx.rect()`
  - fill and stroke it
- create line paths and stroke them
- create a circle path with `ctx.arc()`
  - fill and stroke
- create a semi-circle with `ctx.arc()`

<hr>

## III. Check it Off!
- Easy!:
  - Add 2 more circles to **cs-canvas-2.html**, make them small "eyes" near the center of the screen
  - Add 1 line to **cs-canvas-2.html**, make it 600 pixels long and give it a width of 20 pixels
- Rename **cs-canvas-2.html** to ***lastName-firstInitial*-cs-canvas-2.html**
- Then ZIP and POST ***lastName-firstInitial*-cs-canvas-2.html** to myCourses
- Don't post this to banjo! We'll make better looking stuff soon!

<hr><hr>

| <-- Previous Unit | Home | Next Unit -->
| --- | --- | --- 
|  [**#1 - Intro to the Drawing Context**](1-canvas-intro-to-drawing-context.md) |  [**IGME-330**](../README.md) | [**Skill #3 - Begin making a screensaver**](3-begin-making-screensaver.md)
