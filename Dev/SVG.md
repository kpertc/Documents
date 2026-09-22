
Scalable Vector Graphic (SVG) → Extensible Markup Language (XML) based

```html
<svg>
	<line />
	<rect />
	<circle />
	<polygon />
	<path />
	<path d="M0 0 L10 10" />
	<!-- group -->
	<g id=""> 
	
	</g>
</svg>
```

```html
<circle cx="50" cy="50" r="50" />
```

<br>

Properties|Value
---|---
x, y|number
fill|fill color
stroke|

Layer → order
html → strict `<tag> </tag>`, `<div />` is not self-closing; SVG / MathML are foreign elements so `<circle />` is valid; jsx supports `<tag />`
path -> path command
[d path commands](https://developer.mozilla.org/en-US/docs/Web/SVG/Attribute/d#path_commands)



```
<use />
<defs />
<mask />
```

`document.createElementNS("http://www.w3.org/2000/svg", "circle")` → `document.createElement("circle")` silently gives an unrenderable HTMLUnknownElement