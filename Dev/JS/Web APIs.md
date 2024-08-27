
### IntersectionObserver
Lazy load / infinite scroll
```js
const observer = new IntersectionObserver(
	// callback
	entries => {
		entries.forEach(entry => {
			// when observer update, do something
			entry.target.classList.toggle("show", entry.IsIntersecting)
			// when observed, remove observe the element
			if (entry.isIntersecting) observer.unobserve(entry.target)
		})
	},
	// options
	{
		threshold: 1, // default -> 0
		rootMargin: "-100px",
		root: 
	}
)

observer.observe(element)
```