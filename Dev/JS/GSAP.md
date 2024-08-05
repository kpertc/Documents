https://gsap.com/docs/v3/Installation/

``` js
gsap.to(
	mesh.rotation,
	{
	  duration: 1.5,
	  ease: 'power2.inOut',
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
```