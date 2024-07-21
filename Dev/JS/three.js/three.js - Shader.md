
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
``` js
// install "vite-plugin-glsl"
import glsl from "vite-plugin-glsl";
...
plugins: [glsl()],
```

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
### Shader → [[OpenGL]]

Write Shader

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

// Vertex shader[[
]]const vertexShader = /* glsl */ `
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