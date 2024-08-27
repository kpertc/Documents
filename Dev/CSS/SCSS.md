[[CSS]]


- Variable
- Nesting
  
```scss
button {
	a {
		front-weight: bold;
	}
  
	.success {
		color: green;
	}
}
```

```scss
.btn {
	&:focus {}
	&:hover {}
	&:active {}
}
```


##### @mixin
```scss
@mixin cool-button($color, $bg) {
	display: flex;
	color: $color;
	background: $bg;
}

.btn-orange {
	@include cool-button(black, orange);
}
```


##### Programming?
```scss
@if $theme == 'light' {
	background-color: $light-bg;
}@else {

}

$sizes: 40px, 50px, 80px;
@each $size in $sizes {
	.icon-#{size} {
		font-size: $size;
	}
}

@function sum($number) {
	$sum: 0;
	...
	@return $sum
}

```