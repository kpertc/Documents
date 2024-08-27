#JavaScript #TypeScript #CG 
### [Basic Setup](https://threejs.org/docs/#manual/en/introduction/Creating-a-scene)

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

### Renderer

```js
this.renderer = new THREE.WebGLRenderer({
	canvas: this.canvas,
	antialias: true, // MSAA mix the edge pixel, but not to fix shape inside
	// use clear color ↓
	alpha: true,
});

// set pixel density, for example, retina screen have twice pixel
renderer.setPixelRatio(Math.min(window.devicePixelRatio, 2));

// set toneMapping
this.renderer.toneMapping = THREE.ReinhardToneMapping;
this.renderer.toneMappingExposure = 2.0;
```

![[window#Get Device Pixel Ratio]]

``` js
renderer.info
```

use renderer to render render texture → [[three.js - API#Render Texture]]
### Mesh

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

Rotate the geometry, not mesh
```JavaScript
const geometry = new THREE.PlaneGeometry()
geometry.rotateX(- Math.PI * 0.5) // preferred rotate on geometry
const mesh = new Mesh(geometry, material)
// mesh.rotateX(- Math.PI * 0.5)
```
##### Geometry
##### Manually Create Buffer Geometry
```js
const bufferGeometry = new BufferGeometry()

const positionArray = new Float32Array([
	0.0, 0.0, 0.0, // 0
	0.0, 0.0, 1.0, // 1
	1.0, 0.0, 1.0, // 2
	1.0, 0.0, 0.0, // 3
])

// clockwise
const indices = [
	0, 1, 2,
	2, 3, 0,
];

bufferGeometry.setAttribute('position', new BufferAttribute(positionArray, 3))
bufferGeometry.setIndex(indices)

const _mesh = new Mesh(bufferGeometry, cubeMaterial)

scene.add(_mesh)
```

Convert JS array to `Float32Array`
```js
const JSArray = [0, 1, 2, 3 ...]
const float32Array = new Float32Array(JSArray);
```
#####  Camera Space Plane
draw in front of camera
``` js
const overlayGeometry = new PlaneGeometry(2, 2, 1, 1); // -1 to +1 space, so is 2
const overlayMaterial = new ShaderMaterial({
vertexShader: /* glsl */ `
	varying vec2 vUv;
	void main()
	{
		vUv = uv;
		gl_Position = vec4(position, 1.0); // screen space
	}
`,
fragmentShader: /* glsl */ `
	varying vec2 vUv;
	void main()
	{
		gl_FragColor = vec4(uUv, 0.0, 1.0);
	}
`,
});

const overlay = new Mesh(overlayGeometry, overlayMaterial);
scene.add(overlay);
```
##### update matrix
threejs only updates matrixs when needed at once. The matrix of objects that are not in the scene will not be updated. Need to use `.updateMatrix()` manually.
##### Line
![[threejs-line.png|200]]
[threejs-Drawing lines](https://threejs.org/docs/index.html?q=line#manual/en/introduction/Drawing-lines)
```js
// line position data
const linePositionArray: Vector3[] = [
	new Vector3(-1, 0, 0),
	new Vector3(0, 0, 1),
	new Vector3(1, 0, 0)
]

// line mesh
const lineGometry = new BufferGeometry().setFromPoints(linePositionArray);
const lineMaterial = new LineBasicMaterial({ color: 0xffffff });
const lineMesh = new Line(lineGometry, lineMaterial);
scene.add(line);
```
##### Material
```js
material.color.set('red')
```

vertex info preserves material info, `clear group` and apply material to all face
```js
console.log(_mesh.geometry,groups)

// clear group (if so) and apply material
mesh.geometry.clearGroups()
```

### Light

Directional Light
```JavaScript
const light = new THREE.DirectionalLigh(0xffffff, 1)
scene.add(light)
```

```JavaScript
// set directional directional light target
directionalLight.target.position.set(0, 4, 0)
directionalLight.target.updateWorldMatrix() // directionalLight.target is not in the scene, so have to manual update its matrix

// add camera helper for directional light shadow camera
const directionalLightHelper = new THREE.CamaraHelper(directionalLight.shadow.camera)
scene.add(directionalLightHelper)
```

Shadow
```js
// tweat shadow by tweating the shadow camera
directionalLight.castShadow = true
directionalLight.shadow.camera.far = 15 // manually set shadow distance

// fight shadow acne
directionalLight.shadow.bias
directionalLight.shadow.normalBias
```

### Animation
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

// flipY
_texture.flipY
```

> [!TIP] For mipmap
> Keep resolution of texture size of a power of 2

##### Render Texture
https://threejs.org/docs/#api/en/renderers/WebGLRenderTarget

Render Texture → WebGLRenderTarget
``` js
// create RT / WebGLRenderTarget
let renderTarget = new WebGLRenderTarget(256, 256, {});

// shader, set WebGLRenderTarget.texture to uniform 
let uniforms = {
	uTexture: new Uniform(renderTarget.texture),
};

renderer.setRenderTarget(renderTarget); // set renderer's output to renderTarget
renderer.render(_scene, camera); // render
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

// prevent orbitControl move
control.addEventListener("dragging-changed", function (event) {
	cameraControls.enabled = !event.value;
});

scene.add(control);
// attach to an object
control.attach(cube);
```

### Helpers
##### [AxisHelper](https://threejs.org/docs/#api/en/helpers/AxesHelper)
![[axis-helper.png | 300]]
```JavaScript
_mesh.add( new THREE.AxesHelper( 5 ) );
```

##### [GridHelper](https://threejs.org/docs/#api/en/helpers/GridHelper)
![[grid-helper.png | 300]]
```JavaScript
scene.add( new THREE.GridHelper( 10, 2) );
```

##### [PolarGridHelper](https://threejs.org/docs/#api/en/helpers/PolarGridHelper)

### Scene Background
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

// blur the background
scene.backgroundBlurriness = 0.2
```

> [!TIP] Add a directional light for environment light
> add a directional light that roughly match the direction of light in environment light

##### Realtime Reflection
``` ts
// hide -y axis blocking objects
this.car.showCar(false);

// at mirrored position
cubeCamera.position.copy(
	new THREE.vector3(
		camera.position.x, 
		- camera.position.y, 
		camera.position.z
	)
);

// record image
this.cubeCamera.update(this.renderer, this.scene);

// then show all objects
this.car.showCar(true);
```

### Raycaster
https://threejs.org/docs/#api/en/core/Raycaster

Use Raycaster on different canvas
```JavaScript
const canvasRect = _canvas.getBoundingClientRect() // get rect position

_canvas.addEventListener('pointmove', (event) => {
    const canvasX = event.clientX - canvasRect.left
    const canvasY = event.clientY - canvasRect.top
    this.raycasterPointer.x = (canvasX / _canvas.clientWidth) * 2 - 1
    this.raycasterPointer.y = -(canvasY / _canvas.clientWidth) * 2 - 1
})
```

### Window Resize

```JavaScript
window.addEventListener('resize', onWindowResize, false);

function onWindowResize() {
    camera.aspect = window.innerWidth / window.innerHeight;
    camera.updateProjectionMatrix();
    renderer.setSize(window.innerWidth, window.innerHeight);
}
```

### Time

``` ts
const elapsedTime = clock.getElapsedTime()
```
##### Delta time
```JavaScript
let oldElapsedTime = 0

// ...

const elapsedTime = clock.getElapsedTime()
const deltaTime = elapsedTime - oldElapsedTime
oldElapsedTime = elapsedTime
```

### Add vs Attach

Attach: maintaining the object's world transform.

### Remove

clean the mesh
``` js
geometry.dispose()
material.dispose()
scene.remove(_object)
```

[three.js - How to dispose of objects](https://threejs.org/docs/#manual/en/introduction/How-to-dispose-of-objects)

### Post-Processing ☞ EffectComposer

[three.js-EffectComposer](https://threejs.org/docs/#examples/en/postprocessing/EffectComposer)

``` js
import { EffectComposer } from 'three/addons/postprocessing/EffectComposer.js';
import { RenderPass } from "three/examples/jsm/postprocessing/RenderPass.js";
```

```JavaScript
// after renderer
const effectComposer = new EffectComposer(renderer)

const renderPass = new RenderPass(scene, camera) effectComposer.addPass(renderPass)

// add other passes
const dotScreenPass = new DotScreenPass();
effectComposer.addPass(dotScreenPass);
// disable the pass
// dotScreenPass.enabled = false;

// some passes are shader pass, to add shader a pass
const rgbShiftShader = new ShaderPass(RGBShiftShader);
effectComposer.addPass(rgbShiftShader);
```

in update, remove `renderer.render()`, use `effectComposer.render()`
```js
// renderer.render(scene, camera);
effectComposer.render();
```

update `effectcomposer` size when browser size changes
```js
window.addEventListener('resize', () => { 
	size.width = window.innerWidth 
	size.height = window.innerHeight 
	
	...
	
	renderer.setSize(size.width, size.height) 
	renderer.setPixelRatio(Math.min(window.devicePixelRatio, 2)) 
	
	effectComposer.setSize(size.width, size.height) 
	effectComposer.setPixelRatio(Math.min(window.devicePixelRatio, 2)) 
})
```
---
Other effects
```javascript
import { DotScreenPass } from 'three/examples/jsm/postprocessing/DotScreenPass.js'
```

if the effect is dark, which means colorspace is incorrect, then use `GammaCorrectShader`

```

```

renderer's Antialiasing i
##### Custom Shader Pass
[[three.js - Shader#Post Process Shader]]


### Math

JavaScript Math → [[Math (JavaScript)]]
##### Vector3
```js
// clone to avoid modify original value
direction.clone().cross(this.y);

// vector substraction
position.clone().sub(this.lastSeg.position)
```

Spherical Coord
```JavaScript
const sphericalCoord = new THREE.Spherical(
    radius,
    Math.random() * Math.PI,
    Math.random() * Math.PI
)

const position = new THREE.Vector3().setFromSpherical(sphericalCoord)
```


### Control by Scrolling in Browser

Camera fov is vertical based ➝ Objects' vertical position always stay when window resize

![[window#Scroll]]

``` js
// to get sreen base size scrolling
camera.position.y = - scrollY / window.innerHeight * objectDistance
// vertical distance between each object
```