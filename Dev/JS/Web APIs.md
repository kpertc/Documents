
### IntersectionObserver
Lazy load / infinite scroll
```js
const observer = new IntersectionObserver(
	// callback
	entries => {
		entries.forEach(entry => {
			// when observer update, do something
			entry.target.classList.toggle("show", entry.isIntersecting)
			// when observed, remove observe the element
			if (entry.isIntersecting) observer.unobserve(entry.target)
		})
	},
	// options
	{
		threshold: 1, // default -> 0
		rootMargin: "-100px",
		root: null // null -> viewport (default), or an element to scroll within
	}
)

observer.observe(element)
```