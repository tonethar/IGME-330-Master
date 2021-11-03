# Canvas 2D Essential Skills #7 - Bezier curves and gradients

## I. Canvas Study Guide #2-  Overview
- You will be review these concepts on your own by completing [Canvas Study Guide #2 (see myCourses dropbox for due date)](https://github.com/tonethar/IGME-330-Master/blob/master/notes/HW-SG-2.md) 
- *Canvas Study Guide #2* ??
  - but when did *Canvas Study Guide #1* happen? 
  - answer:  we did not assign *Canvas Study Guide #1* this semester
- The major concepts that will be covered in this Study Guide:
  - setting caps and joins on lines - `ctx.lineCap`, `ctx.lineJoin`, `ctx.setLineDash()`
  - creating linear and radial gradients - `ctx.createLinearGradient()`, `ctx.createRadialGradient()`, and `ctx.addColorStop()`
  - creating bezier curves - `ctx.quadraticCurveTo()`, `ctx.bezierCurveTo()`

<hr>

## II. Gradient Demo Code

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

<hr>

## III. Reference

- Lines:
  - [`ctx.lineCap`](https://developer.mozilla.org/en-US/docs/Web/API/CanvasRenderingContext2D/lineCap)
  - [`ctx.lineJoin`](https://developer.mozilla.org/en-US/docs/Web/API/CanvasRenderingContext2D/lineJoin)
  - [`ctx.setLineDash()`](https://developer.mozilla.org/en-US/docs/Web/API/CanvasRenderingContext2D/setLineDash)
- Gradients:
  - [`ctx.createLinearGradient()`](https://developer.mozilla.org/en-US/docs/Web/API/CanvasRenderingContext2D/createLinearGradient)
  - [`ctx.createRadialGradient()`](https://developer.mozilla.org/en-US/docs/Web/API/CanvasRenderingContext2D/createRadialGradient)
  - [`ctx.addColorStop()`](https://developer.mozilla.org/en-US/docs/Web/API/CanvasGradient/addColorStop)
- Bezier Curves:
  - [`ctx.quadraticCurveTo()`](https://developer.mozilla.org/en-US/docs/Web/API/CanvasRenderingContext2D/quadraticCurveTo)
  - [`ctx.bezierCurveTo()`](https://developer.mozilla.org/en-US/docs/Web/API/CanvasRenderingContext2D/bezierCurveTo)


<hr><hr>

| <-- Previous Unit | Home | Next Unit -->
| --- | --- | --- 
|  [**#6 - Review & More About Paths**](6-review-and-more-about-paths.md) |  [**IGME-330**](../README.md) | [**#8 - Canvas Transformations**](8-canvas-transformations.md)
