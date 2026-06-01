#JavaScript 

[[CSS]]

https://tailwindcss.com/
playground: https://play.tailwindcss.com/

utility
JIT -> only generate the used CSS 

text
```
text-center
text-lg
text-blue-400
```        

margin
`{t|r|b|l}`
```
mt-2 //top
ml // left
mr // right
```

padding
```
p-2
px
py
```

border
```
border-2 // border with border thickness 2
rounded-md // medium border radius
```

```

```

```js
// text ca not be selected
select-none
```

```
shadow-xl
drop-shadow
```

use custom value -> bracket
```
[30px]
[#973F29]
```

group
```
<div classname="group" >
	<div classname-"group-hover: bg-red" />
</div>

group name
<div classname="group/john" >
	<div classname-"group-hover: bg-red" />
</div>
```

peer
same level children
```
<div classname="peer" >
	<div classname-"group-hover: bg-red" />
</div>

<div classname="peer/john" >

<div classname="peer-hover:bg-red" >
</div>
```

Built in Transition
```
transition-colors
transition-colors duration-300
transition-colors duration-300 ease-in-out delay-300
```

```
animate-spin
animate-ping
animate-pulse
animate-bounce
```

advanced: 
pseudo class

``` tsx
classname=`bg-${green}-500` // will not work, tailwindcss will optimize, will not include in the final bundle

const possible = ["bg-green-500", "bg-red-500"] // add to work
```

`theme()`
```css
/* use tailwind color in CSS */
--workflow-node-bg: theme('colors.neutral.900');
```

### Breakpoints
tailwindcss is mobile first
```
// default 
sm: 640px // sm is for greater than sm size, use no prefix for sm
md: 768px
lg: 1024px
xl: 1280px
2xl: 1536px

// arbitrary size
max-[600px]: text-center
min-[320px]: text-center
```
### Dark Mode
```
className = "bg-white dark:bg-blackf"
```

Custom style
https://tailwindcss.com/docs/theme
```
// in config
@theme {
	--color-chestnut: #973F29
}

// in 
classname = "text-chestnut"
```

base → global layout
component 
utilities → tailwindCSS classnames

component 
shadcn -> component
```
// in config
@layer components {
	.card {
		@apply m-10 rounded-lg bg-white
	}
}

// in
classname = "card"
```

base
```
// in config
@layer base {
	h1 {
		...
	}
}
```

utility
```
@utility flex-center {
	@apply flex justify-center items-center
}
``` 

Accent color
```
classname="accent-pink-500"
```

Fluid Text
```

```

File


Highlight 
