# &#9873; Dot Matrix Grid:

This will give you basic idea about implementation of dot matrix grid in HTML canvas

## Steps involved:

- This can be drawn by two levels.
- First, drawing a dot by `moveTo` and `lineTo` method.
- Finally, drawing this dot repeatedly by row and column.
- `cellSize` defines gap between any other two grid points.

```js
// drawing in column
for (var y = 0; y < this.#height; y += this.cellSize) {
	// drawing in row
	for (var x = 0; x < this.#width; x += this.cellSize) {

		// Calling drawLine method
		this.#drawLine(x, y);					
	}
}
``` 

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
// Global scope variable
let canvas;
let ctx;
let drawing1;

// Reference for animation frame
let animationFrameReference;

// Window load event
window.onload = function () {

	// Get access to HTML canvas tag
	canvas = document.getElementById('canvas');

	// Getting special method context for 2d option
	ctx = canvas.getContext('2d');

	// Applying background color to canvas
	canvas.style.backgroundColor = 'black';

	// Setting width and height to canvas
	canvas.width = window.innerWidth;
	canvas.height = window.innerHeight - 5;

	// Creating DrawField class object
	drawing1 = new DrawField(ctx, canvas.width, canvas.height);
	drawing1.animate();
};

// Window resize event
window.addEventListener('resize', function () {

	// Previous animation to be cancel out
	cancelAnimationFrame(animationFrameReference);

	// accessing from global scope
	canvas.width = window.innerWidth;
	canvas.height = window.innerHeight - 5;	

	// Re Creating DrawField class object when window resized
	drawing1 = new DrawField(ctx, canvas.width, canvas.height);
	drawing1.animate();
});

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

		// Creating animation frame interval for uniform animation in all kind of machine without lag
		// interval of 60 frames per 1000 ms
		this.interval = 1000/30;

		// setting last animation time stamp
		this.lastTimeStamp = 0;

		// setting initial timer
		this.timer = 0;

		// dot matrix cell size
		this.cellSize = 10;

		// dot matrix pixel size
		this.pixelSize = 2;

		console.log('DrawField started...');	
	}

	// private draw method
	#drawLine (x, y) {		

		// beginning the drawing path
		this.#ctx.beginPath();

		// Setting stroke color for drawing
		this.#ctx.strokeStyle = 'white';

		// Setting stroke width
		this.#ctx.lineWidth = 1;

		// Moving to starting point for drawing
		this.#ctx.moveTo(x, y);

		// Drawing to the given length
		this.#ctx.lineTo(x + this.pixelSize, y + this.pixelSize);

		// Drawing into the canvas using stroke method
		this.#ctx.stroke();

		// Closing the drawing path
		this.#ctx.closePath();
	}

	// public animate method with time stamp argument
	animate (timeStamp=0) {

		// calculating delta time
		const deltaTime = timeStamp - this.lastTimeStamp;

		// setting current time stamp for next animation frame
		this.lastTimeStamp = timeStamp;		

		// drawing when only timer is greater than the interval otherwise idle until timer gets reach
		if (this.timer > this.interval) {
			// Clearing previous animation frame
			this.#ctx.clearRect(0, 0, this.#width, this.#height);

			// dot matrix by cell size and pixel size
			// drawing in column
			for (var y = 0; y < this.#height; y += this.cellSize) {
				// drawing in row
				for (var x = 0; x < this.#width; x += this.cellSize) {

					// Calling drawLine method
					this.#drawLine(x, y);					
				}
			}


			this.timer = 0;					
		
		} else {
			this.timer += deltaTime;
		}

		// Calling infinite animation loop and default time stamp argument passed
		animationFrameReference = requestAnimationFrame(this.animate.bind(this));

	}

}
```

---

[&#10094; Previous Topic](./delta-time.md)&emsp;[Next Topic &#10095;](./dot-matrix-grid.md)

[&#8962; Goto Home Page](../README.md)