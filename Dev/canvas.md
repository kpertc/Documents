HTML Canvas

``` js
canvasElement.width = 200;
canvasElement.width = window.innerWidth;

const ctx = canvasElement?.getContext("2d");
```

Draw Rectangle
``` js
// Fill
ctx.fillStyle = "red"; // fill with red
ctx.fillRect(0, 0, 100, 100); // x, y, width, height
ctx.st

// Stroke
ctx.lineWidth = 1;
ctx.strokeStyle = "green"; // stroke with black
ctx.strokeRect(200, 200, 100, 100);

// Clear React
ctx.clearRect(10, 10, 50, 50); // clear rect area
```

Draw Text
``` js
ctx.font = "30px Arial"; // set size and font
ctx.fillText("Hello", 100, 200); // fill text
ctx.strokeText("stroke", 100, 300); // stroke text
```

Path
Draw Triangle
``` js
ctx.beginPath();
ctx.moveTo(50, 50); // first point
ctx.lineTo(100, 150); // second point
ctx.lineTo(50, 150); // third point
ctx.closePath(); // back to first point
ctx.fill(); // fill color
ctx.stroke(); // stroke
```

Load Image and process and save to base64 data image