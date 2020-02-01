# Canvas II - More of the canvas API

 - **What is the canvas drawing API, and why is it worth knowing?**
   - It's a [stateful](https://en.wikipedia.org/wiki/State_(computer_science)) bitmap drawing API that is available on all modern web browsers - it's good to know how these kind of APIs work - as both iOS & Android have similar APIs for custom drawing
    
## I. Overview

- Let's review drawing *rectangles*, *circles* and *lines*
- New stuff:
  - draw rings (circles with the center punched out)
  - draw polygons
  - Canvas methods:
      - `ctx.arcTo()`
      - `ctx.setLineDash()`
  - Canvas properties:
    - `ctx.lineJoin` - <code>round|bevel|miter</code>



## II. Obtaining a *drawing context* object
   
- **Steps to getting a drawing context object**:
  - After the page loads, get a reference to a &lt;canvas> element: `let canvas = document.querySelector('canvas');`
  - Now get a reference to the drawing *context* like this: `let ctx = canvas.getContext('2d');`
  - `ctx` is a new `CanvasRenderingContext2D` object- this object has properties and methods that are listed here: https://www.w3.org/TR/2dcontext/#conformance-requirements
  - we could also turn the above 2 statements into a "one-liner" like this:
      
   `let ctx = document.querySelector('canvas').getContext('2d');`
      
## III. How to draw a Rectangle

  A) Optionally, `ctx.save()` (i.e. save or "push") the current value of all of the drawing state attributes so that you can easily restore them to their original values later. This also saves the CTM (current transformation matrix), which we will discuss soon
      
  B) Optionally, set the drawing state attributes (properties) that you wish to have values other than the defaults - for example `ctx.lineWidth`, `ctx.strokeStyle`, `ctx.fillStyle`, `ctx.globalAlpha` - a full list of state properties is here: https://www.w3.org/TR/2dcontext/#the-canvas-state
      
  C) Create a *path* for the rectangle like this:

```js
ctx.beginPath();
ctx.rect(x,y,width,height);
ctx.closePath();
```
      
  D) So we now have a path, but we can't see it. Now we need to stroke and/or fill the rectangular path like so. *Note that the order of these two calls **WILL** have an effect on the appearance of the drawing*:
     
```js
ctx.stroke();
ctx.fill();
```
     
  E) Optionally, `ctx.restore()` the drawing context state properties and CTM to their previous values

- The final version, which gives us a 200px by 200px yellow rectangle, with a 5 pixel thick (visible) red border, looks like this:

**drawin.html**

```html
<!DOCTYPE html>
<html lang="en">
<head>
	<meta charset="utf-8" />
	<title>Drawin'!</title>
	<style>
		canvas{border: 2px solid #ccc;}
	</style>
</head>
<body>
<canvas width="640" height="480"></canvas>
<script>
	let ctx = document.querySelector('canvas').getContext('2d');
	ctx.save();                 // A - optionally, save the drawing state attributes and CTM
	ctx.strokeStyle = "red";    // B - optionally, change the values of one or more drawing state attributes
	ctx.fillStyle = "yellow";   // B
	ctx.lineWidth = "10";       // B
	ctx.beginPath();            // C - describe a path
	ctx.rect(20,20,200,200);    // C
	ctx.closePath();            // C
	ctx.stroke();               // D - draw! i.e. make the path visible
	ctx.fill();                 // D - swap the order of stroke() and fill() to see what happens to the drawing
	ctx.restore();              // E - optionally, restore the saved values of drawing state attributes and CTM
</script>
</body>
</html>
```

\*\* ***Looks good, but note that we can only see 5 pixels of our 10-pixel stroke:*** \*\*

![square image](./_images/square.jpg)

\*\* ***By flipping the order of the stroke and fill calls, in this case calling `ctx.stroke()` AFTER `ctx.fill()`, we can change how the drawing looks. Below we can now see the entire 10-pixels of the stroke:*** \*\*

![square image](./_images/square-2.jpg)


## IV. How to draw a Circle

- virtually identical to drawing a rectangle, just replace the path code - `ctx.rect()` - with:
       
```js
  ctx.beginPath(); 
  ctx.arc(x, y, radius, startAngle, endAngle, counterclockwise);
  ctx.closePath(); 
```
       
 - here's an example:
     
```js
  ctx.beginPath(); 
  ctx.arc(200, 200, 125, 0, Math.PI * 2, false); // draws a circle at 200,200 with a 125-pixel radius
  ctx.closePath();
  ctx.stroke();
  ctx.fill();  
 ```
 
![circle image](./_images/circle.jpg)
 
## V. How to draw a Ring

 \*\* ***You can draw a 2D ring (or donut) shape by punching out the center. The trick is to create an inner arc with the `counterclockwise` value set to `true`  :*** \*\*
 
 ```js
  ctx.beginPath(); 
  ctx.arc(200, 200, 125, 0, Math.PI * 2, false); // draws a circle at 200,200 with a 125-pixel radius
  ctx.arc(200, 200, 100, 0, Math.PI * 2, true);  // punches out the center of the circle
  ctx.closePath();
  ctx.stroke();
  ctx.fill();  
 ```
 
  ![circle image](./_images/circle-2.jpg)

## VI. How to draw a Line

- just replace the path code - `ctx.rect()` - with:
     
```js
  ctx.beginPath(); 
  ctx.moveTo(20,100);  // start the "pen" at x=20, y=100 
  ctx.lineTo(620,100); // draw line to x=620, y=100
  ctx.closePath();
  ctx.stroke();
``` 
   
![line image](./_images/line.jpg)
    
## VI. How to draw a Polygon

- continue adding lines to our path:
     
```js
  ctx.beginPath(); 
  ctx.moveTo(20,100);  	// start the "pen" at x=20, y=100 
  ctx.lineTo(620,100); 	// point #1 -> draw line to x=620, y=100
  ctx.lineTo(340,400);	// point #2 -> draw line to x=340, y=400
  ctx.closePath(); 	// the path will automatically close back to point #1
  ctx.stroke();
  ctx.fill(); 
``` 

![triangle image](./_images/triangle.jpg)

\*\* ***If we stroke the line BEFORE closing the path, then it won't "auto close". See below:*** \*\*

```js
ctx.beginPath();      
ctx.moveTo(20,100);
ctx.lineTo(620,100);  // point #1
ctx.lineTo(340,400);	// point #2
ctx.stroke();         // stroke the path before closing it
ctx.closePath(); 
ctx.fill();
```

![triangle image](./_images/triangle-2.jpg)

\*\* ***If we set another drawing state attribute -  `ctx.lineJoin = "round";` - we get rounded corners. See below:*** \*\*
- other possible values for `.lineJoin` are `"bevel"` and `"miter"` (the default) --> https://developer.mozilla.org/en-US/docs/Web/API/CanvasRenderingContext2D/lineJoin

![triangle image](./_images/triangle-3.jpg)


\*\* ***If we set the line dash pattern -  `ctx.setLineDash([5, 15]);` - we get a dashed line. See below:*** \*\*

- **The dashes are 5px long, and the spaces between the dashes are 15px**
- You can see some other patterns here --> https://developer.mozilla.org/en-US/docs/Web/API/CanvasRenderingContext2D/setLineDash

![triangle image](./_images/triangle-4.jpg)

  - **#5 - How to draw curvilinear shapes**:
    - To draw curves, we can use `ctx.arcTo(CP-1x, CP-1y, CP-2x, CP-2y, radius) // CP = "Control Point"` to build up a path.
    
```js
  ctx.beginPath();
  ctx.moveTo(50, 100);             	// P0
  ctx.arcTo(300, 425, 550, 100, 80); 	// P1, P2 and the radius
  ctx.lineTo(550, 100);               // top line: line segment between P0 & P2     
  ctx.closePath();
  ctx.stroke();               
  ctx.fill();             
```
    
![arc-to image](./_images/arc-to.jpg)
    
- these are some nice reference and interactives about `ctx.arcTo()` here:
  - https://developer.mozilla.org/en-US/docs/Web/API/CanvasRenderingContext2D/arcTo
  - https://www.rgraph.net/blog/an-interactive-example-of-the-html5-canvas-arcto-function.html
  - in SG-2, you will see how to draw [bezier curves](https://en.wikipedia.org/wiki/Bézier_curve) using `ctx. quadraticCurveTo()` and `ctx.bezierCurveTo()`
  - **Try It Yourself:** How could you make just the straight line in the shape above *green* in color, while leaving the rest of the stroke *red* ?
      
## VII. Reference
- https://developer.mozilla.org/en-US/docs/Web/API/CanvasRenderingContext2D
- https://developer.mozilla.org/en-US/docs/Web/API/CanvasRenderingContext2D/setLineDash
- More on clipping: https://stackoverflow.com/questions/18988118/how-can-i-clip-inside-a-shape-in-html5-canvas

<hr><hr>

**[Previous Chapter <- Canvas Part I](canvas-1.md)**

**[Next Chapter -> Canvas Part III](canvas-3.md)**
