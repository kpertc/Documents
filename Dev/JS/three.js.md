#JavaScript #TypeScript #VR 

# Other WebGL based renderer
-   Babylon.js
-   A-Frame (three.js based)
-   React - 360
-   PlayCanvas (WebGL game engine)

# Environment Setup
Environment: Vite + TypeScript + three.js + dat.gui (optional)

Official Website: https://threejs.org/
Editor: https://threejs.org/editor/
Installation: https://threejs.org/docs/index.html#manual/en/introduction/Installation

##### Tutorial
[Three.js + Vite + TypeScript](https://www.youtube.com/watch?v=7xjHM5N7LGQ)

##### Online playground
[codepen.io](https://codepen.io/tompeham/pen/ZWomey)
https://playcode.io/three_js/
https://stemkoski.github.io/Three.js/

Many cool examples:
https://hofk.de/main/discourse.threejs/

### Use Vite to initiate a project
Require: Node.js installation
Initialize a project: `npm init vite`
`npm install` - to install packages in package.json
`n``pm run dev` - host server & preview the website

![[vite-setting1.png | 300]]
![[vite-setting2.png | 300]]

Vite Config file
file name `vite.config.js`
``` js
// vite.config.js
import { defineConfig } from 'vite';

export default defineConfig({
    server: {
        host: '0.0.0.0',
        https: true
    }
})
```

Install three.js `npm install --save three`

### TypeScript Part
Check TypeScript installed: `tsc --version`
Convert TypeScript to JavaScript `tsc name.tx`
`npm install --save @types/three`

### dat.gui
Install dat.gui -> `npm install dat.gui --save-dev`
Install TypeScript type support -> `npm install @types/dat.gui --save-dev`
Import: `import { GUI } from 'dat.gui'`

### Recommend:
three.js Chrome extension: https://chrome.google.com/webstore/detail/threejs-developer-tools/ebpnegggocnnhleeicgljbedjkganaek

## Tween [[Tween.js]]

# Three.js

##### [Basic Setup](https://threejs.org/docs/#manual/en/introduction/Creating-a-scene)

```JavaScript
import * as THREE from 'three';

var scene = new THREE.Scene();
var camera = new THREE.PerspectiveCamera( 50, innerWidth/innerHeight, 0.1, 1000 );
var renderer = new THREE.WebGLRenderer();
renderer.setSize(window.innerWidth, window.innerHeight); // Fullscreen
renderer.setPixelRatio(devicePixelRatio)
camera.position.z = 5; // Move Camea Back

renderer.render(scene, camera);
document.body.appendChild( renderer.domElement );
```

document -> content in the `<HTML>`

[Color](https://threejs.org/docs/#api/en/math/Color), [MeshBasicMaterial – three.js docs](https://threejs.org/docs/?q=MeshBasicMaterial#api/en/materials/MeshBasicMaterial)

##### Mesh

```JavaScript
// Create scene Object
const boxGeometry = new THREE.BoxGeometry(1,1,1);
const material = new THREE.MeshBasicMaterial({color: 0x00ff00});
const mesh = new THREE.Mesh(boxGeometry, material);
scene.add(mesh);

const material = new THREE.MeshBasicMaterial({color: 0x00ff00, side: THREE.doubleSide});
```

```JavaScript
mesh.position.set(x, y, z);
mesh.scale.set();
```

##### Light

```JavaScript
const light = new THREE.DirectionalLigh(0xffffff, 1)
scene.add(light)
```

##### Animation

```JavaScript
function animate() {
    requestAnimationFrame( animate );
    // Update()
    renderer.render( scene, camera );
}

animate();
```

```JavaScript
function Update() {
    mesh.rotation.x += 0.01;
    mesh.rotation.y += 0.01;
}
```

### Texture

##### Loader
```ts
static loadTexture(url: string): Promise<THREE.Texture> {
	return new Promise((resolve, reject) => {
		const loader = new THREE.TextureLoader();
		loader.load(url, resolve, undefined, reject);
	}
);
```

##### settings
```ts
// set wrap mode
_texture_.wrapS = THREE.RepeatWrapping;
_texture_.wrapT = THREE.RepeatWrapping;

// set repeat scale
normalTextureRes.repeat.set(uvScale, uvScale);
```

### Orbit OrbitControls

```JavaScript
import { OrbitControls } from 'three/examples/jsm/controls/OrbitControls'

const controls = new OrbitControls( camera, renderer.domElement );
```

### TransformControls

```JavaScript
import { TransformControls } from 'three/examples/jsm/controls/TransformControls.js';

const control = new TransformControls(camera, renderer.domElement)
// control.attach(_mesh)
```

### [AxisHelper](https://threejs.org/docs/#api/en/helpers/AxesHelper)
![[axis-helper.png | 300]]
```JavaScript
_mesh.add( new THREE.AxesHelper( 5 ) );
```

### [GridHelper](https://threejs.org/docs/#api/en/helpers/GridHelper)
![[grid-helper.png | 300]]
```JavaScript
scene.add( new THREE.GridHelper( 10, 2) );
```

### [PolarGridHelper](https://threejs.org/docs/#api/en/helpers/PolarGridHelper)

### Scene Background - CubeMap
[Convert equirectangular texture to cubemap](https://jaxry.github.io/panorama-to-cubemap/)

```JavaScript
// load cubemap
const CubeTextureLoader = new THREE.CubeTextureLoader();
const Cubetexture = CubeTextureLoader.load([
  'px.png',
  'nx.png',
  'py.png',
  'ny.png',
  'pz.png',
  'nz.png',
]);
scene.background = Cubetexture;

// load Equirectangular .hdr file
new RGBELoader().setPath("/").load("harvest_1k.hdr", (texture) => {
	texture.mapping = THREE.EquirectangularReflectionMapping;
	scene.environment = texture;
});

// "Realtime Reflection"
cubeCamera.position.copy(
	new THREE.vector3(
		camera.position.x, 
		- camera.position.y, 
		camera.position.z
	)
);
```

##### Window Resize

```JavaScript
window.addEventListener('resize', onWindowResize, false);

function onWindowResize() {
    camera.aspect = window.innerWidth / window.innerHeight;
    camera.updateProjectionMatrix();
    renderer.setSize(window.innerWidth, window.innerHeight);
}
```

##### Add vs Attach

Attach: maintaining the object's world transform.
  
### dat.gui / lil-gui

Tutorial

-   [dat.GUI API](https://github.com/dataarts/dat.gui/blob/master/API.md)
      https://lil-gui.georgealways.com
-   [手把手教你使用dat.gui](https://zhuanlan.zhihu.com/p/47752059)
-   [Dat.gui 使用教程 - 小牛仔太棒棒 - 博客园](https://www.cnblogs.com/xiaoniuzai/p/6685556.html)

```JavaScript
import { GUI } from 'dat.gui' // use dat,gui
import { GUI } from 'three/examples/jsm/libs/lil-gui.module.min.js' // use lil-gui
```

```JavaScript
const gui = new GUI()
const folder = gui.addFolder('folderName')

folder.open()
```

![[dat-gui.png | 300]]

```JavaScript
folder.add(mesh.position, 'x') // no min max will show float input
folder.add(mesh.rotation, 'x', 0 ,10)
folder.add(mesh.scale, 'x', 0 ,10)
```


### Stats
```JavaScript
import Stats from 'three/examples/jsm/libs/stats.module'

const stats = Stats()
document.body.appendChild(stats.dom)

stats.update();
```

Module: a file that exports some code
Treeshakable: import what you need shake off the rest

### Using three.js with [[Web XR]]

## Custom shader

[ShaderMaterial](https://threejs.org/docs/#api/en/materials/ShaderMaterial)

### File
	↳ `vertex.glsl`
	↳ `fragment.glsl`

GLSL code in `glsl.js` file

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

### ShaderMaterial in three.js

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
```OpenGL
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