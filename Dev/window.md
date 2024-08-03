#JavaScript 
### Mouse move
``` js
window.addEventListener('mousemove', (e) => {
	// mouse move
	
	// pixel distance
	e.clientX 
	e.clientY

	// to get screen base 0 - 1 value (normalized)
	e.clientX / window.innerWidth
	e.clientX / window.innerHeight

	// centered
	e.clientX / window.innerWidth - 0.5
	e.clientX / window.innerHeight - 0.5
})
```

### Scroll
``` js
window.addEventListener('scroll', () => {
	// is scrolling
	window.scrollY
})
```

### Get Device Pixel Ratio
``` js
window.devicePixelRatio
```