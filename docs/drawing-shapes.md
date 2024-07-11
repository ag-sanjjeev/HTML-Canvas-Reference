# &#9873; Drawing Shapes:

This will give you basic idea about creating shapes like,
- Squares
- Rectangles
- Circles

## Drawing Squares:

> HTML Code:

```xml
<!DOCTYPE html>
<html>
<head>
	<meta charset="utf-8" />
	<meta name="viewport" content="width=device-width, initial-scale=1" />
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

- Squares can be created using `fillRect()` method of context 
- `context.fillRect(xPosition, yPosition, width, height);`
- Where, Width and Height to be same for squares.

```js
// Getting access point reference for canvas tag
let canvas = document.getElementById('canvas');

// Drawing Rectangle
let context = canvas.getContext('2d');

// Applying color to square
context.fillStyle = "blue";

// Drawing Square
context.fillRect(50, 150, 100, 100);
```

## Drawing Rectangles:

> JavaScript Code:

- Rectangles can be created using `fillRect()` method of context 
- `context.fillRect(xPosition, yPosition, width, height);`

```js
// Getting access point reference for canvas tag
let canvas = document.getElementById('canvas');

// Drawing Rectangle
let context = canvas.getContext('2d');

// Applying color to square
context.fillStyle = "blue";

// Drawing Square
context.fillRect(200, 350, 200, 100);
```

## Drawing Circles:

> JavaScript Code:

- Circle can be created using `arc()` and `stroke()` method of context 
- This will start with `beginPath()` and end with `closePath()` method
- Where, the arc method accept X and Y co-ordinates, starting angle / Radius of the circle, Ending angle and drawing direction by either clock-wise or anti clock-wise.

```js
// Getting access point reference for canvas tag
let canvas = document.getElementById('canvas');

// Drawing Circle
let context = canvas.getContext('2d');

// Begin Path
context.beginPath();

// Applying border / stroke color
context.strokeStyle = 'green';

// Applying border line / stroke width
context.lineWidth = '3';

// Arc method to set values to the circle
context.arc(50, 300, 0, Math.PI * 2, false);

// stroke method to draw into the canvas
context.stroke();

// after completing the drawing need to close the path
context.closePath();
```

---

[&#10094; Previous Topic](./styling-canvas.md)&emsp;[Next Topic &#10095;](./drawing-lines.md)

[&#8962; Goto Home Page](../README.md)