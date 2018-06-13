# Study Guide 1

## I. Overview

- The &lt;canvas> tag defines an area on the page that we can draw into using a procedural drawing API. This bitmap drawing API has methods for drawing lines, paths, rectangles, arcs, circles, curves, text, images, and video. 
- Apple invented the canvas 2D drawing API in 2004 as a way to add customized dashboard widgets to OS X. It has since been adopted by all major desktop and mobile  browsers and is supported by the current versions of Chrome, Firefox, Internet Explorer (8>), Konquerer, and Opera.
- The canvas drawing API allows a developer to create Flash-like (do you remember Adobe Flash?) games and experiences without using the Flash SDK and with no need for a browser plug-in.
- We will be utlizing the online MDN canvas tutorial located here: https://developer.mozilla.org/en-US/docs/Web/API/Canvas_API

### I-A. Hello World

- Take a look at the canvas example here - https://developer.mozilla.org/en-US/docs/Web/API/Canvas_API - note that you can manipulate the examples here and get live updates. 

**Things to try:**
- Go ahead and modify the `.fillStyle` property to change the color of the rectangle from `green` to `purple`
- Now change the color of the rectangle to a dark gray - use a hexidecimal value like `#333`
- Change the height of the rectangle from `100` to `50`
- Change the width of the rectangle from `100` to `600` (which makes it wider than the available space)
- Change the x and y values of the rectangle from `10,10` to `25,25`

### I-B. Example
Here is a full working version of the MDN example - note that we are using a slightly different JavaScript style than the examples, but the core canvas concepts are the same.

**sg1-1.html**

```
<!DOCTYPE html>
<html lang="en">
<head>
	<meta charset="utf-8" />
	<title></title>
</head>
<body>

<canvas id="canvas"></canvas>
<script>
	// get reference to <canvas> element>
	let canvas = document.querySelector('#canvas');
	
	// get reference to drawing "context" (i.e. the canvas API)
	let ctx = canvas.getContext('2d');

	// set all "fill" operations to green
	ctx.fillStyle = 'green';
	
	// create a green rectangle starting at 10,10 - and make it 50x50 pixels
	ctx.fillRect(10, 10, 100, 100);
</script>
</body>
</html>
```

### I-C. Resources
- The canvas API is focused on drawing, and is fairly lightweight. The full specification is here: http://www.w3.org/TR/2dcontext/
- Another great online reference is here: https://developer.apple.com/library/safari/documentation/AudioVideo/Conceptual/HTML-canvas-guide/Introduction/Introduction.html
- Also note the list of resources at the end of the MDN page.


## II. Basic Usage

MDN Page: https://developer.mozilla.org/en-US/docs/Web/API/Canvas_API/Tutorial/Basic_usage

### II-A. Review Questions

Read this page over an answer the following questions:

A. What is the default size of the &lt;canvas> element?

B. Give at least 3 CSS properties that can be set for the &lt;canvas>

C. How would you specify "fallback" text - for example "Get a real browser!" - for browsers that do not support &lt;canvas>? Give an example.


### II-B. A Simple Example

Here is our version of the MDN "simple example". Note that we are NOT testing for the existance of canvas as it is already widely supported by modern web browsers.

**sg1-2.html**

```

```



## I. About Canvas


https://developer.mozilla.org/en-US/docs/Web/API/Canvas_API

and answer the following questions:

**A. You can add a Canvas element with a few lines of code**

*(no answer required - we'll do this in the next section)*


**B. There are Methods for Drawing ______**

*You draw shapes other than rectangles by creating a path, adding line segments, curves, or arcs, and closing the path. Begin a path using beginPath(). Set the starting point, or start a discontinuous subpath, by calling the moveTo(x, y) method. The closePath() method draws a line from the current endpoint to the starting point of the path, creating a closed shape.*

**B-i. The path is not actually drawn until you _______**

**B-ii. Canvas supports matrix transforms — anything you draw can be _______**

**C. It's Easy To Include _______**

**D. You Can Also Render _______**

**E. Canvas is Great for InfoGraphics - give examples:**

**F. Canvas Can Create Fast, Lightweight Animations.**

*(no answer required  - note: Apple's examples use `setInterval()` for animation - we’ll instead be using `requestAnimationFrame()` in our examples)*

G. You Can Manipulate Pixels Directly for Image Processing - give examples:

H. Make Games That Play on Desktop and iOS Devices.
(or Android, Blackberry, Windows, … - no answer required )

I. The Web Inspector Provides Built-in JavaScript Debugging

- To access the Web Inspector on Chrome and Safari, right-click in the browser window and select "Inspect Element" to bring up the debugger. On Apple's Safari browser, you’ll first have to Choose Safari > Preferences > Advanced and check the "Show Develop in menu bar" box.

*no answer required*

J. Export to Canvas is Possible from Illustrator or Flash

*no answer required*

<hr><hr>

## II. Setting Up the Canvas

1) Read over the "Setting Up the Canvas" section - the following steps are listed:

- Start by Adding a &lt;canvas> Tag

- Specify the Fallback Behavior

- Create a Drawing Context

- Support Retina Displays from the Start
  - *a good practice, but we're not going to worry about this in the course*

- Save and Restore the Context
  - *we'll get into this soon*

