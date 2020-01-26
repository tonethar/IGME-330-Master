# Conway's Game of Life (now in Canvas!)

## I. Overview
- Some info about *Conway's Game of Life* and cellular automata is below: 
  - https://en.wikipedia.org/wiki/Conway%27s_Game_of_Life
  - https://en.wikipedia.org/wiki/Cellular_automaton


Here is a GIF of the Life "Glider Gun" pattern:

![Glider Gun Image](_images/HW-life-gospers-glider-gun.gif)

- Here are the rules to Life:
  - Any live cell with fewer than two live neighbours dies, as if caused by underpopulation.
  - Any live cell with two or three live neighbours lives on to the next generation.
  - Any live cell with more than three live neighbours dies, as if by overpopulation.
  - Any dead cell with exactly three live neighbours becomes a live cell, as if by reproduction.

## II. Completed Version




## III. Start Files

**life-HW-start.html**

```html
<!DOCTYPE html>
<html lang="en">
<head>
	<meta charset="utf-8" />
	<title></title>
	<style>
		body{
			font-family: sans-serif;
		}
		canvas{
			background-color: #0000AD;
		}
	</style>
	<script src="src/lifeworld.js"></script>
	<script src="src/main.js"></script>
</head>
<body>
	<canvas></canvas>
	
	<h2>About</h2>
	<ul>
	<li><a href="http://www.ibiblio.org/lifepatterns/october1970.html"><i>MATHEMATICAL GAMES - The fantastic combinations of John Conway's new solitaire game "life"</i></a> by Martin Gardner</li>
	<li><a href="https://en.wikipedia.org/wiki/Conway%27s_Game_of_Life">Wikipedia entry about Conway's Game of Life</a></li>
	<li><a href="https://en.wikipedia.org/wiki/Oscillator_(cellular_automaton)">https://en.wikipedia.org/wiki/Oscillator_(cellular_automaton)</a></li>
	<li><a href="https://conwaylife.com/forums/viewtopic.php?f=7&t=20">https://conwaylife.com/forums/viewtopic.php?f=7&t=20</a></li>
	</ul>
	
</body>
</html>
```

**main.js**

```js
let canvas, ctx;
const canvasWidth = 600, canvasHeight = 400;
const cellWidth = 10;
const fps = 12;
let lifeworld;

window.onload = init;

function init(){
	canvas = document.querySelector("canvas");
	canvas.width = canvasWidth;
	canvas.height = canvasHeight;
	ctx = canvas.getContext("2d");
	// TODO: init lifeworld
	loop();
}

function loop(){
	setTimeout(loop,1000/fps);
	// TODO: update lifeworld
	drawBackground();
	drawWorld();
}

function drawBackground(){
	ctx.save();
	ctx.fillStyle = "black";
	ctx.globalAlpha = 4/fps;
	ctx.fillRect(0,0,canvasWidth,canvasHeight);
	ctx.restore();
}

function drawWorld(){
	// TODO: implement
}

function drawCell(col,row,dimensions,alive) {
	// TODO: implement
}
```

**lifeworld.js**

```js
// model class Lifeworld
// TODO: Write code
```


## IV. Instructions

1) Go ahead and create all of the above files and then preview them in a web browser. You should see a black 600 x 400 rectangle in the browser window.

2) Add the following to **Lifeworld.js**:

![screenshot](_images/HW-canvas-life-1.jpg)


3) In **main.js**, add the following to `init()`

`lifeworld = new Lifeworld(60,40,.2);`

4) Test the code, and check the console. you should see the 2D array we are using has been created and populated with random 0's and 1's

![screenshot](_images/HW-canvas-life-2.jpg)

5) xxx
