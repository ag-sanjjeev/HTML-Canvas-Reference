# &#9873; Delta Time:

This will give you basic idea about implementation of calculating and implementing delta time concept in HTML canvas

## Steps involved:

- This is important concept in canvas animation.
- To animate without any performance lag on different devices, Then delta time concepts should be used.
- For one second or 1000 milli-second, We can set frames per second to be played.
- This will avoid any performance lag one different devices, due to limiting and setting Frames Per Second.
- This can be done by utilizing default argument passed in `requestAnimationFrame(callback)` method.
- Calculating delta time `const deltaTime = timeStamp - lastTimeStamp;`
- Setting 30 FPS `let interval = 1000/30;`. Which denotes 1000 milli-seconds divided by 30 Frames.
- Plays animation once the interval reached by comparing current timestamp. otherwise increments the timer.
- For the low end specification devices, the deltaTime is greater than high end devices.
- This drop some animation frames with given FPS range based on the performance. 

```js
// drawing when only timer is greater than the interval otherwise idle until timer gets reach
if (timer > interval) {
 ...
 ...
} else {
	timer += deltaTime;
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
		this.interval = 1000/30;

		// setting last animation time stamp
		this.lastTimeStamp = 0;

		// setting initial timer
		this.timer = 0;

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

			// Calling draw method
			this.#draw();	

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

[&#10094; Previous Topic](./mouse-movement-animation.md)&emsp;[Next Topic &#10095;](./delta-time.md)

[&#8962; Goto Home Page](../README.md)