#CG 

Old: Immediate mode → Fixed function pipeline
New: Core-profile mode → immediate mode deprecated in v3.0, removed in v3.1 (v3.2 added the core / compatibility profile split)

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
	gl_FragColor = vec4(1,1,0,1); // GLSL 1.20 only
	// GLSL 3.30 core / ES 3.00: out vec4 fragColor; fragColor = vec4(1,1,0,1);
}
```



Command Palate show GLSL Canvas

## Vertex Shader
```glsl
// varying vec2 texCoords

void main() {
	texCoords = ...
	
	gl_Position = projectionMatrix * modelViewMatrix * vec4(position, 1.0);
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
	gl_FragColor = vec4(1,1,0,1); // GLSL 1.20 only
	// GLSL 3.30 core / ES 3.00: out vec4 fragColor; fragColor = vec4(1,1,0,1);
}
```

<br>

qualifiers

### `attribute`
```glsl
// GLSL 1.20 / ES 1.00 (WebGL1)
attribute vec3 position;
attribute vec2 texcoord0;

// GLSL 3.30 core / ES 3.00 (WebGL2) -> attribute / varying removed
in vec3 position;
in vec2 texcoord0;
```

> [attribute](https://thebookofshaders.com/glossary/?search=attribute#:~:text=attribute%20read%2Donly%20variables%20containing,texture%20coordinates%20of%20a%20vertex)  read-only variables containing data shared from WebGL/OpenGL environment to the ==vertex shader==.

<br>

### `varying`
```glsl
// GLSL 1.20 / ES 1.00 (WebGL1)
varying vec2 uv;

// GLSL 3.30 core / ES 3.00 (WebGL2): out in vertex shader, in in fragment shader
out vec2 uv; // vertex
in  vec2 uv; // fragment
```

> `varying` variables contain data shared from a vertex shader to a fragment shader.

<br>

### `uniform`
```glsl
uniform float u_time;
```

> `uniform` read-only values set per draw call from the host, identical for every vertex / fragment, usable in both stages.
> JS side: `gl.getUniformLocation(program, 'u_time')` → `gl.uniform1f(loc, t)`
