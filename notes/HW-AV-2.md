# HW - Audio Visualizer - Part II

## I. Overview
In part II of this HW we will look at grabbing RGBa data from the canvas, and performing manipulations on it:
- [`ctx.getImageData(x,y,width,height)`](https://developer.mozilla.org/en-US/docs/Web/API/CanvasRenderingContext2D/getImageData) returns an [ImageData](https://developer.mozilla.org/en-US/docs/Web/API/ImageData) object
- [`ImageData.data`](https://developer.mozilla.org/en-US/docs/Web/API/ImageData/data) is a typed array - in this case a [`Uint8ClampedArray`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Uint8ClampedArray)
- "Photoshop-like" color manipulations we will do:
  - tint
  - invert
  - emboss
- Other effects
  - motion detection
  - object recognition

## II. Links from Exercise

**The examples that rely on a Webcam only work in Chrome:**

- Video Filters Example: http://igm.rit.edu/~acjvks/courses/2014-spring/450/code/getImageData-putImageData-demo/video-image-data-demo-3.html
- Web Cam Example: https://igm.rit.edu/~acjvks/courses/2014-spring/450/code/video/webcam-image-data-demo.html
- Web Cam plus Motion Detect Example: https://igm.rit.edu/~acjvks/courses/2014-spring/450/code/video/webcam-image-data-demo-2.html
- Web Cam plus Face Detect Example: https://igm.rit.edu/~acjvks/courses/2014-spring/450/code/video/webcam-image-data-demo-3.html
- Web Cam sunglasses app: https://igm.rit.edu/~acjvks/courses/2014-spring/450/code/video/JS-Object-Detect/js-objectdetect-master/examples/example_sunglasses_jquery.htm
- Web Cam head tracker app:  https://igm.rit.edu/~acjvks/courses/2014-spring/450/code/headtracker/headtracker2.html

## III. Submission
- the instructions are here: [Audio-Viz-ICE-2.pdf](_files/Audio-Viz-ICE-2.pdf)
- see the mycourses.rit.edu dropboxes for due date
