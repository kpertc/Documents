#JavaScript #TypeScript #VR 

### Other WebGL based renderer
-   Babylon.js
-   A-Frame (three.js based)
-   React - 360
-   PlayCanvas (WebGL game engine)

### Related Topics:
- [[three.js - Setup]]
- [[three.js - Shader]]
- [[Tween.js]]

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

### Light
```JavaScript
const light = new THREE.DirectionalLigh(0xffffff, 1)
scene.add(light)
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
```

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

### Window Resize

```JavaScript
window.addEventListener('resize', onWindowResize, false);

function onWindowResize() {
    camera.aspect = window.innerWidth / window.innerHeight;
    camera.updateProjectionMatrix();
    renderer.setSize(window.innerWidth, window.innerHeight);
}
```

### Add vs Attach

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