# 3 - Machine Learning with ml5 - Pose Detection

## I. Overview
- **PoseNet** is a machine learning model that allows for Real-time Human Pose Estimation
  - https://learn.ml5js.org/#/reference/posenet

<hr>

## II. API

- The pose data we get back from the API looks like this - an `x`, a `y`, and a `confidence` value for multiple locations of a body
- Below we can see that these locations are named:

```
pose:
  keypoints: (17) [{…}, {…}, {…}, {…}, {…}, {…}, {…}, {…}, {…}, {…}, {…}, {…}, {…}, {…}, {…}, {…}, {…}]
  leftAnkle: {x: 599.1597746318416, y: 494.98787727801255, confidence: 0.0012563241180032492}
  leftEar: {x: 453.69841223097035, y: 243.16036951681053, confidence: 0.5885285139083862}
  leftElbow: {x: 656.4851325959083, y: 524.3184439217534, confidence: 0.01574356108903885}
  leftEye: {x: 427.34051656166406, y: 210.8243997180508, confidence: 0.9987946152687073}
  leftHip: {x: 511.92643577486626, y: 513.2484204481548, confidence: 0.0015425400342792273}
  leftKnee: {x: 605.6700555823656, y: 440.8782258386278, confidence: 0.0018843129510059953}
  leftShoulder: {x: 546.5062336606275, y: 383.60506347181274, confidence: 0.9093210697174072}
  leftWrist: {x: 644.0373194356837, y: 507.3040159945358, confidence: 0.005719129927456379}
  nose: {x: 398.29327215944284, y: 233.91148429900295, confidence: 0.999527096748352}
  rightAnkle: {x: 157.13915843444113, y: 498.5294403640213, confidence: 0.0026795780286192894}
  rightEar: {x: 292.11110987088097, y: 235.13465614170417, confidence: 0.9823558926582336}
  rightElbow: {x: 100.91644287109375, y: 499.3624140223641, confidence: 0.016158990561962128}
  rightEye: {x: 361.0062862648574, y: 203.81996600080555, confidence: 0.9998224973678589}
  rightHip: {x: 240.868740156003, y: 515.7029599438382, confidence: 0.0039060795679688454}
  rightKnee: {x: 139.3682766331773, y: 480.2924581446073, confidence: 0.008052365854382515}
  rightShoulder: {x: 189.40683802741975, y: 372.3791877954386, confidence: 0.9166773557662964}
  rightWrist: {x: 125.657828958118, y: 508.26836493228666, confidence: 0.004718870855867863}
  score: 0.37980522320140153
```

- There is also a `skeleton` array that will have values for body locations at the shoulder level or lower

```
pose: {score: 0.39227001670309725, keypoints: Array(17), nose: {…}, leftEye: {…}, rightEye: {…}, …}
skeleton: Array(1)
  0: Array(2)
    0:
      part: "leftShoulder"
      position: {x: 584.6195324849526, y: 264.7412002504104}
      score: 0.8373012542724609
    1:
      part: "rightShoulder"
      position: {x: 157.6269431800694, y: 254.8937783445366}
      score: 0.9107379913330078
```


<hr>

## III. Code

- The PoseNet docs and quick start code are here:
  - https://learn.ml5js.org/#/reference/posenet?id=quickstart
- There is some sample code for drawing the skeleton `drawSkeleton()`,  and keypoints `drawKeypoints()`, both utilizing canvas - we adapt it below - it came from here:
  - https://github.com/ml5js/ml5-library/blob/main/examples/javascript/PoseNet/PoseNet_webcam/sketch.js
- Here is the demo code, we'll walk throught how it works in class:

**posenet-1.html**

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta http-equiv="X-UA-Compatible" content="IE=edge">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>ML5 Posenet Test</title>
    <script src="https://unpkg.com/ml5@latest/dist/ml5.min.js"></script>
    <!-- <script src="https://cdn.jsdelivr.net/npm/ml5@0.10.6/dist/ml5.min.js"></script> -->
		<style>
    	* {
				box-sizing: border-box;
			}

			body {
				font-family:sans-serif;
				margin:0; padding:0;
			}

			div {
				padding:10px;
			}

			#image img {
				width:100%;
			}
			
			video{
				display: none;
			}
			
			canvas{
				transform: scaleX(-1);
			}
    </style>
  </head>
  <body>
    <canvas width="640" height="360"></canvas> 
    <video width="640" height="360" autoplay></video>
    <div id="msg">Loading...</div>

		<script>
		let canvas, div, ctx, video, poseNet;
		let poses = [];


		// I. CALLBACKS
		// When the model is loaded
		const modelLoaded = () => {
			console.log("Model Loaded!");
			div.innerHTML = "PoseNet model loaded!";
		};


		// II. SETUP
		const setupUI = () => {
			div = document.querySelector("#msg");
			canvas = document.querySelector("canvas");
			ctx = canvas.getContext("2d");
		};

		const setupVideo = () => {
			// Create a webcam capture
			video = document.querySelector("video");
			if (navigator.mediaDevices && navigator.mediaDevices.getUserMedia) {
				navigator.mediaDevices.getUserMedia({ video: true }).then(function(stream) {
					video.srcObject = stream;
					video.play();
				
					/* double check your webcam width / height */
					const stream_settings = stream.getVideoTracks()[0].getSettings();
					console.log('Width: ' + stream_settings.width);
					console.log('Height: ' + stream_settings.height);
				});
			}
		};

		const setupPosenet = () => {
			// Create a new poseNet instance
			poseNet = ml5.poseNet(video, modelLoaded);
			// Listen to new 'pose' events
			poseNet.on('pose', results => {
				poses = results;
			});
		};

		// III. UTILS
		// Note that we are drawing eveything from the "center"
		// which is a good idea becaue the canvas is flipped on its x-axis
		// meaning that (0,0) is in the upper-right corner
		const fillRect = (ctx,x,y,width,height,fillStyle="white") => {
			ctx.save();
			ctx.translate(x,y);
			ctx.fillStyle=fillStyle;
			ctx.fillRect(-width/2,-height/2,width,height)
			ctx.restore();
		};

		const strokeRect = (ctx,x,y,width,height,strokeStyle="white",lineWidth=5) =>{
			ctx.save();
			ctx.translate(x,y);
			ctx.strokeStyle=strokeStyle;
			ctx.lineWidth=lineWidth;
			ctx.strokeRect(-width/2,-height/2,width,height);
			ctx.restore();
		}

		const fillCircle = (ctx,x,y,radius,fillStyle="white",startAngle=0,endAngle=Math.PI*2,counterClockwise=false) =>{
			ctx.save();
			ctx.translate(x,y);
			ctx.fillStyle=fillStyle;
			ctx.beginPath();
			ctx.arc(0,0,radius,startAngle,endAngle,counterClockwise);
			ctx.closePath();
			ctx.fill();
			ctx.restore();
		}

		const strokeCircle = (ctx,x,y,radius,strokeStyle="white",lineWidth=5,startAngle=0,endAngle=Math.PI*2,counterClockwise=false) =>{
			ctx.save();
			ctx.translate(x,y);
			ctx.strokeStyle=strokeStyle;
			ctx.lineWidth=lineWidth;
			ctx.beginPath();
			ctx.arc(0,0,radius,startAngle,endAngle,counterClockwise);
			ctx.closePath();
			ctx.stroke();
			ctx.restore();
		}

		// IV. MAIN

		const drawKeypoints = () => {
			// Loop through all the poses detected
			for (let i = 0; i < poses.length; i += 1) {
				// For each pose detected, loop through all the keypoints
				for (let j = 0; j < poses[i].pose.keypoints.length; j += 1) {
					let keypoint = poses[i].pose.keypoints[j];
					// Only draw an ellipse is the pose probability is bigger than 0.2
					if (keypoint.score > 0.2) {
						strokeCircle(ctx,keypoint.position.x, keypoint.position.y, 10, "red");
					}
				}
			}
			ctx.restore();
		};

		// A function to draw the skeletons
		const drawSkeleton = () => {
			ctx.save();
			ctx.strokeStyle = "red";
			ctx.lineWidth = 3;
			// Loop through all the skeletons detected
			for (let i = 0; i < poses.length; i += 1) {
				// For every skeleton, loop through all body connections
				for (let j = 0; j < poses[i].skeleton.length; j += 1) {
					let partA = poses[i].skeleton[j][0];
					let partB = poses[i].skeleton[j][1];
					ctx.beginPath();
					ctx.moveTo(partA.position.x, partA.position.y);
					ctx.lineTo(partB.position.x, partB.position.y);
					ctx.stroke();
				}
			}
			ctx.restore();
		};

		const drawStuff = () => {
			for (let item of poses){
				const leftEye = item.pose.leftEye;
				const rightEye = item.pose.rightEye;
				
				// draw a green translucent rectangle over where the eyes are
				if(leftEye && rightEye){
					ctx.save();
					ctx.beginPath();
					ctx.moveTo(leftEye.x+30,leftEye.y -15);
					ctx.lineTo(rightEye.x-30,rightEye.y-15);
					ctx.lineTo(rightEye.x-30,rightEye.y+15);
					ctx.lineTo(leftEye.x+30,leftEye.y+15);
					ctx.closePath();
					ctx.fillStyle = "green";
					ctx.globalAlpha = .4;
					ctx.fill();
					ctx.stroke();
					ctx.restore();
				}

				// now draw creepy eyes!
				if(leftEye){
					strokeRect(ctx,leftEye.x,leftEye.y,30,30,"yellow",3);
					fillCircle(ctx,leftEye.x,leftEye.y,10,"white");
					fillCircle(ctx,leftEye.x,leftEye.y,4,"black");
				}

				if(rightEye){
					strokeRect(ctx,rightEye.x,rightEye.y,30,30,"yellow",3);
					fillCircle(ctx,rightEye.x,rightEye.y,10,"white");
					fillCircle(ctx,rightEye.x,rightEye.y,4,"black");
				}

				// draw with your hands!
				// Head to `loop()` and uncomment/comment some code to try it
				const leftWrist = item.pose.leftWrist;
				const rightWrist = item.pose.rightWrist;
				if(leftWrist && leftWrist.confidence > 0.2){
					fillCircle(ctx,leftWrist.x,leftWrist.y,50,"rgba(128,0,128,.5)");
					strokeCircle(ctx,leftWrist.x,leftWrist.y,50,2);
				}
				if(rightWrist && rightWrist.confidence > 0.2){
					fillCircle(ctx,rightWrist.x,rightWrist.y,50,"rgba(0,255,0,.5)");
					strokeCircle(ctx,rightWrist.x,rightWrist.y,50,2);
				}
			}
		};

		// https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/Optional_chaining
		const updateUI = () => {
			for (let item of poses){
				div.innerHTML = `
					<p><b>Left Eye</b>: (${(item.pose.leftEye?.x)?.toFixed(2)},${(item.pose.leftEye?.y)?.toFixed(2)}) - confidence = ${(item.pose.leftEye?.confidence)?.toFixed(2)}</p>
					<p><b>Right Eye</b>: (${(item.pose.rightEye?.x)?.toFixed(2)},${(item.pose.rightEye?.y)?.toFixed(2)}) - confidence = ${(item.pose.rightEye?.confidence)?.toFixed(2)}</p>
					<p><b>Nose</b>: (${(item.pose.nose?.x)?.toFixed(2)},${(item.pose.nose?.y)?.toFixed(2)}) - confidence = ${(item.pose.nose?.confidence)?.toFixed(2)}</p>
					<p><b>Left Ear</b>: (${(item.pose.leftEar?.x)?.toFixed(2)},${(item.pose.leftEar?.y)?.toFixed(2)}) - confidence = ${(item.pose.leftEar?.confidence)?.toFixed(2)}</p>
					<p><b>Right Ear</b>: (${(item.pose.rightEar?.x)?.toFixed(2)},${(item.pose.rightEar?.y)?.toFixed(2)}) - confidence = ${(item.pose.rightEar?.confidence)?.toFixed(2)}</p>
					`;
			}
		};

		const loop = () => {
			requestAnimationFrame(loop);
			//console.log(poses);
			ctx.drawImage(video, 0, 0, 640, 360);
			// ctx.save();
			// ctx.fillStyle = "rgb(0,0,0,.01)";
			// ctx.fillRect(0,0,640,360);
			// ctx.restore();
			drawKeypoints();
			drawSkeleton();
			drawStuff();
			updateUI();
		};

		const init = () => {
			setupUI();
			setupVideo();
			setupPosenet();
			loop();
		};

		init();
		</script>
    
  </body>
</html>
```


<hr>

## IV. Resources
- https://learn.ml5js.org/#/reference/posenet
- https://examples.ml5js.org/


<hr><hr>

**[Previous Chapter <- 2 - Machine Learning with ml5 - Object Detection](2-ml-object-detection.md)**
