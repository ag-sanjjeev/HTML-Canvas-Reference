# &#9873; Drawing Lines:

This will give you basic idea about creating lines in HTML canvas

## Steps involved:

- Drawing lines should starts with `beginPath()` method.
- It gives ability to draw lines with help of two methods.
- First, we need to set starting point of line using this `moveTo(x, y)` method.
- Second, Stroked by `stroke()` method.
- Third, we need to set ending point of line using this `lineTo(x + length, y + length)` method.
- Both accept x and y co-ordinates.
- Finally, We should close the drawing path by `closePath()` method.


> HTML Code:

```xml
<!DOCTYPE html>
<html>
<head>
	<meta charset="utf-8" />
	<meta name="viewport" content="width=device-width, initial-scale=1" />
	<link rel="stylesheet" type="text/css" href="./main.css" media="all" />
	<title>Canvas Playground</title>
</head>
<body>

	<!-- Canvas -->
	<canvas id="canvas"></canvas>
	<!-- ./ Canvas -->

	<!-- Main Script -->
	<script type="text/javascript" src="./main.js"></script>
	<!-- ./ Main Script -->
</body>
</html>
```

> JavaScript Code:

```js
// Window load event
window.onload = function () {

	// Get access to HTML canvas tag
	let canvas = document.getElementById('canvas');

	// Getting special method context for 2d option
	let ctx = canvas.getContext('2d');

	// Applying background color to canvas
	canvas.style.backgroundColor = 'black';

	// Setting width and height to canvas
	canvas.width = window.innerWidth;
	canvas.height = window.innerHeight - 5;

	// Creating DrawField class object
	const drawing1 = new DrawField(ctx, canvas.width, canvas.height);

};

// Class DrawField

class DrawField {

	// Creating private class properties
	#ctx;
	#width;
	#height;

	// class constructor
	constructor (ctx, width, height) {

		// Assigning property values
		this.#ctx = ctx;
		this.#width = width;
		this.#height = height;

		console.log('DrawField started...');

		// Calling draw method
		this.#draw(150, 500, 300);	
	}

	// private draw method
	#draw (x, y, length) {		

		// begining the drawing path
		this.#ctx.beginPath();

		// Setting stroke color for drawing
		this.#ctx.strokeStyle = 'white';

		// Moving to starting point for drawing
		this.#ctx.moveTo(x, y);

		// Drawing to the given length
		this.#ctx.lineTo(x + length, y + length);

		// Drawing into the canvas using stroke method
		this.#ctx.stroke();

		// Closing the drawing path
		this.#ctx.closePath();
	}

}
```

---

[&#10094; Previous Topic](./drawing-shapes.md)&emsp;[Next Topic &#10095;](./drawing-lines.md)

[&#8962; Goto Home Page](../README.md)