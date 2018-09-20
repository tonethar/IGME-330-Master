# Canvas Image Data Demo

## I. Overview
- Here we will:
  - review hooking up DOM controls to canvas
  - play with blending mode a little more
  - grab the image data from the canvas, perform manipulations on that data, and copy it back to the canvas
  - see the effects of drawing an insecure image on the canvas 
  - think about you could potentially use all of this in your Audio Visualizer project - including having the audio frequency data effect the motion of sprites
  - think about how you incorporate mouse movement into this demo or your audio visualizer project. See the *Speed Circles* demo in mycourses for JS code that accesses the mouse position
- Other stuff to note:
  - be sure to look the code over and ask questions about anything you don't understand - there's a lot here!
  - everything will still work even if we change the `height` and `width` attributes of the &lt;canvas>
  - an IFFE
  - a handy helper function for creating gradients
  - creating sprite instances using object literals and a factory function. This is the first of the multiple ways to create objects we will be looking at this semester
  - note that these sprites use vectors for movement - so if you've already taken IGME-202 you can put that some of that flocking code to work if you wish
  - this is a lot of code to put in one file! We will soon look at how to split this into multiple *modules*, and go beyond merely copying chunks of code to distinct JS files

## II. Start Files

See comments #1 - #6 in the source code. We will walk through these steps together in class, but feel free to modify these effects to make them more interesting.
- #1  - Show Trails
- #2  - Show Blending
- #3  - Show Noise
- #4  - Show Tint
- #5  - Show Image
- #6  - Stop using an insecure image

**sprite-literals-and-filters-start.html**

```html
<!DOCTYPE html>
<html lang="en">
<head>
	<meta charset="utf-8" />
	<title>Sprite Literals and Filters Start</title>
	<style>span{font-family:sans-serif;margin-right:2em;}</style>
</head>
<body>
<canvas id="mycanvas" width="800" height="600"></canvas>
<p>
	<span><label for="trailsCB">Trails</label><input type="checkbox" id="trailsCB"></span>
	<span><label for="blendingCB">Funky Blending</label><input type="checkbox" id="blendingCB"></span>
	<span><label for="noiseCB">Red Noise</label><input type="checkbox" id="noiseCB"></span>
	<span><label for="tintCB">Magenta Tint</label><input type="checkbox" id="tintCB"></span>
	<span><label for="showImageCB">Show Image</label><input type="checkbox" id="showImageCB"></span>
</p>
	<script>
	(function(){
		"use strict";
		const ctx = document.querySelector("canvas").getContext("2d");
		const canvasWidth = mycanvas.width;
		const canvasHeight = mycanvas.height;
		let sprites = []; // an array to hold all of our sprites
		let gradient = getLinearGradient(0,0,0,canvasHeight,[{percent:0,color:"blue"},{percent:.25,color:"green"},{percent:.5,color:"yellow"},{percent:.75,color:"red"},{percent:1,color:"magenta"}])
		let image = new Image();
		// #6 - stop using an insecure image
		image.src = "https://vignette.wikia.nocookie.net/yoshi/images/6/68/Yoshi_Happy.png/revision/latest?cb=20150508143229";
		//image.src = "Yoshi_Happy.png";
		let showNoise,showBlending,showTint,showImage,showTrails = false;

		init();

		function init(){
			sprites = createSprites();
			setupUI();
			loop();
		}
		
		function setupUI(){
			// YOU DO - we will need one of these lines per checkbox
			document.querySelector('#trailsCB').checked = showTrails;
			
			// YOU DO - we will need one of these lines per checkbox
			document.querySelector('#trailsCB').onchange = e => showTrails = e.target.checked;
			
		}

		function loop(){
			// schedule a call to loop() in 1/60th of a second
			requestAnimationFrame(loop);
	
			// draw background
			ctx.save();
			ctx.fillStyle = gradient;
			// #1 Show Trails
			//if (showTrails) ctx.globalAlpha = 0.05;
			ctx.fillRect(0,0,canvasWidth,canvasHeight);
			ctx.restore();
	
			// #5 Show Image
			
		
	
			// loop through sprites
			ctx.save();
			let counter = 0;
			for (let s of sprites){
				// move sprites
				s.move();

				// check sides and bounce
				if (s.x <= s.radius || s.x >= canvasWidth-s.radius){
					s.reflectX();
					s.move();
				}
				if (s.y <= s.radius || s.y >= canvasHeight-s.radius){
					s.reflectY();
					s.move();
				}
	
				// draw sprites
				ctx.save();
				counter ++;
	
				// #2 - show blending
	
				s.draw(ctx);
				ctx.restore();
		
			} // end for
			ctx.restore();
			
			
			// Bitmap Manipulation
			let imageData = ctx.getImageData(0, 0, canvasWidth, canvasHeight);
			let data = imageData.data;
			let length = data.length;
			let width = imageData.width; // not using here
			// Iterate through each pixel
			for (let i = 0; i < length; i +=4) {
			
				// #3 - Show noise
				// red noise
				
				// #4 - Show tint
				// magenta tint
				
						
		
			}	// end for
			
			// copy data back to canvas
			ctx.putImageData(imageData, 0, 0);
			
			
		} // end loop()
		
		// FILTER FUNCTIONS
		

		// FACTORY FUNCTIONS
		function createSprites(num=20){
		// create array to hold all of our sprites
		let sprites = [];
		for(let i=0;i<num;i++){
			// create Object literal
			let s = { };
	
			// add properties
			s.radius = 10 + Math.random() * 15;;
			s.color = getRandomColor();
			s.x = Math.random() * (canvasWidth - 100) + 50;
			s.y = Math.random() * (canvasHeight - 100) + 50;
			s.fwd = getRandomUnitVector();
			s.speed = Math.random() + 2;
	
			//add methods
			s.draw = function(ctx){
					ctx.save();
					ctx.beginPath();
					ctx.arc(this.x, this.y, this.radius, 0, Math.PI*2, false);
					ctx.arc(this.x, this.y, this.radius/2, 0, Math.PI*2, true);
					ctx.closePath();
					ctx.fillStyle = this.color;
					ctx.fill();
					ctx.restore();
			};
		
			s.move = function(){
				this.x += this.fwd.x * this.speed;
				this.y += this.fwd.y * this.speed;
			};

			s.reflectX = function(){
				this.fwd.x *= -1;
			}

			s.reflectY = function(){
				this.fwd.y *= -1;
			}
		
			// add to array
			sprites.push(s);
		} // end for
	
		// return  array
		return sprites;
	}


	// UTILITY FUNCTIONS
		function getRandomUnitVector(){
			let x = getRandom(-1,1);
			let y = getRandom(-1,1);
			let length = Math.sqrt(x*x + y*y);
			if(length == 0){ // very unlikely
				x=1; // point right
				y=0;
				length = 1;
			} else{
				x /= length;
				y /= length;
			}

			return {x:x, y:y};
		}

		function getRandom(min, max) {
			return Math.random() * (max - min) + min;
		}
	
		function getRandomColor(){
			const getByte = _ => 35 + Math.round(Math.random() * 220);
			return `rgba(${getByte()},${getByte()},${getByte()},1)`;
		}
	
		function getLinearGradient(startX,startY,endX,endY,colorStops){
			let lg = ctx.createLinearGradient(startX,startY,endX,endY);
			for(let stop of colorStops){
				lg.addColorStop(stop.percent,stop.color);
			}
			return lg;
		}
	
	})();
	
	</script>
</body>
</html>

```



