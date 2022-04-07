# 2 - Machine Learning with ml5 - Object Detection

## I. Overview
- The [ml5 Object Detector API](https://learn.ml5js.org/#/reference/object-detector) can detect multiple specific objects in an image, and give us an `x`, `y`, `width`, `height` and a `confidence` value for each object
- For a model, we will use the Microsoft [COCO - Common Objects in Context](https://cocodataset.org/#explore) - which contains "complex everyday scenes of common objects in their natural context"
- What is the COCO Dataset? - https://viso.ai/computer-vision/coco-dataset/
- List of COCO object classes:

`'person', 'bicycle', 'car', 'motorcycle', 'airplane', 'bus', 'train', 'truck', 'boat', 'traffic light', 'fire hydrant', 'stop sign', 'parking meter', 'bench', 'bird', 'cat', 'dog', 'horse', 'sheep', 'cow', 'elephant', 'bear', 'zebra', 'giraffe', 'backpack', 'umbrella', 'handbag', 'tie', 'suitcase', 'frisbee', 'skis','snowboard', 'sports ball', 'kite', 'baseball bat', 'baseball glove', 'skateboard', 'surfboard', 'tennis racket', 'bottle', 'wine glass', 'cup', 'fork', 'knife', 'spoon', 'bowl', 'banana', 'apple', 'sandwich', 'orange', 'broccoli', 'carrot', 'hot dog', 'pizza', 'donut', 'cake', 'chair', 'couch', 'potted plant', 'bed', 'dining table', 'toilet', 'tv', 'laptop', 'mouse', 'remote', 'keyboard', 'cell phone', 'microwave', 'oven', 'toaster', 'sink', 'refrigerator', 'book', 'clock', 'vase', 'scissors', 'teddy bear', 'hair drier', 'toothbrush'`

- List of COCO keypoint classes (for poses):

`"nose", "left_eye", "right_eye", "left_ear", "right_ear", "left_shoulder", "right_shoulder", "left_elbow", "right_elbow", "left_wrist", "right_wrist", "left_hip", "right_hip", "left_knee", "right_knee", "left_ankle", "right_ankle"`

<hr>

## II. Creating an Object Detector that utilizes the webcam

- ml5 `ObjectDetector` documentation & code example:
  - https://learn.ml5js.org/#/reference/object-detector
  - https://github.com/ml5js/ml5-library/tree/main/examples/javascript/ObjectDetector/COCOSSD_webcam
- Here is the completed code:

**object-detect-webcam-1.html**

```html
<!DOCTYPE html>
<html lang="en">
  <head>
		<title>Real time Object Detection using CocoSsd</title>
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <script src="https://unpkg.com/ml5@latest/dist/ml5.min.js"></script>
		<style>
			body{
				font-family: sans-serif;
			}
			canvas{
				background-color: #ddd;
				/* transform: scaleX(-1); */
				/* display:none; */
			}
			video{
				display: none;
			}
		</style>
	
	</head>

  <body>
		<h1>Real time Object Detection using CocoSsd</h1>
		<video></video>
		<canvas></canvas>
		<p id="status"></p>
		
		<script>
		// code from https://github.com/ml5js/ml5-library/tree/main/examples/javascript/ObjectDetector/COCOSSD_webcam
		// Copyright (c) 2019 ml5
//
// This software is released under the MIT License.
// https://opensource.org/licenses/MIT

/* ===
ml5 Example
Real time Object Detection using objectDetector
=== */
"use strict";

let objectDetector;
let status;
let objects = [];
let video;
let canvas, ctx;
const width = 480;
const height = 360;

window.onload = init;

async function init() {
  // init status & canvas & ctx
  status = document.querySelector("#status");
  status.innerHTML = "... loading model ...";
  canvas = document.querySelector("canvas");
  canvas.width = width;
  canvas.height = height;
  ctx = canvas.getContext('2d');

  // get the video
  video = await setupVideo();

  // load ml5 objectDetector model
  objectDetector = await ml5.objectDetector('cocossd', startDetecting)
}

function startDetecting(){
  status.textContent = "Model ready";
  detect();
}

function detect() {
  objectDetector.detect(video, (error, results) => {
    if(error){
      console.log(error);
      return
    }
    objects = results;

    if(objects){
      draw();
			status.innerHTML = objects.map(obj => `<p><b>${obj.label}</b> - x: ${obj.x.toFixed(0)}, y: ${obj.y.toFixed(0)}, width: ${obj.width.toFixed(0)}, height: ${obj.height.toFixed(0)}, confidence: ${obj.confidence.toFixed(4)}</p>`).join("");
    }else{
			status.innerHTML = "... detecting ...";
		}
    // keep detecting!
    detect();
  });
}

function draw(){
  ctx.save();
  ctx.fillStyle = "black";
  ctx.fillRect(0,0, width, height);

  ctx.drawImage(video, 0, 0);
  ctx.font = "16px Arial";
  ctx.fillStyle = "red";
  for (let i = 0; i < objects.length; i += 1) {
    ctx.fillText(objects[i].label, objects[i].x + 4, objects[i].y + 16); 
    ctx.beginPath();
    ctx.rect(objects[i].x, objects[i].y, objects[i].width, objects[i].height);
    ctx.strokeStyle = "green";
    ctx.stroke();
    ctx.closePath();
  }
  ctx.restore();
}

// Helper Functions
async function setupVideo(){
	const videoElement = document.querySelector("video");
  videoElement.width = width;
  videoElement.height = height;

  // Create a webcam capture
  const capture = await navigator.mediaDevices.getUserMedia({ video: true })
  videoElement.srcObject = capture;
  videoElement.play();

  return videoElement
}
  </script>
  </body>
</html>
```

<hr>

## III. Resources
- COCO - Common Objects in Context - https://cocodataset.org/#explore
- ml5:
  - https://learn.ml5js.org/#/reference/object-detector
  - JS code examples: https://github.com/ml5js/ml5-library/tree/main/examples/javascript/ObjectDetector


<hr><hr>

**[Previous Chapter <- 1 - Machine Learning with ml5 - Image Classification](1-ml-pre-trained-models.md)**

**[Next Chapter -> 3 - Machine Learning with ml5 - PoseNet](3-ml-posenet.md)**
