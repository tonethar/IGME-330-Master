# Simplex Noise 1

## I. Demo Code

**simplex-noise-1.html**

```html
<!DOCTYPE html>
<html lang="en">
<head>
	<meta charset="utf-8" />
	<title>Open Simplex Noise 1</title>
	<style>canvas{ border: 1px solid black; }</style>
	<script src="https://cdnjs.cloudflare.com/ajax/libs/simplex-noise/2.4.0/simplex-noise.js" integrity="sha256-u8njNpzE/7fzKRST7Eu38nECKwFREeLMkipUauqgPpY=" crossorigin="anonymous"></script></head>
	<script>
	"use strict";
	const canvasWidth = 400, canvasHeight = 300;
	let ctx;
	let x = 0;
	const fps = 12;
	
	const simplex = new SimplexNoise(); 
	let t = 0; // "time" value that we pass to the Simplex function
	
	window.onload = init;

	function init(){
		ctx = canvas.getContext("2d");
		canvas.width = canvasWidth;
		canvas.height = canvasHeight;
		ctx.fillRect(0,0,canvasWidth,canvasHeight);
		loop();
	}
	
	function loop(){
		setTimeout(loop,1000/fps);
		x+=10;
		let y=0
		
		// I. fade effect
		ctx.save();
		ctx.fillStyle = "black";
		ctx.globalAlpha = 1/fps;
		ctx.fillRect(0,0,canvasWidth,canvasHeight);
		ctx.restore();
		
		// II. draw a random red dot, to show how bad random distribution looks
		y = Math.random() * canvasHeight; 
		drawCircle(ctx,x,y,2,"red");
		
		// increment time to pass to simplex-noise function
		t += .01;
		
		// III. determine `y` from simple noise values and draw yellow circle
		let noiseValue = simplex.noise2D(t, t); // range is -1 to +1
		console.log(`noiseValue = ${noiseValue}`);
		let percent = (noiseValue + 1) / 2; // normalized to 0-1
		console.log(`percent = ${percent}`);
  	y = percent * canvasHeight;
  	drawCircle(ctx,x,y,4,"yellow");
  	
  	// IV. draw green circles and also change size based in simplex-noise
  	let noiseValue2 = simplex.noise2D(t+1, t+1);
  	let percent2 = (noiseValue2 + 1) / 2; // normalized to 0-1
  	y = percent2 * canvasHeight;
  	drawCircle(ctx,x,y,2 + percent2 * 10,"darkgreen"); // gets bigger as it moves down screen
  	percent2 = 1-percent2;
  	y = percent2 * canvasHeight;
  	drawCircle(ctx,x,y,12 - percent * 10,"lightgreen"); // mirrors other green circle, gets smaller as it moves down screen
  	
  	
	// V. draw purple circle changing both `x` and `y` and radius according to noise values
		let noiseValue3 = simplex.noise2D(t+5, t/2); 
		let percent3 = (noiseValue3 + 1) / 2; // normalized to 0-1
		y = percent3 * canvasHeight;
		drawCircle(ctx,percent3 * canvasWidth,y,percent2 * 50,"purple"); // gets bigger as it moves down screen
  	
  	
  	// wrap to left side of screen if `x` gets too big
		if (x >= canvasWidth) x=0;
	}


	// helpers
	function drawCircle(ctx,x,y,radius,color){
		ctx.save();
		ctx.fillStyle = color;
		ctx.beginPath();
		ctx.arc(x,y,radius,0,Math.PI * 2);
		ctx.closePath();
		ctx.fill();
		ctx.restore();
	}

	</script>
</head>
<body>
<canvas id="canvas"></canvas>
<ul>
	<li><a href="http://webstaff.itn.liu.se/~stegu/simplexnoise/simplexnoise.pdf">Simplex noise demystified (PDF)</a></li>
	<li><a href="https://github.com/jwagner/simplex-noise.js">Github - simplex-noise.js</a></li>
	<li><a href="https://cdnjs.com/libraries/simplex-noise">cdnjs.com/libraries/simplex-noise</a></li>
</ul>

</body>
</html>
```
