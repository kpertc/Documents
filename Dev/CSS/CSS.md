### CSS Pre-processor
- [[SCSS]]
- [[Less]]

### Variable

```css
:root {
--variable: value;
}

/* Use a variable */ 
background: var(--variable);
```

```css
:root {
	--dark-color: #535bff;
	--light-color: #80e9ff;
}

#darkGroup {
	fill: var(--dark-color);
}
```
### Todo React


### Units

`%` relative to parent
`vw` `vh`: view-width / view-height, relative to entire ==viewport==
	1 viewport unit is 1% of viewport length, can be used for font
`rem`, `em`: both relative to font size, rem -> always root font size; em -> relative to parent's font size. Useful when scaling font with elements.
`fr`: use in flex and grid

``` css
font-size: clamp(min, current, upper)
font-size: clamp(50px, 8vw, 100px) // 8vw font, low to 50px, up tp 100px
```

### Position

`Static`: default -> document flow

`Relative`: adjustable base on static

`Absolute`: ignore document flow, can be applied (top, right, bottom, left), to relative to parent, without parent, ultimately fall back to root, relative to the viewport, move with content

`Fixed`: Similar to absolute, relative to the viewport. Move with scroll.

`Sticky`:

  
<br>

### Display

Block: `<div>` occupy full line
Inline: `<span>` minimum size,
Inline-Block: `<img>` similar to inline, but can set width / height

None:

Flex:
![[flex.png]]

##### Flexbox
Flexible Box Model
https://css-tricks.com/snippets/css/a-guide-to-flexbox/


- Container
```CSS
display: flex;

flex-direction: row | column

/* for Main Axis */ 
justify-content: flex-start; /* flex-start, center, space-between, space-around */ 

/* Cross Axis */ 
align-items:  ;

flex-wrap: ;
```

- Flex item (Children)
```css
flex-basis: ;

order: ; /* customize order */
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
### Scroll
```css
animation: animationName ...;

animation-timeline: scroll()
animation-timeline: scroll(x) // for check horizontal percentage

animation-timeline: view()
animation-timeline: view(250px) // offset

animation-range-start: 500px; // start animation 500px away
animation-range-end: 700px; // end animation 700px away
```

<br>

### Attribute selector

```html
<a href="..."> ... </a>
<button data-tooltip="Tooltip">Submit form</button>
```

```css
a[href] {

}

a[target="_blank"] {

}

[data-tooltip]::after {
	content: 
}
```
 
### Attribute Function
```css
attr()
```

[Pseudo-classes_and_pseudo-elements](https://developer.mozilla.org/en-US/docs/Learn/CSS/Building_blocks/Selectors/Pseudo-classes_and_pseudo-elements)

### Pseudo Classes
state
```css
:first-child
:last-child
:only-child
:invalid

:hover
:focus
```

### Pseudo Elements
actual part

< css3 `:` single colon
\> css3 `::` double colon

```css
::before
::after

::selection
```

`::before` ☞ red
`::after` ☞ blue

![[PseudoElements-before-after.png]]
> [Learn CSS Pseudo Elements In 8 Minutes by Web Dev Simplified](https://youtu.be/OtBpgtqrjyo?si=c2Zo524sbyPGlbjO)

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

### IntersectionObserver
![[Web APIs#IntersectionObserver]]