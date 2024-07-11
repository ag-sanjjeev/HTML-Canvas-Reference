# &#9873; Flower Animation:

This will give you basic idea about implementation of drawing flower animation out of circles in HTML canvas

## Steps involved:

- This can be drawn by three levels.
- First, calculate starting point of drawing.
- Second, calculate radius of circle before start drawing.
- Third, draw circle using `arc` method with co-ordinates and dimensions.
- Fourth, update the co-ordinates and dimensions after each circle drawn.
- Continuously draw this circles until the given number of circles to draw.


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
		this.interval = 1000/60;

		// setting last animation time stamp
		this.lastTimeStamp = 0;

		// setting initial timer
		this.timer = 0;

		// circle size
		this.circleSize = 5;

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

		// interation number
		this.number = 0;

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

	// private draw circle method
	#drawCircle() {
		// change these values to change animation flower pattern
		let noOfCircles = 5000;
		let gap = 30;
		let sizeFactor = 5.75;
		let numberIncremental = 0.01;
		let circleSizeIncremental = 0.1;

		let angle = this.number * noOfCircles;
		this.radius = sizeFactor * Math.sqrt(this.number); 
		let scale = this.radius * gap;
		this.x = scale * Math.sin(angle) + (this.#width/2);
		this.y = scale * Math.cos(angle) + (this.#height/2);
		let startAngle = 0;
		let endAngle = Math.PI * 2;

		this.#ctx.fillStyle = this.gradient;
		this.#ctx.strokeStyle = 'white';//this.gradient;
		this.#ctx.beginPath();
		this.#ctx.arc(this.x, this.y, this.circleSize, startAngle, endAngle);
		this.#ctx.closePath();
		this.#ctx.fill();
		this.#ctx.stroke();	

		this.number += numberIncremental;
		this.circleSize += circleSizeIncremental;		

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
			// this.#ctx.clearRect(0, 0, this.#width, this.#height);

			// draw circle
			this.#drawCircle();

			this.timer = 0;					
		
		} else {
			this.timer += deltaTime;
		}

		// When the drawing reaches window width and height then animation cancels 
		if (this.x > this.#width && this.y > this.#height) {
			// Previous animation to be cancel out
			cancelAnimationFrame(animationFrameReference);
		} else {
			// Calling infinite animation loop and default time stamp argument passed
			animationFrameReference = requestAnimationFrame(this.animate.bind(this));
		}

	}

}
```

---

[&#10094; Previous Topic](./gradient-animation.md)&emsp;[Next Topic &#10095;](./flower-animation.md)

[&#8962; Goto Home Page](../README.md)