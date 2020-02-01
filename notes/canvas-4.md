# IV - Canvas: Gradients & Bezier Curves

## I. Overview

- Here we will review canvas capabilities covered in [HW-SG-2.md](./HW-SG-2.md)

## II. SG-2

1) line caps, line joins, line dashes (we actually already talked about this in [canvas-2.md](./canvas-2.md))

2) It turns out we can *fill* or *stroke* a path with solid colors, gradients, and patterns. It's just a matter of what we set our `ctx.fillStyle` to:
    - *solid colors* we have been doing all along, and we specify these like this --> `ctx.fillStyle="red"`, `ctx.fillStyle="rgb(255,0,0)"`, `ctx.fillStyle="#FF0000"`,`ctx.fillStyle="#F00"`, `ctx.fillStyle="#FF0000"`, `ctx.fillStyle="hsl(0, 100%, 50%)"` etc
    - *patterns* as fills are created with `ctx.createPattern(image, repetition)` - you can see a working example in the *apple-canvas-text-examples* folder from SG-2
    - a **gradient** specifies a starting color, an ending color, and an area over which color changes. A single gradient can encompass more than one color change
    - linear gradient - https://developer.mozilla.org/en-US/docs/Web/API/CanvasRenderingContext2D/createLinearGradient
    - radial gradient - https://developer.mozilla.org/en-US/docs/Web/API/CanvasRenderingContext2D/createRadialGradient
    - see demo code below:
      - how can we get a gradient flowing from left to right? Right to left? Top to Bottom? Diagonally?
      - can you animate a gradient? Yes! You can see a working example in the *apple-canvas-text-examples* folder from SG-2

3) bezier curves:
  - `ctx.quadraticCurveTo(ctrlX, ctrlY, endX, endY)` draws bezier curves with 1 control point
  - `ctx.bezierCurveTo(ctrlX, ctrlY, ctrlXa, ctrlYa, endX, endY)` draws cubic bezier curves with 2 control points
  - curve building demos
  - animating curves

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



<hr><hr>

**[Previous Chapter <- Canvas Part III](canvas-3.md)**
