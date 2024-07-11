# &#9873; Mouse Movement Animation:

This will give you basic idea about Mouse Movement Animation to draw line based on mouse click and mouse co-ordinate positions in HTML canvas

## Steps involved:

- This can be done with help of two mouse events.
- For setting starting point of line can be done with `click` event.
- For updating ending point of line can be done with `mousemove` event.


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

// mouse clicked co-ordinate
let mouseClicked = {
	x: 0,
	y: 0
};

// mouse movement co-ordinate 
let mouseMove = {
	x: 0,
	y: 0
};

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

// adding mouse click event listener
window.addEventListener('click', function(e) {
	mouseClicked.x = e.x;
	mouseClicked.y = e.y; 
});

// adding mouse over event listener
window.addEventListener('mousemove', function(e) {
	mouseMove.x = e.x;
	mouseMove.y = e.y;
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

		console.log('DrawField started...');	
	}

	// private draw method
	#draw () {		

		// beginning the drawing path
		this.#ctx.beginPath();

		// Setting stroke color for drawing
		this.#ctx.strokeStyle = 'white';

		// Setting stroke width
		this.#ctx.lineWidth = 5;

		// Moving to starting point for drawing
		this.#ctx.moveTo(mouseClicked.x, mouseClicked.y);

		// Drawing to the given length
		this.#ctx.lineTo(mouseMove.x, mouseMove.y);

		// Drawing into the canvas using stroke method
		this.#ctx.stroke();

		// Closing the drawing path
		this.#ctx.closePath();
	}

	// public animate method
	animate () {

		// Clearing previous animation frame
		this.#ctx.clearRect(0, 0, this.#width, this.#height);

		// Calling draw method
		this.#draw();	

		// Calling infinite animation loop
		animationFrameReference = requestAnimationFrame(this.animate.bind(this));
	}

}
```

---

[&#10094; Previous Topic](./responsive-animation.md)&emsp;[Next Topic &#10095;](./mouse-movement-animation.md)

[&#8962; Goto Home Page](../README.md)