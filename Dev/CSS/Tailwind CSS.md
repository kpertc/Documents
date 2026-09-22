#web-dev 

[[CSS]]

https://tailwindcss.com/
playground: https://play.tailwindcss.com/

v4: `@import "tailwindcss";` in the CSS entry file, replaces `@tailwind base/components/utilities;`

utility
only used utilities are generated (default since v3, v4 engine = Oxide; "JIT" retired) 

text
```css
text-center
text-lg
text-blue-400
```        

margin
`{t|r|b|l}`
```css
mt-2 //top
ml // left
mr // right
```

padding
```css
p-2
px
py
```

border
```css
border-2 // border with border thickness 2
rounded-md // medium border radius
```

```

```

```js
// text ca not be selected
select-none
```

```css
shadow-xl
drop-shadow
```

use custom value -> bracket
```css
[30px]
[#973F29]
```

group
variant never contains a space → `hover:bg-red-500`, not `hover: bg-red-500`
```jsx
<div className="group" >
	<div className="group-hover:bg-red-500" />
</div>

// group name → name goes on the variant too
<div className="group/john" >
	<div className="group-hover/john:bg-red-500" />
</div>
```

peer
a **later sibling** reacts to this element's state (compiles to `~`), not children → use `group` for children
```jsx
<input className="peer" />
<p className="peer-focus:text-red-500" />

// peer name → name goes on the variant too
<input className="peer/john" />
<p className="peer-hover/john:bg-red-500" />
```

Built in Transition
```css
transition-colors
transition-colors duration-300
transition-colors duration-300 ease-in-out delay-300
```

```css
animate-spin
animate-ping
animate-pulse
animate-bounce
```

advanced: 
pseudo class

``` tsx
classname=`bg-${green}-500` // will not work, tailwindcss will optimize, will not include in the final bundle

const possible = ["bg-green-500", "bg-red-500"] // add to work, only if this file is scanned
```
classes that exist nowhere in source → `safelist: ['bg-green-500']` in tailwind.config.js (v3) / `@source inline("bg-green-500");` in CSS (v4)

`theme()`
```css
/* use tailwind color in CSS */
--workflow-node-bg: var(--color-neutral-900);
/* v3: theme('colors.neutral.900') — deprecated in v4 */
```

### Breakpoints
tailwindcss is mobile first
```css
// default 
sm: 640px // sm is for greater than sm size, use no prefix for sm
md: 768px
lg: 1024px
xl: 1280px
2xl: 1536px

// arbitrary size
max-[600px]:text-center
min-[320px]:text-center
```
### Dark Mode
```jsx
className="bg-white dark:bg-black"
```
default follows `prefers-color-scheme`; manual toggle: v4 `@custom-variant dark (&:where(.dark, .dark *));` in CSS / v3 `darkMode: 'class'` in tailwind.config.js

Custom style
https://tailwindcss.com/docs/theme
```css
// in your CSS entry file (app.css / globals.css)
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
```css
// in your CSS entry file (app.css / globals.css)
@layer components {
	.card {
		@apply m-10 rounded-lg bg-white
	}
}

// in
classname = "card"
```

base
```css
// in your CSS entry file (app.css / globals.css)
@layer base {
	h1 {
		...
	}
}
```

utility
```css
@utility flex-center {
	@apply flex justify-center items-center
}
``` 

Accent color
```html
classname="accent-pink-500"
```

Fluid Text
```

```

File


Highlight 
