# &#9873; Responsive Animation:

This will give you basic idea about Responsive Animation in HTML canvas

## Steps involved:

- For resizing browser window, the fixed style of canvas will be the same.
- To Update dimensions of canvas size based on browser window resize event.
- When re-setting size of canvas that will affect the created frame and or animation.
- To avoid that canvas glitches, use this `cancelAnimationFrame(animationFrameReference)` method.
- Which will stops the previous frame of animation.
- Once everything is re-setted then again call `requestAnimationFrame(callback)` method. 


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

		console.log('DrawField started...');	
	}

	// private draw method
	#draw (x, y, length) {		

		// beginning the drawing path
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
		animationFrameReference = requestAnimationFrame(this.animate.bind(this));
	}

}
```

---

[&#10094; Previous Topic](./moving-lines.md)&emsp;[Next Topic &#10095;](./responsive-animation.md)

[&#8962; Goto Home Page](../README.md)