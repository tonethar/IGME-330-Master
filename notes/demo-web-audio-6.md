# Web Audio VI - Bitmap effects

## I. Overview

- `ctx.getImageData(x, y, width, height)` returns an array of RGBA values which we can manipulate in various ways, and then copy back to the canvas with `ctx.putImageData(x, y, width, height)`
- You have already had a chance to do this in [HW - Audio Visualizer - Part III](./HW-AV-2195-3.md) - so let's experiment with some additional effects we can apply

<hr>

## II. Getting `imageData` from video
- In the demos below we are:
  1) sampling the contents of a &lt;video> element or the user's Webcam 60 times a second
  2) copying the video source's current frame to a &lt;canvas> element with `ctx.drawImage()`
  3) getting a reference to the &lt;canvas> `imageData` (which is a `Uint8ClampedArray`) with `ctx.getImageData(x, y, width, height)`
  4) looping through this typed array, and modifying some of its values
  5) putting the modified array of data back onto the &lt;canvas> with `ctx.putImageData(x, y, width, height)`
- The source code and video files for these demo are NOT in myCourses, so be sure to:
  - follow along with the demos
  - "inspect" the source code of the demos to see how the various effects are accomplished
  - put in break points so that you can understand how the program flow works, as well as inspect the values of the variables

### II-A. Manipulating the image data of a video file

- Video Filters Example: http://igm.rit.edu/~acjvks/courses/2014-spring/450/code/getImageData-putImageData-demo/video-image-data-demo-3.html
- Here we have the following effects:
  - Invert (seen in AV - Part III)
  - Noise (seen in AV - Part III)
  - Emboss (seen in AV - Part III, and is a more interesting effect because the value of each pixel is dependent on neighboring pixels)
  - Tint
  - Desaturate
  - Sepia
  - Shift RGB (similar to Invert)
  
<hr>

## III. Webcam input
- Below, we will grab the contents of the webcam and copy it to a &lt;canvas> element 60 times a second - no  &lt;video> element is required
- these webcam examples only reliably work in Chrome

### III-A. 
- Webcam Example: https://igm.rit.edu/~acjvks/courses/2014-spring/450/code/video/webcam-image-data-demo.html

### III-B. 
- Webcam plus Motion Detect Example: https://igm.rit.edu/~acjvks/courses/2014-spring/450/code/video/webcam-image-data-demo-2.html

### III-C. 
- Webcam plus Face Detect Example: https://igm.rit.edu/~acjvks/courses/2014-spring/450/code/video/webcam-image-data-demo-3.html

### III-D. 
- Webcam sunglasses app: https://igm.rit.edu/~acjvks/courses/2014-spring/450/code/video/JS-Object-Detect/js-objectdetect-master/examples/example_sunglasses_jquery.htm

### III-E. 
- Webcam head tracker app:  https://igm.rit.edu/~acjvks/courses/2014-spring/450/code/headtracker/headtracker2.html

<hr>

## IV.  Image filters as matrix operations

<hr><hr>

**[Previous Chapter <- Web Audio V](demo-web-audio-5.md)**
