# Web Audio VI - Bitmap effects

## I. Overview

- `ctx.getImageData(x, y, width, height)` returns an array of RGBA values which we can manipulate in various ways, and then copy back to the canvas with `ctx.putImageData(x, y, width, height)`
- You have already had a chance to do this in [HW - Audio Visualizer - Part III](./HW-AV-2195-3.md)

## II. Getting `imageData` from video
- In the demos below we are sampling the contents of a &lt;video> element and the user's Webcam 60 times a second, copying the frame to a &lt;canvas> element, 



- `ctx.drawImage()` 

## II-A. Manipulating the image data of a video file

- Video Filters Example: http://igm.rit.edu/~acjvks/courses/2014-spring/450/code/getImageData-putImageData-demo/video-image-data-demo-3.html

## II-B. Webcam input
- Below, we will grab the contents of the webcam and copy it to a &lt;canvas> element 60 times a second - no  &lt;video> element is required
**The examples below that rely on a Webcam only work reliably in Chrome:**
- Webcam Example: https://igm.rit.edu/~acjvks/courses/2014-spring/450/code/video/webcam-image-data-demo.html
- Webcam plus Motion Detect Example: https://igm.rit.edu/~acjvks/courses/2014-spring/450/code/video/webcam-image-data-demo-2.html
- Webcam plus Face Detect Example: https://igm.rit.edu/~acjvks/courses/2014-spring/450/code/video/webcam-image-data-demo-3.html
- Webcam sunglasses app: https://igm.rit.edu/~acjvks/courses/2014-spring/450/code/video/JS-Object-Detect/js-objectdetect-master/examples/example_sunglasses_jquery.htm
- Webcam head tracker app:  https://igm.rit.edu/~acjvks/courses/2014-spring/450/code/headtracker/headtracker2.html

## III.  Image filters as matrix operations

<hr><hr>

**[Previous Chapter <- Web Audio V](demo-web-audio-5.md)**
