https://gsap.com/docs/v3/Installation/

``` sh
# Install the GSAP library  
npm install gsap  
```

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


### React
``` sh
# Install the GSAP React package  
npm install @gsap/react
```

```js
import { useGSAP } from "@gsap/react";

gsap.registerPlugin(useGSAP);

// contextSafe outside useGSAP()
const { contextSafe } = useGSAP();
```

```js
useGSAP() => {}

useGSAP((context, contextSafe) => {

})

useGSAP((context, contextSafe) => {
	
	context.kill() // kill previous animation
	
	if (state) {
		gsap...
	} else {
		// clear first
		context.kill(); // keep property
		context.revert(); // not keep property
		gsap...
	}
}. [state])

```


array 
``` js
// a list of element
gsap.to(
	refList.current.map((i) => i.rotation),
	{
		y: `+=${Math.PI / 2}`,	
		repeat: -1,
		ease: "back",
		stagger: {
			each: 0.1,
		},
		duration: 1,
	}
);

// a list of meshes
refList.current.forEach((mesh, index) => {
	if (mesh) {
		gsap.to(mesh.scale, {
			x: 0.3,
			z: 0.3,
			delay: 0.25 * index,
			repeat: -1,
			yoyo: true,
			ease: "sine.inOut",
			duration: 1,
		});
	}
});
```