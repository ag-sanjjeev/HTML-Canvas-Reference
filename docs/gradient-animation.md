# &#9873; Gradient Animation:

This will give you basic idea about implementation of gradient animation in HTML canvas

## Steps involved:

- This can be drawn by three levels.
- First, create dot gradient grid drawing technique.
- Second, Get mouse co-ordinates using the `mousemove` event.
- Finally, add line draw technique with some mouse hover effect as below mentioned.
- This will make black color on mouse hover position with some radius of distance.

```js
// applying mouse hover effect
let posX = x;
let posY = y;
let dx = mouseMove.x - x;
let dy = mouseMove.y - y;
let distance = Math.sqrt(dx * dx + dy * dy);

this.pixelSize = distance / 10;

// Drawing to the given length
this.#ctx.lineTo(x + Math.cos(angle)*this.pixelSize, y + Math.sin(angle)*this.pixelSize);
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

		// Creating animation frame interval for uniform animation in all kind of machine without lag
		// interval of 60 frames per 1000 ms
		this.interval = 1000/10;

		// setting last animation time stamp
		this.lastTimeStamp = 0;

		// setting initial timer
		this.timer = 0;

		// dot matrix cell size
		this.cellSize = 15;

		// dot matrix pixel size
		this.pixelSize = 70;

		// line width or stroke width
		this.lineWidth = 1;

		// gradient property
		this.gradient;

		// calling gradient method to add linear gradient colors
		this.#linearGradient();

		// animation properties
		// radius property
		this.radius = 0;

		// change in radius
		this.dr = 0.003;

		console.log('DrawField started...');	
	}

	// private gradient method
	#linearGradient() {
		this.gradient = this.#ctx.createLinearGradient(0, 0, this.#width, this.#height);
		this.gradient.addColorStop('0.1', '#E57373');
		this.gradient.addColorStop('0.2', '#F06292');
		this.gradient.addColorStop('0.3', '#BA68C8');
		this.gradient.addColorStop('0.4', '#5C6BC0');
		this.gradient.addColorStop('0.5', '#42A5F5');
		this.gradient.addColorStop('0.6', '#4CAF50');
		this.gradient.addColorStop('0.7', '#FFEB3B');
		this.gradient.addColorStop('0.8', '#FF9800');
		this.gradient.addColorStop('0.9', '#BDBDBD');
	}

	// private draw method
	#drawLine (x, y, angle) {		

		// beginning the drawing path
		this.#ctx.beginPath();

		// Setting stroke color with new linear gradient color for drawing
		this.#ctx.strokeStyle = this.gradient;

		// Setting stroke width
		this.#ctx.lineWidth = this.lineWidth;

		// Moving to starting point for drawing
		this.#ctx.moveTo(x, y);

		// applying mouse hover effect
		let posX = x;
		let posY = y;
		let dx = mouseMove.x - x;
		let dy = mouseMove.y - y;
		let distance = Math.sqrt(dx * dx + dy * dy);

		this.pixelSize = distance / 10;

		// Drawing to the given length
		this.#ctx.lineTo(x + Math.cos(angle)*this.pixelSize, y + Math.sin(angle)*this.pixelSize);

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

					this.radius += this.dr;

					if (this.radius > 5 || this.radius < -5) {
						this.dr *= -1;
					}

					var angle = (Math.cos(x/2 * 0.01) + Math.sin(y * 0.01)) * this.radius;
					// Calling drawLine method
					this.#drawLine(x, y, angle);
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

[&#10094; Previous Topic](./gradient-grid.md)&emsp;[Next Topic &#10095;](./gradient-animation.md)

[&#8962; Goto Home Page](../README.md)