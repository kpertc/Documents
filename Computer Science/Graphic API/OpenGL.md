#CG 

Old: Immediate mode → Fixed function pipeline
New: Core-profile mode → Deprecate immediate mode from v3.2

Learn from OpenGL v3.3

[The Book of Shaders](https://thebookofshaders.com/)

[[OpenGL Examples]]

### GLSL

[[GLSL]]

-   lowp
-   mediump
-   Highp

https://www.shaderific.com/glsl-qualifiers

Setup in VSCode:
	Shader Language support for VSCode
	glsl canvas



```


```

## 
```glsl
void main() {
	gl_FragColor = vec4(1,1,0,1);
}
```



Command Palate show GLSL Canvas

## Vertex Shader
```glsl
// varying vec2 texCoords

void main() {
	texCoords = ...
	
	gl_Position = 
}
```


## Fragment Shader

```c++
#ifdef GL_ES
precision mediump float;
#endif

const float PI = 3.1415926535897932384626433832795;

// varying vec2 texCoords

void main() {
	// texCoords do something
	gl_FragColor = vec4(1,1,0,1);
}
```

<br>

qualifiers

### `attribute`
```glsl
attribute vec3 position;
attribute vec2 texcoord0;
```

> [attribute](https://thebookofshaders.com/glossary/?search=attribute#:~:text=attribute%20read%2Donly%20variables%20containing,texture%20coordinates%20of%20a%20vertex)  read-only variables containing data shared from WebGL/OpenGL environment to the ==vertex shader==.

<br>

### `varying`
```glsl
varying vec2 uv;
```

> `varying` variables contain data shared from a vertex shader to a fragment shader.

<br>

### `uniform`
```glsl

```
