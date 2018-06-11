# Study Guide 1

## Overview

- The &lt;canvas> tag defines an area on the page that we can draw into using a procedural drawing API. This bitmap drawing API has methods for drawing lines, paths, rectangles, arcs, circles, curves, and text. 
- Apple invented the canvas 2D drawing API in 2004 as a way to add customized dashboard widgets to OS X. It has since been adopted by all major desktop and mobile  browsers and is supported by the current versions of Chrome, Firefox, Internet Explorer (8>), Konquerer, and Opera.
- The canvas drawing API allows a developer to create Flash-like (do you remember Adobe Flash?) games and experiences without using the Flash SDK and with no need for a browser plug-in.

## Resources
- The canvas API is focused on drawing, and is fairly lightweight. The full specification is here: http://www.w3.org/TR/2dcontext/
- Our free canvas "textbook" is located here: https://developer.apple.com/library/safari/documentation/AudioVideo/Conceptual/HTML-canvas-guide/Introduction/Introduction.html
- Another great online reference is here: https://developer.mozilla.org/en-US/docs/Web/API/Canvas_API/Tutorial

## I. About Canvas
**Read the "At a glance" section under *About Canvas*** - 

https://developer.apple.com/library/safari/documentation/AudioVideo/Conceptual/HTML-canvas-guide/Introduction/Introduction.html 

and answer the following questions:

A. You can add a Canvas element with a few lines of code 

*(no answer required - we'll do this in the next section)*


B. There are Methods for Drawing _______



*You draw shapes other than rectangles by creating a path, adding line segments, curves, or arcs, and closing the path. Begin a path using beginPath(). Set the starting point, or start a discontinuous subpath, by calling the moveTo(x, y) method. The closePath() method draws a line from the current endpoint to the starting point of the path, creating a closed shape.*

The path is not actually drawn until you _______

Canvas supports matrix transforms—anything you draw can be _______

C. It's Easy To Include _______

D. You Can Also Render _______

E. Canvas is Great for InfoGraphics - give examples:


F. Canvas Can Create Fast, Lightweight Animations.

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

