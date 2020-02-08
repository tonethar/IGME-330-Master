# Canvas VI - Canvas Sprites

## I. Overview
- So there's no new Canvas API concepts below, but there's a lot of potentially helpful example code below - see comments in source file:
  - #1 - ES6 Classes with `draw()` and `move()` methods
  - #2 - `Object.assign()`
  - #3 - ES6 Class inheritance
  - #4 - A handy `createLinearGradient()` helper function
  - #5 - `array.concat()` and the ES6 spread operator
  - #6 - The CSS attribute selector
  - #7 - Form values are returned as strings! Don't forget to convert them to a number if that's what you need!
  - #8 - ES6 class reference used as an argument to a function
  - #9 - Standard "move and check world boundaries" code
  - #10 - How to set up the HTML for radio buttons

## II. Screenshot

![Animated GIF](./_images/canvas-animated-sprites-example.gif)


## III. Code

**sprites-and-radio-buttons.html**

```html
<!DOCTYPE html>
<html lang="en">
<head>
	<meta charset="utf-8" />
	<title>Sprites and Radio Buttons</title>
	<script>
	// #1 CLASS CODE
	// we've put these Sprite classes in a separate <script> tag from the rest of the code, but this code should really be in another file
	class Sprite{
		constructor(x=0,y=0,span=10,fwd={x:1,y:0},speed=0,color="black"){
			this.x = x;
			this.y = y;
			this.span = span;
			this.fwd = fwd;
			this.speed = speed;
			this.color = color;
			
			// #2 - Here's a cooler idiom to accomplish the same property assignment as above, 
			// with one line of code!
			// https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Object/assign
			//Object.assign(this,{x,y,span,fwd,speed,color});
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
	
	// #3 - Inheritance example. Note that `RingSprite` is using all the methods of Sprite 
	// except for `draw()`, which it is replacing (overriding) with its own implementation
	class RingSprite extends Sprite{
		draw(ctx){
			ctx.save();
			ctx.translate(this.x,this.y);
			ctx.beginPath();
			ctx.arc(0,0,this.span/2,0,Math.PI * 2,false);
			ctx.arc(0,0,this.span/4,0,Math.PI * 2,true);
			ctx.closePath();
			ctx.fillStyle = this.color;
			ctx.fill();
			ctx.restore();
		}
		
	}
	</script>
	
	<script>
		// #4 - UTILITY CODE
		// Here's more code that should probably be in a separate file
		// Maybe in abcLIB.js (if you are working on Project 1) or utils.js (if you are working on Project 2)
		// Also check out `createLinearGradient()`, it's new and handy

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

		function createLinearGradient(ctx,startX,startY,endX,endY,colorStops){
			let lg = ctx.createLinearGradient(startX,startY,endX,endY);
			for(let stop of colorStops){
				lg.addColorStop(stop.percent,stop.color);
			}
			return lg;
		}
	</script>
	
	<script>
	// MAIN code
	let ctx,canvas
	let gradient;
	let sprites = [];
	const canvasWidth = 600, canvasHeight = 400;
	
	window.onload = init;
	
	function init(){
		canvas = document.querySelector('canvas');
		canvas.width = canvasWidth;
		canvas.height = canvasHeight;
		ctx = canvas.getContext("2d");
		gradient = createLinearGradient(ctx,0,0,0,canvasHeight,[{percent:0,color:"blue"},{percent:.25,color:"green"},{percent:.5,color:"yellow"},{percent:.75,color:"red"},{percent:1,color:"magenta"}])
		
		// #5 - make 2 different kinds of sprites and use `array.concat()` to append them to 
		// the `sprites` array
		sprites = sprites.concat(sprites,createSprites(10,Sprite));
		sprites = sprites.concat(sprites,createSprites(20,RingSprite));

		// But cool kids use the spread operator instead of array.concat() 
		// https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/Spread_syntax
		// sprites =  [...createSprites(10,Sprite), ...createSprites(20,RingSprite)];
		
		// hook up event handlers
		setupUI();
		
		// kick off animation loop
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
		
		// move and draw sprites
		moveAndDrawSprites(ctx);
	}
	
	function setupUI(){
		// #6 - note the attribute selector we are using here
		let radioButtons = document.querySelectorAll("input[type=radio][name=speed]");
		for (let r of radioButtons){
			r.onchange = function(e){
				// #7 - form values are returned as Strings, so we have to convert them to a Number
				let speed = Number(e.target.value);
				for (let s of sprites){
					s.speed = Math.random() + speed;
				}
			}
		}
	}
	
	// #8 - Note that here we take a Class as a function to an argument
	// That means that in JS, classes (as well as functions) are "first class" types like
	// String, Number etc in that they can be passed as arguments to functions, and also
	// returned from functions.
	function createSprites(num=5,classRef=Sprite){
		// create array to hold all of our sprites
		let array = [];
		
		// make some sprites
		for(let i=0;i<num;i++){
			// determine random properties and instantiate new sprite
			let x = Math.random() * (canvasWidth - 100) + 50;
			let y = Math.random() * (canvasHeight - 100) + 50;
			let span = 15 + Math.random() * 25;
			let fwd = getRandomUnitVector();
			let speed = Math.random() + 2;
			let color = getRandomColor();
			let s = new classRef(x,y,span,fwd,speed,color);
	
			// add to end of array
			array.push(s);
		} // end for
		
		return array;
	}
	
	// #9 - standard "move and check world boundaries" code
	function moveAndDrawSprites(ctx){
		ctx.save();
		for (let s of sprites){
			// move sprite
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
				
			// draw sprite
			s.draw(ctx);

		} // end for
		ctx.restore();
	}
	
	</script>
	
</head>
<body>
<canvas></canvas>
<!-- 
#10 - note that for radio buttons to be in a group, where only one is selected at a time,
they need to all have the same value for the `name` attribute. 
Also note that we have given each of them individually their own `id`, but we're not really
using that value
 -->
<div>
  <input type="radio" id="crawlRadio" name="speed" value="0.1"> <label for="crawlRadio">Crawl</label>
  <input type="radio" id="slowRadio" name="speed" value="1"> <label for="slowRadio">Slow</label>
  <input type="radio" id="mediumRadio" name="speed" value="2" checked> <label for="mediumRadio">Medium</label>
  <input type="radio" id="fastRadio" name="speed" value="3"> <label for="fastRadio">Fast</label>
</div>
</body>
</html>
```

**[Previous Chapter <- Canvas Part V](canvas-5.md)**
