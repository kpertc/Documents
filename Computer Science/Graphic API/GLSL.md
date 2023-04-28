[[OpenGL]]

OpenGL Shading Language
Syntax similar to C/C++

-   Version Specification
    -   OpenGL version
    -   GLSL version

### Comment
```glsl
/* 
	Multi-line comment
*/

// Single-line comment
```

### Variable

<div style="display: grid; grid-template-columns: repeat(3, 2fr); grid-gap: 10px;">
	<div> 
		<span>float</span><br>
		<span>vec2</span><br>
		<span>vec3</span><br>
		<span>vec4</span><br>
	 </div> 
	 <div> 
		<span></span><br>
		<span>mat2</span><br>
		<span>mat3</span><br>
		<span>mat4</span><br>
	 </div> 
	 <div> 
		<span>int</span><br>
		<span>ivec2</span><br>
		<span>ivec3</span><br>
		<span>ivec4</span><br>
	 </div> 
</div>

bool
sampler2D

<br>

### Float

```glsl
vec3 color = vec3(0.0, 0.0 ,0.0);

vec3 color = vec3(1.0); // = vec3(1.0, 1.0, 1.0)

// compose vector
vec4 colorAlpha = vec4(color, 1.0);
```

### Vector 

```glsl
vec3 color = vec3(0.0, 0.0 ,0.0);

vec3 color = vec3(1.0); // = vec3(1.0, 1.0, 1.0)

// compose vector
vec4 colorAlpha = vec4(color, 1.0);
```

##### Swizzling
```glsl
vec3 color = colorAlpha.rgb;
vec3 colorBGR = colorAlpha.bgr;
vec4 grayscale = colorAlpha.rrra;
```

<div style="display: grid; grid-template-columns: repeat(4, 2fr); grid-gap: 10px;">
	<div> 
		<span>Array-style accessor</span><br>
		<span>[0]</span><br>
		<span>[1]</span><br>
		<span>[2]</span><br>
		<span>[3]</span><br>
	 </div> 
	 <div> 
		<span>Coordinate Dimension</span><br>
		<span>.x</span><br>
		<span>.y</span><br>
		<span>.z</span><br>
		<span>.w</span><br>
	 </div> 
	 <div> 
		<span>Color Channel</span><br>
		<span>.r</span><br>
		<span>.g</span><br>
		<span>.b</span><br>
		<span>.a</span><br>
	 </div> 
	 <div> 
		<span>Texture Dimension</span><br>
		<span>.s</span><br>
		<span>.t</span><br>
		<span>.p</span><br>
		<span>.q</span><br>
	 </div> 
</div>

### Matrix

```glsl
mat3 identityMatrix = mat3(
	1.0, 0.0, 0.0,
	0.0, 1.0, 0.0,
	0.0, 0.0, 1.0
);
```

### Function
```glsl
float computeSum(float a, float b) {
	return a + b;
}
```

```glsl
float computeSum(in float a, in float b) {
	return a + b;
}

float computeSum(out float a, out float b) {
	return a + b;
}

float computeSum(inout float a, inout float b) {
	return a + b;
}
```