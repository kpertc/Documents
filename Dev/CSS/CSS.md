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
`rem`, `em`: both relative to font size, rem -> always root font size; em -> the element's OWN computed font size, only inside `font-size` itself does it resolve against the parent (font-size inherits). On a 16px parent `{ font-size: 2em; padding: 1em }` gives 32px font AND 32px padding. Useful when scaling font with elements.
`fr`: grid only -> a fraction of the leftover space in `grid-template-columns` / `rows` and `grid-auto-*`. Flex has no `fr`, use the unitless grow factor (`flex: 1`)

``` css
font-size: clamp(MIN, PREFERRED, MAX); /* = max(MIN, min(PREFERRED, MAX)) */
font-size: clamp(50px, 8vw, 100px); /* 8vw font, floor 50px, ceiling 100px */
```

### Position

`Static`: default -> document flow

`Relative`: adjustable base on static

`Absolute`: ignore document flow, can be applied (top, right, bottom, left), relative to the nearest ancestor whose `position` is not `static` (an ancestor with `transform` / `filter` / `will-change` also becomes the containing block), without one, ultimately fall back to the initial containing block (viewport-sized, but move with content)

`Fixed`: Similar to absolute, relative to the viewport. Move with scroll.

`Sticky`: relative until it crosses the threshold, then fixed within its scroll container. Requires at least one of top / right / bottom / left, or it does nothing. Any ancestor with `overflow: hidden / auto / scroll` becomes its scroll container, so it silently stops sticking to the page.

  
<br>

### Display

Block: `<div>` occupy full line
Inline: `<span>` minimum size,
Inline-Block: flows inline, but can set width / height and vertical margin. Nothing defaults to it, opt in with `display: inline-block` (`<img>` is `display: inline` yet still takes width / height, being a replaced element)

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

gap: ; /* works on flex too, unlike grid-gap */
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
gap: 10px 20px; /* grid-gap is the legacy alias */ 
/* vertical, Horizontal */ 
```

Grid cross section
![[grid-cross-section.gif]]

<br>
### Scroll
```css
animation: animationName ...;

animation-timeline: scroll();
animation-timeline: scroll(x); /* for check horizontal percentage */

animation-timeline: view();
animation-timeline: view(250px); /* offset */

animation-range-start: 500px; /* start animation 500px away */
animation-range-end: 700px; /* end animation 700px away */
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
	content: attr(data-tooltip);
}
```
 
### Attribute Function
```css
attr() /* only usable in content; typed form attr(data-x type(<length>)) is new, check support */
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
:focus-visible /* keyboard-only focus ring */

:has() /* parent / previous-sibling selection */
:is() /* grouping */
:where() /* grouping, zero specificity */
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
```tsx
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
import containerStyles from "./container.module.css"

export default function Container({ children }) {

	return (
	<section className={containerStyles.container}>{children}</section>
	)
}
```

### IntersectionObserver
![[Web APIs#IntersectionObserver]]