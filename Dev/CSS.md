### Variable

```css
:root {
--variable: value;
}

/* Use a variable */ 
background: var(--variable);
```


### Todo React



### Units

`%` relative to parent
`vw` `vh`: view-width / view-height, relative to entire viewport
`rem`, `em`: both relative to font size, rem -> always root font size; em -> relative to parent's font size. Useful when scaling font with elements.
`fr`: use in flex and grid

  

### Position

`Static`: default -> document flow

`Relative`: adjustable base on static

`Absolute`: ignore document flow, can be applied (top, right, bottom, left), to relative to parent, without parent, ultimately fall back to root, relative to the viewport, move with content

`Fixed`: Similar to absolute, relative to the viewport. Move with scroll.

`Sticky`:

  

### Display

Block: `<div>` occupy full line

Inline: `<span>` minimum size,

Inline-Block: `<img>` similar to inline, but can set width / height

None:

Flex:
![[flex.png]]

Flexbox
https://css-tricks.com/snippets/css/a-guide-to-flexbox/

```CSS
display: flex;

/* for Main Axis */ 
justify-content: flex-start; /* flex-start, center, space-between, space-around */ 

/* Cross Axis */ 
align: 
```

Grid

```CSS
display: grid;
grid-template-columns: 1fr 1fr 1fr;
Grid-template-rows: 1fr 1fr 1fr;
grid-gap: 10px 20px; 
/* vertical, Horizontal */ 
```

Grid cross section
![[grid-cross-section.gif]]

<br>

### Dark Mode

https://lukelowrey.com/css-variable-theme-switcher/

```css
:root {
    --background-color: #fff;
    --text-color: #121416d8;
    --link-color: #543fd7;
}

html[data-theme='light'] {
    --background-color: #fff;
    --text-color: #121416d8;
    --link-color: #543fd7;
}

html[data-theme='dark'] {
    --background-color: #212a2e;
    --text-color: #F7F8F8;
    --link-color: #828fff;
}
```

### React CSS Properties Object
```jsx
const buttonStyle: React.CSSProperties = {
	padding: "20px",
	margin: "10px",
	fontSize: "20px",
};

<button style={buttonStyle}> ... </button>
```

### .module.css

component scope css
```jsx
import React from "react"
import * as containerStyles from "./container.module.css"

export default function Container({ children }) {

	return (
	<section className={containerStyles.container}>{children}</section>
	)
}
```