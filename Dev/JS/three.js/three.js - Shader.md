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

### Write Shader
- [[OpenGL]]
- [[GLSL]]

- Threejs shader built-in uniform: https://threejs.org/docs/index.html#api/en/renderers/webgl/WebGLProgram
- Threejs shader path: `three.js/src/renderers/shaders/`

- Shader Library: [lygia](https://github.com/patriciogonzalezvivo/lygia)

Dev Setup:

![[three.js - Setup#Shader]]

![[three.js - Setup#Vite GLSL plugin setup]]
## ShaderMaterial

- ShaderMaterial
- RawShaderMaterial - no built-in uniforms and attributes

##### A minimal shader Template
```js
const shaderMaterial = new ShaderMaterial({
	vertexShader: /* glsl */ `
	varying vec2 vUv;
	
	void main() {
		vUv = uv;
		gl_Position = projectionMatrix * modelViewMatrix * vec4(position, 1.0);
	}
	`,
	fragmentShader: /* glsl */ `
	varying vec2 vUv;
	
	void main() {
	
		gl_FragColor = vec4(1.0, 0.0, 0.0, 1.0);
	}
	`,
});
```

add `tonemapping_fragment` &  `colorspace_fragment` to the end of fragment shader
```glsl
#include <tonemapping_fragment> // optional, if use tonemapping feature
#include <colorspace_fragment> // output color in sRGB color space
```
##### Uniforms & Properties
```ts
// create
import vertexShader from "../shaders/vertex.glsl";
import fragmentShader from "../shaders/fragment.glsl";

const customMaterial = new THREE.ShaderMaterial({
	// there is a default shader when vertexShader and fragmentShader are not provided
	vertexShader: vertexShader,
	fragmentShader: fragmentShader,
	
	side: THREE.DoubleSide,
	uniforms: {
		uTime: { value: 1.0 },
		uTexture: { value: texture },
		// setting uniforms by values or setting uniforms by new Uniform()
		// https://threejs.org/docs/#api/en/core/Uniform
	},
	transparent: true, // Enable transparency
	// wireframe: true // wireframe is always support, even when no vs and fs
});

// set uniform
_mesh.material.uniforms.uTime.value += 0.1;
```
##### Set Uniform value by reference - `Uniform` Class
no need to set uniform in material like `_mesh.material.uniforms.uTime.value = ...`
``` js
// create uniform / create debugUI object
const debugeObj = {
	uniform: new Uniform(0)
}

...

// add to shaderMaterial
const shaderMaterial = new ShaderMaterial({ 
	uniforms: {
		uUniform: debugeObj.uniform
	},

...
// set by referencing class
debugeObj.uniform.value = ...

// set by debug object
gui.add(debugeObj.uniform, "value").min(0).max(1)
```
##### Overwrite built-in shader
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

##### Shader for Points / Particles
Compensate the size of renderer pixel ratio
```JavaScript
uniforms: {
	uSize: { value: 8 * renderer.getPixelRatio() }
}
```

Size attenuation
reference can be found at `points_vert.glsl.js`
```js
gl_PointSize *= (1.0 / - viewPosition.z);
```

`gl_PointCoord` is the UV in fragment shader
```JavaScript
gl_FragColor = vec4(gl_PointCoord, 1.0, 1.0)
```

draw circle, distance to center, `vec2(0.5) // center
```JavaScript
float circle = distance(gl_PointCoord, vec2(0.5))
```

some hardware (windows) can not render `gl_PointSize` below 1.0
``` js
// Move point to far away to hide points
if (gl_PointSize < 1.0) 
    gl_Position = vec4(9999.9);
```

##### Post Process Shader

post-process shader reference `/three/examples/jsm/shaders/xxx.js`
``` js
const customShader = {
	uniforms: {
		tDiffuse: { value: null }, // previous image
	},
	vertexShader: /* glsl */ `
		varying vec2 vUv;
		void main()
		{
			vUv = uv;
			gl_Position = vec4(position, 1.0);
		}
	`,
	fragmentShader: /* glsl */ `
		varying vec2 vUv;
		uniform sampler2D tDiffuse;
		void main()
		{
			vec4 base = texture2D( tDiffuse, vUv ); // previous image
			gl_FragColor = vec4(base.rgb, 0.1);
		}
	`,
};

const shaderPass = new ShaderPass(customShader);
effectComposer.addPass(shaderPass);
```

update shader uniform by accessing `_shaderPass.material`
```js
_shaderPass.material.uniforms.${uniformName}.value = ...
```

##### Screen Space Plane
``` js

```

## Inject built-in material

| Variable name | Meaning | Type | File                      | Require                       |
| ------------- | ------- | ---- | ------------------------- | ----------------------------- |
| diffuseColor  | 颜色      |      | `color_fragment.glsl.js`  |                               |
|               |         |      |                           |                               |
|               |         |      |                           |                               |
| vPosition     | 本地坐标    |      | `begin_vertex.glsl.js`    | require define `Alphahash`    |
| worldPosition | 世界空间坐标  | vec4 | `worldpos_vertex.glsl.js` | require define `transmission` |
| vUv           | UV      |      | `uv_vertex.glsl.js`       |                               |
| objectNormal  | normal  |      | `beginnormal_vertex`      |                               |

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
// Add custom uniforms

	if (params.uniforms) {
		params.uniforms.forEach((uniform: Uniform) => {
		// unifrom class
			if (uniform.value instanceof THREE.Uniform) {
				// resolution: new Uniform( new Vector2() )
				shader.uniforms[uniform.name] = uniform.value;
			} else {
				// regualr value
				shader.uniforms[uniform.name] = { value: uniform.value };
			}
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
      `#include <dithering_fragment>\n
      ${params.fsInsertEndOfMain}`
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

### three-custom-shader-material Library
https://www.npmjs.com/package/three-custom-shader-material

```javascript
import CustomShaderMaterial from 'three-custom-shader-material/vanilla'
```

```javascript
// Material
const material = new CustomShaderMaterial({
    // CSM
    baseMaterial: THREE.MeshStandardMaterial,
    silent: true, // ignore the warning in the console

    // MeshStandardMaterial
    metalness: 0,
    roughness: 0.5,
    color: '#85d534',

	// uniforms
	uniforms: {
		uNoiseTexture: { value: noiseTexture },
	},
	
	// vs
	vertexShader: /* glsl */ `
		uniform sampler2D uNoiseTexture;
		void main()
		{
			float noiseColor = texture2D(uNoiseTexture, vec2(fract(csm_Position.x) * 0.03, fract(csm_Position.z) * 0.03)).r * 2.0 - 1.0;
			
			csm_Position.y += noiseColor;
		}
`,
})
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

## Fix

### Shadow

> The material used for the shadows is MeshDepthMaterial

```javascript
const depthMaterial = new THREE.MeshDepthMaterial({
    depthPacking: THREE.RGBADepthPacking
})

mesh.customDepthMaterial = depthMaterial
```

Modify depth material vertex shader
```javascript
depthMaterial.onBeforeCompile = (shader) =>
{
    shader.uniforms.uTime = customUniforms.uTime
    shader.vertexShader = shader.vertexShader.replace(
        '#include <common>',
        `
            #include <common>
			...
        `
    )
    shader.vertexShader = shader.vertexShader.replace(
        '#include <begin_vertex>',
        `
            #include <begin_vertex>
            ...
        `
    )
}
```

### Normal


### Test
```js
window.addEventListener('keydown', (e) => { 
	if (e.key === 'o') { 
		this.uniforms.uTransition.value -= 0.01 
		this.poiEntity.uniforms.uTransition.value -= 0.01 console.log('-', 
		this.uniforms.uTransition.value) 
	} 
	else if (e.key === 'p') { 
		this.uniforms.uTransition.value += 0.01 
		this.poiEntity.uniforms.uTransition.value += 0.01 console.log('+', 
		this.uniforms.uTransition.value) 
	} 
})
```