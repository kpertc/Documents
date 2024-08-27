https://lesscss.org/

[[CSS]]

`.less` → compile down to `.css`

```
// variable
@background-color:#f4f4f4; 
```

```
h1 {
	.bordered // use .bordered properties
}

.bordered {
	...
}
```

```
// inherit
.btn{
	...
}

.primary-btn:extend(.btn){
	...
}
```

### Mixins
```
.btn {
	.border-radius(10px);
}

.border-radius(@radius) {
	border-radius: @radius;
}
```

nest
```
ul#menu{
	list-style: none;
	li {
		padding: 10px 0;
		a {
			color: #ffffff;
			&:hover {
				
			}
		}
	}
}
```