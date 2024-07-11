# &#9873; Moving Lines:

This will give you basic idea about move the lines created in HTML canvas

## Steps involved:

- Moving lines can be possible by clearing old frame and drawing new frame on certain time interval.
- For clearing old frame by using this `clearRect(0, 0, canvaswidth, canvasheight)`
- Re-drawing the frame by re-calling the drawing logics.
- To request this continuesly using `requestAnimationFrame(callback)`.
- For effective use of re-calling, avoid setInterval or any other loops.


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
	drawing1.animate();
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
		this.x = 0;
		this.y = 0;

		console.log('DrawField started...');	
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

	// public animate method
	animate () {

		// Clearing previous animation frame
		this.#ctx.clearRect(0, 0, this.#width, this.#height);

		// incrementing co-ordinates
		this.x += 0.5;
		this.y += 1.5;

		// Calling draw method
		this.#draw(this.x, this.y, 300);	

		// Calling infinite animation loop
		requestAnimationFrame(this.animate.bind(this));
	}

}
```

---

[&#10094; Previous Topic](./drawing-lines.md)&emsp;[Next Topic &#10095;](./moving-lines.md)

[&#8962; Goto Home Page](../README.md)