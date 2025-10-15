Documentation: https://motion.dev/

``` ts
import { motion } from "motion/react";

import { motion, AnimatePresence } from "motion/react";
```

``` tsx
<motion.div
	style={{
		...
	}}
	whileHover={{ background: "green" }} // hover state
	initial={{ rotate: "0deg" }} // start state
	animate={{ rotate: "135deg" }} // entry and animate
	transition = {{ duration: 1, delay: 1 }}
>
	divElement
</motion.div>
```

MotionConfig
``` tsx
<MotionConfig
	transition={{
		duration: 1,
		ease: "backInOut",
	}}
> ... </MotionConfig>
```

Variants
``` tsx
variants={{
	flip: {
	
	},
	banana: {
	
	}
}}
whileHover="flip"

//
animate={controls}

```

useAnimationControls
``` tsx
const controls = useAnimationControls()

() => {
	controls.start("flip")
}
```

`useInView`
``` tsx
const isInView = useInView(ref) // ref of the element
const isInView = useInView(ref, { once: true }) // only first time

// ===== Element =====
style = {{
	background: isInView ? "red" : "green"
}}
```

Scroll triggered
``` tsx
<motion.div>
	whileInView = {}
	viewport ={{
	 once: true,
	 amount: "some" | "all" | 0.8
	 // some -> play animation when partial appear
	 // all -> play animation when fully appear
	 // value
	 margin: "-200px" // offset
	}}
</motion.div>
```

control
``` ts
const control = useAnimation()

useEffect(() => {
	control.start("variantName")
}, [isInView])
```