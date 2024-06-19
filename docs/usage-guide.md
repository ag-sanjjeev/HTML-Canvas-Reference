# &#9873; Usage Guide

This usage guide will give you basic usage and implementation of `canvas` in web pages. Before proceeding to the `canvas`, Ensure that you have basic knowledge and understanding in `HTML` and `JavaScript`. 

## Steps:
&emsp; &#10004; Create new or Open existing HTML file to get started. <br />
&emsp; &#10004; Add the canvas tag `<canvas></canvas>` inside the body tag. <br />
&emsp; &#10004; Use the DOM reference for the above canvas tags using JavaScript. <br />
&emsp; &#10004; Finally, play with your logic that you can find in next further topic of this reference.


## Demo:

> Create new or Open existing HTML file to get started. and Add the canvas tag as below

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

> Add JavaScript code to the before closing of the body tag or in new script files as below

```js
// Getting access point reference for canvas tag
let canvas = document.getElementById('canvas');

// Getting window inner height and width
let windowHeight = window.innerHeight;
let windowWidth = window.innerWidth;

// Styling canvas
canvas.style.background = '#b1b1b1';
canvas.height = windowHeight;
canvas.width = windowWidth;

// Drawing Rectangle
let context = canvas.getContext('2d');
context.fillRect(20, 30, 200, 100);
```

**&emsp; &#10004; Once done, You can run this HTML file in your web browser to see the canvas.**


---

[&#10094; Previous Topic](./introduction.md)&emsp;[Next Topic &#10095;](./styling-canvas.md)

[&#8962; Goto Home Page](../README.md)