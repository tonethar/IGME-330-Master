# Demo: Canvas & Sprites

## I. Overview
- Here we will:
  - review ES6 class syntax and how to make a `Sprite` class
  - render these sprites to the screen using drawing context methods
  - look at how to utilize *inheritance* and *method overriding* to extend the functionality of the `Sprite` class
  - look at some handy utility methods that might come in useful when working on Project 1
- Helpful stuff (reusable code!) in demo file:
  - ES6 class: `Sprite`
  - Canvas Utility Functions: `createLinearGradient()`
  - General Utility Functions: `getRandom()`, `getRandomColor()`, `getRandomUnitVector()`
  
## II. Start Code

**sprites.html**

```html
<!DOCTYPE html>
<html lang="en">
<head>
	<meta charset="utf-8" />
	<title>ES6 Sprites & Canvas</title>
	<style>
		body{font-family:sans-serif;margin:2%;}
		code{font-size:1.1em;}
	</style>
</head>
<body>
<canvas id="mycanvas" width="1000" height="600"></canvas>

<h2>Helpful stuff (reusable code!) in here:</h2>
<ul>
	<li>ES6 class: <code>Sprite</code></li>
	<li>Canvas Utility Functions: <code>createLinearGradient()</code></li>
	<li>General Utility Functions: <code>getRandom()</code>, <code>getRandomColor()</code>, <code>getRandomUnitVector()</code></li>
</ul>
	<script>
	/*
	DISCUSSION: 
	1) First we'll walk though the app and make sure we understand all of this code
			
	2) We have 5 major sections of code for this demo - all jammed into the same file,
	as well as the variables and functions all being in the same "global" scope (namespace).
			
	3) Soon we will look at how we can re-factor code like this into separate files to 
	make it easier to work on, especially for a team, and how to place code into distinct 
	*modules* to make it more extensible and reliable
			
	IN-CLASS EXERCISE:
	1) Create a new class named `RingSprite` that extends `Sprite`
			
	2) In RingSprite, create a draw() method that will override the draw method in Sprite.
	It will draw a circle using ctx.arc() - Hint: use `this.span/2` to get the radius 
			
	3) In your sprite creation loop, modify the code to create a *ring* instead of
	a circle. See Week 2A for an example of where we drew a ring by 
	altering the `counterClockwise` parameter of ctx.arc()
		
	4) Move the JS code to 4 separate files (named **src/utils.js**, **src/canvas-utils.js**, 
	**src/sprites.js**, **src/main.js**) and link to them via multiple `<script>` tags. 
	Hint: **main.js** needs to load last 
			
	5) Finished early? Bored? Create another subclass of Sprite and add rotations or 
	other behaviors to it. 
	*/
		
		// I. CLASSES
		class Sprite{
			constructor(x=0,y=0,span=10,fwd={x:1,y:0},speed=0,color="black"){
				this.x = x;
				this.y = y;
				this.span = span;
				this.fwd = fwd;
				this.speed = speed;
				this.color = color;
			}
	
			draw(ctx){
				ctx.save();
				ctx.translate(this.x,this.y);
				ctx.beginPath();
				ctx.rect(-this.span/2,-this.span/2,this.span, this.span);
				ctx.closePath();
				ctx.fillStyle = this.color;
				ctx.fill();
				ctx.restore();
			}
	
			move(){
				this.x += this.fwd.x * this.speed;
				this.y += this.fwd.y * this.speed;
			}

			reflectX(){
				this.fwd.x *= -1;
			}

			reflectY(){
				this.fwd.y *= -1;
			}
		}
	</script>
	<script>
		// II. MAIN CODE
		"use strict";
		const ctx = document.querySelector("canvas").getContext("2d");
		const canvasWidth = mycanvas.width;
		const canvasHeight = mycanvas.height;
		let sprites = []; // an array to hold all of our sprites
		let gradient = createLinearGradient(ctx,0,0,0,canvasHeight,[{percent:0,color:"blue"},{percent:.25,color:"green"},{percent:.5,color:"yellow"},{percent:.75,color:"red"},{percent:1,color:"magenta"}])
	

		init();

		function init(){
			sprites = createSprites();
			loop();
		}
		

		function loop(){
			// schedule a call to loop() in 1/60th of a second
			requestAnimationFrame(loop);
	
			// draw background
			ctx.save();
			ctx.fillStyle = gradient;
			ctx.fillRect(0,0,canvasWidth,canvasHeight);
			ctx.restore();
	
			// loop through sprites, move & draw!
			ctx.save();
			for (let s of sprites){
				// move sprites
				s.move();

				// check sides and bounce
				if (s.x <= s.span/2 || s.x >= canvasWidth-s.span/2){
					s.reflectX();
					s.move();
				}
				if (s.y <= s.span/2 || s.y >= canvasHeight-s.span/2){
					s.reflectY();
					s.move();
				}
				// draw sprites
				s.draw(ctx);
		
			} // end for
			ctx.restore();
			
			
		} // end loop()
		

		// III. HELPER FUNCTIONS
		function createSprites(num=20){
			// create array to hold all of our sprites
			let sprites = [];
			for(let i=0;i<num;i++){
				// determine random properties and instantiate new RingSprite
				let x = Math.random() * (canvasWidth - 100) + 50;
				let y = Math.random() * (canvasHeight - 100) + 50;
				let span = 15 + Math.random() * 25;
				let fwd = getRandomUnitVector();
				let speed = Math.random() + 2;
				let color = getRandomColor();
				let s = new Sprite(x,y,span,fwd,speed,color);
			
				// add to array
				sprites.push(s);
			} // end for
	
			// return  array
		  return sprites;
	}

	// IV. GENERAL UTILITY FUNCTIONS
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
	
		// V. CANVAS UTILITY FUNCTIONS
		function createLinearGradient(ctx,startX,startY,endX,endY,colorStops){
			let lg = ctx.createLinearGradient(startX,startY,endX,endY);
			for(let stop of colorStops){
				lg.addColorStop(stop.percent,stop.color);
			}
			return lg;
		}
	
	</script>
</body>
</html>
```

## III. Demo & In-class Exercise

- See comments in HTML file above

## IV. Reference

- https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Classes
- https://2ality.com/2015/02/es6-classes-final.html
