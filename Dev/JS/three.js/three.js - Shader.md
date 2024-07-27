## Custom shader

[ShaderMaterial](https://threejs.org/docs/#api/en/materials/ShaderMaterial)

## Use Shader Code in js files
### File
	↳ `vertex.glsl`
	↳ `fragment.glsl`

GLSL code in `.glsl.js` file

```js
const vertex = /* glsl */ `
    ...
`;

export default vertex;

// import at other file
import vertex from './shaders/vertex.js'
```

Include three.js header files

```OpenGL
#include <common>
```

### type
``` ts
declare module "*.glsl" {
	const value: string;
	export default value;
}
```

### Vite setup

[npm - vite-plugin-glsl](https://www.npmjs.com/package/vite-plugin-glsl)

``` js
// install "vite-plugin-glsl"
import glsl from "vite-plugin-glsl";
...
plugins: [glsl()],
```

use `#include` with `vite-plugin-glsl` plugin
![[threejs-shader-vite-include.png]]

### Write Shader
- [[OpenGL]]
- [[GLSL]]

## ShaderMaterial

- ShaderMaterial
- RawShaderMaterial - no built-in uniforms and attributes

```ts
// create
import vertexShader from "../shaders/vertex.glsl";
import fragmentShader from "../shaders/fragment.glsl";

const customMaterial = new THREE.ShaderMaterial({
	vertexShader: vertexShader,
	fragmentShader: fragmentShader,
	side: THREE.DoubleSide,
	uniforms: {
		uTime: { value: 1.0 },
		uTexture: { value: texture },
	},
	transparent: true, // Enable transparency
});

// set uniform
_mesh.material.uniforms.uTime.value += 0.1;
```

Threejs shader uniform: https://threejs.org/docs/index.html#api/en/renderers/webgl/WebGLProgram

Threejs shader path: `three.js/src/renderers/shaders/`

> [!NOTE] VScode plugin `glsl-literal`
> Using `.glsl.js` file, get syntax highlight
Put `/* glsl */` to get syntax highlight

Overwrite built-in shader
[[YouTube] Customize ThreeJS Materials With Shaders](https://www.youtube.com/@visionary_3_d)
```ts
const _material = new MeshStandardMaterial({
    color: '#f69f1f',
    metalness: 0.5,
    roughness: 0.7,
    
    // get shader 
    onBeforeCompile: (shader) => {         
        // shader content
        shader.vertexShader
        shader.fragmentShader
        
        // edit fragment shader
        shader.fragmentShader = shader.fragmentShader.replace(
            /* glsl */`#include <color_fragment>`,
            /* glsl */`#include <color_fragment>
                
                #ifdef NO_ANIMATION
                    greenValue = 1.0;
                #else
                    greenValue = sin(uTime);
                #endif
                
                diffuseColor = vec4(1, greenValue, 0, 1);
            `
        )
        
        // get & set shader uniform
        shader.uniform
        shader.uniform.uTime.value = 1.0;
        
        // save shader variable for later use
        _material.userData.shader = shader
    }
}

// define
_material.defines.NO_ANIMATION = true; // or false
```

##### A minimal texture shader
```ts
new TextureLoader().load("./texture.png", (texture) => {

// Vertex shader
const vertexShader = /* glsl */ `
	varying vec2 vUv;
	uniform sampler2D uTexture;
	void main() {
		vUv = uv;
		gl_Position = projectionMatrix * modelViewMatrix * vec4(position, 1.0);
	}
`;

// Fragment shader
const fragmentShader = /* glsl */ `
	varying vec2 vUv;
	uniform sampler2D uTexture;
	
	void main() {
		vec4 textureColor = texture2D(uTexture, vUv);
		gl_FragColor = textureColor;
	}
`;

const shaderMaterial = new ShaderMaterial({
		vertexShader: vertexShader,
		fragmentShader: fragmentShader,
			uniforms: {
				uTexture: { value: texture },
			},
		transparent: true, // Enable transparency
	});

	cube = new Mesh(cubeGeometry, shaderMaterial);
	cube.castShadow = true;
	cube.position.y = 0.5;
	scene.add(cube);
});
```

use `#include <colorspace_fragment>` at the end of fragment shade to output color in sRGB color space

## Inject built-in material

| Variable name | Meaning | Type | File                      | Require                       |
| ------------- | ------- | ---- | ------------------------- | ----------------------------- |
| diffuseColor  | 颜色      |      | `color_fragment.glsl.js`  |                               |
|               |         |      |                           |                               |
|               |         |      |                           |                               |
| vPosition     | 本地坐标    |      | `begin_vertex.glsl.js`    | require define `Alphahash`    |
| worldPosition | 世界空间坐标  | vec4 | `worldpos_vertex.glsl.js` | require define `transmission` |
| vUv           | UV      |      | `uv_vertex.glsl.js`       |                               |
|               |         |      |                           |                               |

```
// get worldPos
varying vec3 vWorldPosition;

vec4 worldPosition = modelMatrix * vec4(position, 1.0);
vWorldPosition = worldPosition.xyz;
```

##### Custom Shader Helper Function

```JavaScript
let g_shader: any; // global variable to store the shader

interface Uniform {
  name: string;
  value: any;
}

interface ShaderParams {
  uniforms?: Uniform[];
  vsInsertBeforeMain: string;
  vsInsertEndOfMain: string;
  fsInsertBeforeMain: string;
  fsInsertEndOfMain: string;
  callBack?: (shader: any) => void;
}

// 使用案例
const customShaderPararms: ShaderParams = {
  uniforms: [{ name: "u_Time", value: 0 }],
  fsInsertBeforeMain: /* glsl */ `
    uniform float u_Time;
  `,
  fsInsertEndOfMain: /* glsl */ `
    gl_FragColor = vec4(u_Time, 0.0, 0.0, 1.0);
  `,

  callBack: (shader) => { // custom shader behavior
    g_shader = shader;
    console.log(shader);
  },
};

export function customMeshPhysicalMaterial(shader: any, params: ShaderParams) {
  // Add custom uniforms
  if (params.uniforms) {
    params.uniforms.forEach((uniform: Uniform) => {
      shader.uniforms[uniform.name] = { value: uniform.value };
    });
  }

  // Inject code before main function in vertex shader
  if (params.vsInsertBeforeMain) {
    shader.vertexShader = shader.vertexShader.replace(
      "#include <clipping_planes_pars_vertex>",
      `#include <clipping_planes_pars_vertex>\n${params.vsInsertBeforeMain}`
    );
  }

  // Inject code at the end of main function in vertex shader
  if (params.vsInsertEndOfMain) {
    shader.vertexShader = shader.vertexShader.replace(
      "#include <fog_vertex>",
      `#include <fog_vertex>\n${params.vsInsertEndOfMain}`
    );
  }

  // Inject code before main function in fragment shader
  if (params.fsInsertBeforeMain) {
    shader.fragmentShader = shader.fragmentShader.replace(
      "#include <clipping_planes_pars_fragment>",
      `#include <clipping_planes_pars_fragment>\n${params.fsInsertBeforeMain}`
    );
  }

  // Inject code at the end of main function in fragment shader
  if (params.fsInsertEndOfMain) {
    shader.fragmentShader = shader.fragmentShader.replace(
      "#include <dithering_fragment>",
      `#include <dithering_fragment>\n${params.fsInsertEndOfMain}`
    );
  }

  if (params.callBack) params.callBack(shader);
}
```

在`onBeforeCompile`中使用
```JavaScript
const physicalMaterial = new MeshPhysicalMaterial({
    normalMap: texture,
    metalness: 0.9,
    roughness: 0.5,
    clearcoat: 1.0,
    clearcoatRoughness: 0.1,
    transparent: true,
    transmission: 1.0, // to enable worldposit
    color: 0x8418ca,
    onBeforeCompile: (shader) => {
        customMeshPhysicalMaterial(shader, customShaderPararms);
    },
});
```

### Attribute

add custom attribute via BufferGeometry

in three.js
```javascript
const count = geometry.attributes.position.count
const randoms = new Float32Array(count)

for(let i = 0; i < count; i++)
{
    randoms[i] = Math.random()
}

geometry.setAttribute('aRandom', new THREE.BufferAttribute(randoms, 1))
```

in shader
```glsl
attribute float aRandom;
```

### Shader Effects
##### Blink
```c++
// blink
float blinkValue = step(0.5, fract(u_Time));
// fract() to extract the fractional part (i.e., the 0.xxx part)

// gradient blink
float blinkValue = abs(sin(u_Time));
```

##### Perlin 3D Noise
```c++

Classic Perlin 3D Noise 
// by Stefan Gustavson
//
vec4 permute(vec4 x)
{
    return mod(((x*34.0)+1.0)*x, 289.0);
}
vec4 taylorInvSqrt(vec4 r)
{
    return 1.79284291400159 - 0.85373472095314 * r;
}
vec3 fade(vec3 t)
{
    return t*t*t*(t*(t*6.0-15.0)+10.0);
}

float cnoise(vec3 P)
{
    vec3 Pi0 = floor(P); // Integer part for indexing
    vec3 Pi1 = Pi0 + vec3(1.0); // Integer part + 1
    Pi0 = mod(Pi0, 289.0);
    Pi1 = mod(Pi1, 289.0);
    vec3 Pf0 = fract(P); // Fractional part for interpolation
    vec3 Pf1 = Pf0 - vec3(1.0); // Fractional part - 1.0
    vec4 ix = vec4(Pi0.x, Pi1.x, Pi0.x, Pi1.x);
    vec4 iy = vec4(Pi0.yy, Pi1.yy);
    vec4 iz0 = Pi0.zzzz;
    vec4 iz1 = Pi1.zzzz;

    vec4 ixy = permute(permute(ix) + iy);
    vec4 ixy0 = permute(ixy + iz0);
    vec4 ixy1 = permute(ixy + iz1);

    vec4 gx0 = ixy0 / 7.0;
    vec4 gy0 = fract(floor(gx0) / 7.0) - 0.5;
    gx0 = fract(gx0);
    vec4 gz0 = vec4(0.5) - abs(gx0) - abs(gy0);
    vec4 sz0 = step(gz0, vec4(0.0));
    gx0 -= sz0 * (step(0.0, gx0) - 0.5);
    gy0 -= sz0 * (step(0.0, gy0) - 0.5);

    vec4 gx1 = ixy1 / 7.0;
    vec4 gy1 = fract(floor(gx1) / 7.0) - 0.5;
    gx1 = fract(gx1);
    vec4 gz1 = vec4(0.5) - abs(gx1) - abs(gy1);
    vec4 sz1 = step(gz1, vec4(0.0));
    gx1 -= sz1 * (step(0.0, gx1) - 0.5);
    gy1 -= sz1 * (step(0.0, gy1) - 0.5);

    vec3 g000 = vec3(gx0.x,gy0.x,gz0.x);
    vec3 g100 = vec3(gx0.y,gy0.y,gz0.y);
    vec3 g010 = vec3(gx0.z,gy0.z,gz0.z);
    vec3 g110 = vec3(gx0.w,gy0.w,gz0.w);
    vec3 g001 = vec3(gx1.x,gy1.x,gz1.x);
    vec3 g101 = vec3(gx1.y,gy1.y,gz1.y);
    vec3 g011 = vec3(gx1.z,gy1.z,gz1.z);
    vec3 g111 = vec3(gx1.w,gy1.w,gz1.w);

    vec4 norm0 = taylorInvSqrt(vec4(dot(g000, g000), dot(g010, g010), dot(g100, g100), dot(g110, g110)));
    g000 *= norm0.x;
    g010 *= norm0.y;
    g100 *= norm0.z;
    g110 *= norm0.w;
    vec4 norm1 = taylorInvSqrt(vec4(dot(g001, g001), dot(g011, g011), dot(g101, g101), dot(g111, g111)));
    g001 *= norm1.x;
    g011 *= norm1.y;
    g101 *= norm1.z;
    g111 *= norm1.w;

    float n000 = dot(g000, Pf0);
    float n100 = dot(g100, vec3(Pf1.x, Pf0.yz));
    float n010 = dot(g010, vec3(Pf0.x, Pf1.y, Pf0.z));
    float n110 = dot(g110, vec3(Pf1.xy, Pf0.z));
    float n001 = dot(g001, vec3(Pf0.xy, Pf1.z));
    float n101 = dot(g101, vec3(Pf1.x, Pf0.y, Pf1.z));
    float n011 = dot(g011, vec3(Pf0.x, Pf1.yz));
    float n111 = dot(g111, Pf1);

    vec3 fade_xyz = fade(Pf0);
    vec4 n_z = mix(vec4(n000, n100, n010, n110), vec4(n001, n101, n011, n111), fade_xyz.z);
    vec2 n_yz = mix(n_z.xy, n_z.zw, fade_xyz.y);
    float n_xyz = mix(n_yz.x, n_yz.y, fade_xyz.x); 
    return 2.2 * n_xyz;
}
```