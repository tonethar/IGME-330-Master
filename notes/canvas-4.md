# Canvas IV - Gradients & Bezier Curves

## I. Overview

- Here we will review the canvas capabilities covered in [HW-SG-2.md](./HW-SG-2.md)

## II. SG-2

1) Setting some properties of lines (other than the `ctx.strokeStyle` and `ctx.lineWidth`) - we actually already talked about some of this in [canvas-2.md](./canvas-2.md):
    - [`ctx.lineCap`](https://developer.mozilla.org/en-US/docs/Web/API/CanvasRenderingContext2D/lineCap) is the shape used to draw the end points of lines
    - [`ctx.lineJoin`](https://developer.mozilla.org/en-US/docs/Web/API/CanvasRenderingContext2D/lineJoin) is the shape used to join two line segments where they meet
    - [`ctx.setLineDash(segments)`](https://developer.mozilla.org/en-US/docs/Web/API/CanvasRenderingContext2D/setLineDash) - sets the line dash pattern used when stroking lines
    - [`ctx.lineDashOffset`](https://developer.mozilla.org/en-US/docs/Web/API/CanvasRenderingContext2D/lineDashOffset) - this wasn't in SG-2 - it adjusts the "phase" i.e. starting point - of a dash pattern 

2) Bezier curves:
    - [`ctx.quadraticCurveTo(ctrlX, ctrlY, endX, endY)`](https://developer.mozilla.org/en-US/docs/Web/API/CanvasRenderingContext2D/quadraticCurveTo) draws bezier curves with 1 control point
    - [`ctx.bezierCurveTo(ctrlX, ctrlY, ctrlXa, ctrlYa, endX, endY)`](https://developer.mozilla.org/en-US/docs/Web/API/CanvasRenderingContext2D/bezierCurveTo) draws cubic bezier curves with 2 control points
    - See the working canvas curve demos - we'll look at these together:
      - [quadratic-bezier-curves-playground.html](http://igm.rit.edu/~acjvks/courses/shared/330/sg-2/bezier-curve-playgrounds/quadratic-bezier-curves-playground.html)
      - [cubic-bezier-curves-playground.html](http://igm.rit.edu/~acjvks/courses/shared/330/sg-2/bezier-curve-playgrounds/cubic-bezier-curves-playground.html)
      - [animated-curves-playground.html](http://igm.rit.edu/~acjvks/courses/shared/330/sg-2/bezier-curve-playgrounds/animated-curves-playground.html)
      - [bezier-curves-tool-2.html](http://igm.rit.edu/~acjvks/courses/shared/330/sg-2/bezier-curves-tool-2.html)
    
3) It turns out we can *fill* or *stroke* a path with solid colors, gradients, and patterns. It's just a matter of what we set our `ctx.fillStyle` to:
    - **solid colors** we have been doing all along, and we specify these like this --> `ctx.fillStyle="red"`, `ctx.fillStyle="rgb(255,0,0)"`, `ctx.fillStyle="#FF0000"`,`ctx.fillStyle="#F00"`, `ctx.fillStyle="#FF0000"`, `ctx.fillStyle="hsl(0, 100%, 50%)"` etc
    - **patterns** as fills are created with `ctx.createPattern(image, repetition)` - you can see a working example in the *apple-canvas-text-examples* folder from SG-2
    - a **gradient** specifies a starting color, an ending color, and an area over which color changes. A single gradient can encompass more than one color change
      - linear gradient - https://developer.mozilla.org/en-US/docs/Web/API/CanvasRenderingContext2D/createLinearGradient
      - radial gradient - https://developer.mozilla.org/en-US/docs/Web/API/CanvasRenderingContext2D/createRadialGradient
      - see demo code below - let's work on this this together in-class:
        - how can we get a gradient flowing from left to right? Right to left? Top to Bottom? Diagonally?
        - can you animate a gradient? Yes! You can see a working example in the *apple-canvas-text-examples* folder from SG-2

## III. Demo Code

**linear-gradient.html**

```html
<!DOCTYPE html>
<html lang="en">
<head>
	<meta charset="utf-8" />
	<title>Linear Gradient</title>
</head>
<body>
<canvas width="640" height="480"></canvas>
<script>
	let ctx = document.querySelector("canvas").getContext("2d");
	let grad = ctx.createLinearGradient(100, 0, 300, 0);
	grad.addColorStop(0, 'red');
	grad.addColorStop(1 / 6, 'orange');
	grad.addColorStop(2 / 6, 'yellow');
	grad.addColorStop(3 / 6, 'green')
	grad.addColorStop(4 / 6, 'aqua');
	grad.addColorStop(5 / 6, 'blue');
	grad.addColorStop(1, 'purple');
	
	ctx.fillStyle = grad;
	ctx.fillRect(0,0,640,480);

/*
	ctx.strokeStyle = "white";
	ctx.lineWidth = 5;
	ctx.beginPath();
	ctx.rect(100, 50, 200,50);
	ctx.closePath();
	ctx.stroke();
	ctx.fill();
*/
</script>
</body>
</html>
```

**radial-gradient.html**

```html
<!DOCTYPE html>
<html lang="en">
<head>
	<meta charset="utf-8" />
	<title>Radial Gradient</title>
</head>
<body>
<canvas width="640" height="480"></canvas>
<script>
	let ctx = document.querySelector("canvas").getContext("2d");
	let grad = ctx.createRadialGradient(150,150, 20, 150, 150, 125);
	grad.addColorStop(0, 'red');
	grad.addColorStop(1 / 6, 'orange');
	grad.addColorStop(2 / 6, 'yellow');
	grad.addColorStop(3 / 6, 'green')
	grad.addColorStop(4 / 6, 'aqua');
	grad.addColorStop(5 / 6, 'blue');
	grad.addColorStop(1, 'purple');
	
	ctx.fillStyle = grad;
	ctx.fillRect(0,0,640,480);
	
// 	ctx.beginPath();
// 	ctx.arc(150,150,125,0,Math.PI*2,false);
// 	ctx.closePath();
// 	ctx.fill();
</script>
</body>
</html>
```

## IV. Videos

- [Canvas - Gradients (11:45)](https://video.rit.edu/Watch/s8FSy64T)
- [Canvas - Animating Curves (11:07)](https://video.rit.edu/Watch/Ay94Cpo7)



<hr><hr>

**[Previous Chapter <- Canvas Part III](canvas-3.md)**

**[Next Chapter -> Canvas Part V](canvas-5.md)**
