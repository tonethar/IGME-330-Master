# HW - Canvas Paint App

## I. Overview

- Over the next week or so, we're going to build a canvas paint app - it looks like this:

![screenshot](_images/_canvas-paint-app/paint-app-1.jpg)

<hr>

## II. Start Code

- Here's the HTML for your "copy/paste" pleasure!

**canvas-paint.html**

```html
<!DOCTYPE html>
<html lang="en">
	<head>
		<meta charset="utf-8" />
		<title>Canvas Paint App</title>
		<style></style>
    <script></script>
	</head>
<body>
	<canvas id="mainCanvas">
	Get a real browser!
  </canvas>
    
	<section id="controls">
		<label>Tool:
			<select id="chooserTool">
				<option value="pencil" selected>Pencil</option>
				<option value="rectangle">Rectangle</option> 
				<option value="line">Line</option>
				<option value="circle">Circle</option>
    		</select>
    </label>
    	
    <label>Line Width: 
			<select id="chooserLineWidth">
				<option value="0" >0</option>
				<option value="1" selected>1</option>
				<option value="5">5</option>
        <option value="10">10</option>
        
    		</select>
		</label>
		
		<label>Line Color: 
			<select id="chooserStrokeStyle"> 
				<option value="red">Red</option>
				<option value="green" selected>Green</option>
        <option value="blue">Blue</option>
    	</select>
    </label>
        
    	
    	<span><input id="btnClear" type="button" value="Clear"/></span>
    	<span><input id="btnExport" type="button" value="Export"/></span>
    </section>
    
    <section id="info">
    	<p>???</p>
    </section>

		
</body>
</html>

```

<hr>

## III. CSS

- Here's the CSS for your typing pleasure!

![screenshot](_images/_canvas-paint-app/paint-app-2.jpg)

<hr>
