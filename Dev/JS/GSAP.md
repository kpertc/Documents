https://gsap.com/docs/v3/Installation/

``` js
gsap.to(
	mesh.rotation,
	{
	  duration: 1.5,
	  ease: 'power2.inOut', // ease ☞ https://gsap.com/docs/v3/Eases
	  x: '+=6',
	  y: '+=3'
	}
)
```

``` js
gsap.to(
	material.uniforms.uUniform,
	{
		duration: 3.0,
		value: 1.0, 
		onComplete: () => {}
	}
)

gsap.fromTo(
	// from
	{
		value: 0,
	},
	// to
	{
		duration: 0.7,
		ease: "power2.out",
		value: 1,
		onComplete: () => {
			...
		},
}
}
```


Scroll Trigger

```js
// register plugin - scroll trigger
gasp.registerPlugin(ScrollTrigger);
```

```js
// animate CSS
gasp.to(".className", {
    x: 700,
    duration: 3,
    // Scroll Trigger
    // when .className element come into the viewport
	scrollTrigger: ".className"
})
```