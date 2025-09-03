https://gsap.com/docs/v3/Installation/

### Basics
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

`revert()` → returning the targets to their pre-animation state

### Utils
``` ts
// get elements to array
gsap.utils.toArray(".panel").forEach((panel, i) => {

})
```

Draggable ?
### ScrollTrigger

> https://gsap.com/docs/v3/Plugins/ScrollTrigger/

```js
import { ScrollTrigger } from "gsap/ScrollTrigger";

// register plugin - scroll trigger
gasp.registerPlugin(ScrollTrigger);
```

```js
gasp.to(".className", {
    x: 700,
    duration: 3,
    // Scroll Trigger
    // when .className element come into the viewport, move x to 700
	scrollTrigger: ".className"
})
```

``` ts
gasp.to(".className", {
    x: 700,
    duration: 3,
	scrollTrigger: {
		
		// toggle the playback of the animation
		trigger: ".a",
		endTrigger: ".c", // trigger can be different element
		// toggleAction: "play none none none", // default, only play one
		toggleAction: "restart none none none", // restart every time

		markers: true, // debug visualizer
		id: "my_id", // show text on the marker
		// const trigger = ScrollTrigger.getById("my-id"), can get the trigger
		
		start: "top center", // default, element, viewport
		start: "top center", // 20px from element top, and 80% of viewport
		end: "bottom top", // default
		end: "+=300", // += 300 unit relative to start
		end: () => value, // can be function, use dynamic value

		// scrub -> animate follow the scroll start-end range
		scrub: true, // true | number, number -> smooth

		// 
		pin: true,
		
		// callback
		onEnter: () => {}, // first time enter
		onLeave: () => {}, // first time leave
		onEnterBack: () => {}, // re-enter
		onLeaveBack: () => {}, // re-leave
		onUpdate: (self) => {
			self.progress // 0 - 1 progress
		},
		onToggle: (self) => { self.isActive }, // return true when in, return false when not in 
		toggleClass: '.classname', // apply class to change style when toggled

		// 
		scroller: "#container", // use other element instead of self viewport

		// 
		horizontal: true // watch horizontal scroller instead of vertical scroller
	}
})
```

embed Timeline and create ScrollTrigger independently

``` ts
const tl // timeline

ScrollTrigger.create({
	animation: tl 
})
```

``` ts
const trigger = ScrollTrigger.getById("my-id")
```

Set default behavior for ScrollTrigger
``` ts
ScrollTrigger.defaults({
	toggleActions: "restart pause resume none",
	markers: true
})
```

### ScrollSmoother

``` ts

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

### SplitText

> https://www.youtube.com/watch?v=L1afzNAhI40

``` ts
useGSAP(() => {
	if (!textRef.current) return;
	const split = SplitText.create(textRef.current, {
		type: "chars, lines, words", // create split object base on different level
		worldClass: "word", // add custom classname ".word", allow use css
	});

	console.log(split);

	// split.chars | split.lines | split.words
	gsap.from(split.lines, {
		y: 20,
		autoAlpha: 0,
		stagger: 0.05,
	});
}, []);
```

### MatchMedia

``` ts
const mm = gsap.matchMedia();

const scopeRef = useRef<HTMLDivElement>(null);
// const mm = gsap.matchMedia(scopeRef); // optional scope ref -> only animate children of the element
```

``` ts
mm.add(
	// conditions object
	{
		isMobile: "(max-width: 640px)", // media query string ?
		isDesktop: "(min-width: 641px)",
	},
	(context) => {
		console.log(context.conditions);
		
		if (!divRef.current) return;
		
		const conditions = context.conditions;
		
		// const {isMobile, isDesktop} = conditions;
		console.log(context.isReverted); // has been played?
		
		gsap.to(divRef.current, {
			background: conditions.isMobile ? "red" : "green",
		}
	);
	},
);

// clean up
mm.revert();
```
### drawSVG

``` ts
gsap.to(pathRef.current, { duration: 1, drawSVG: `${progress * 100}%` });

gsap.fromTo(
	pathRef.current,
	{ drawSVG: `40% 60%` }, // from 40% - 60%
	{ duration: 1, drawSVG: `100%` }, // to 0 - 100%
	// can also animate other properties on the svg element
	// { stoke: "white", strokeWidth: 20, fill: "green" }
);

drawSVG: `20 350` // absolute unit

```
### MorphSVG

let object follow a path

``` ts
const motionPath = MorphSVGPlugin.pathDataToBezier("#selector")
```

``` ts

```

### Motion Path
follow a path, path can be svg

``` ts

```

``` ts
gsap.to("#rect", // the element to animate
{
	duration: 5,
	motionPath: {
		path: "#path" // the svg path
		autoRotate: true, // move and rotate follow the front direction

		delay: 2,

// start and end base on path ratio
		start: 0.25, 
		end: 0.75,
		end: 1.5, // repeat back to 0.5

		align: "#path" // change coord to target coord

		curveness: // 0 - 1, can covert straight line to curve line
	}
})
```

``` ts
MotionPathHelper.create("#rect")
// copy motion path
```
### Flip
FLIP → First, Last, Invert, Play

- change css style
- change dom nested structure



``` ts
fill: gsap.utils.interpolate([colorString1, colorString2], idx / numberOfDots),
```