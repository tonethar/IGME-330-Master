# HW - Canvas Helper Functions

## I. Overview


## II. Start File

**canvas-helpers-start.html**
```html
<!DOCTYPE html>
<html lang="en">
<head>
	<meta charset="utf-8" />
	<title>Canvas Helpers Starter</title>
	<style type="text/css">
	canvas{
		border:1px solid gray;
	}
	</style>
</head>
<body>
	<canvas width="640" height="480">
		Get a real browser!
	</canvas>
	<script>
	'use strict';
		
	init();
	
	function init(){
		let ctx = document.querySelector('canvas').getContext('2d');
		// test the drawRectangle() function
		drawRectangle(ctx);
		drawRectangle(ctx,100,100,250,250,"red","yellow",10);
	}
	
	
	function drawRectangle(ctx,x=0,y=0,width=25,height=25,fillStyle="red",strokeStyle="black",lineWidth=0){
		ctx.save();                
		ctx.beginPath();            
		ctx.rect(x,y,width,height);   
		ctx.closePath(); 
		ctx.fillStyle = fillStyle;
		ctx.strokeStyle = strokeStyle;    
		ctx.lineWidth = lineWidth;  
		ctx.fill();              
		ctx.stroke();                            
		ctx.restore();             
	}
	
	function drawCircle(ctx,x=0,y=0,radius=10, fillStyle="red",strokeStyle="black",lineWidth=0,startAngle=0,endAngle=Math.PI*2){
		// you do!
	}
	
	function drawLine(ctx,x1=0,y1=0,x2=100,y2=0,strokeStyle="black",lineWidth=5){
		// you do!
	}
	
	function drawTriangle(ctx,x1=0,y1=0,x2=50,y2=50,x3=-50,y3=50,fillStyle="red",strokeStyle="black",lineWidth=5){
		// you do!
	}
	
	function drawArc(ctx,x1=0,y1=0,x2=300,y2=0,cpX=150,cpY=75,fillStyle="red",strokeStyle="black",lineWidth=5){
		// you do!
	}
	
	</script>
</body>
</html>
```


## III. Example

Here's an example that meets requirements (you can probably come up with something better):
- The head is made with `drawRectangle()`
- The eyes and pupils are made with `drawCircle()`
- The hair is made with `drawLine()` and a `for` loop, with a little `Math.random()` to slightly vary the length of the strands
- The nose is done with 2 `drawLine()` calls
- The mouth is done with `drawArc()`
- The teeth are done with `drawTriangle()` and here we used `ctx.translate()`/`ctx.rotate()`/`ctx.scale()` to make it MUCH easier to position the teeth


