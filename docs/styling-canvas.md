# &#9873; Styling Canvas:

This will give you idea about basic styling of canvas container. Like,
- Setting Width
- Setting Height
- Applying Background Color

## Accessing Canvas Tag:

```js
// Getting access point reference for canvas tag
let canvas = document.getElementById('canvas');
```

## Setting Width:

```js
let width = 100;
canvas.width = width;
```

## Setting Height:

```js
let height = 100;
canvas.height = height;
```


## Applying Background Color:

```js
canvas.style.background = '#b1b1b1';
```

## Demo:

> HTML Code 

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

> JavaScript Code

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

```

---

[&#10094; Previous Topic](./usage-guide.md)&emsp;[Next Topic &#10095;](./drawing-shapes.md)

[&#8962; Goto Home Page](../README.md)