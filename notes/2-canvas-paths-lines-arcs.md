# Canvas 2D Essential Skills #2 - Paths & Lines & Arcs

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


- Or, we can always look in the Canvas2D spec: https://www.w3.org/TR/2dcontext/#conformance-requirements

<hr>

## II. Demo
- create a rectangle path the hard way - with `ctx.rect()`
  - fill and stroke it
- create line paths and stroke them
- create a circle path with `ctx.arc()`
  - fill and stroke
- create a semi-circle with `ctx.arc()`

<hr>

## III. Check it Off!

- Just ZIP and POST this to myCourses - that's it!

<hr><hr>

| <-- Previous Unit | Home | Next Unit -->
| --- | --- | --- 
|  [#1 - Intro to the Drawing Context](1-canvas-intro-to-drawing-context.md) |  [**IGME-330**](../README.md) | [**Skill #3 - TBA**]()
