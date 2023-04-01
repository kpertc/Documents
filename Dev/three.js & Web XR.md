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
```
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

##### Aniamtion

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

##### Orbit OrbitControls

```JavaScript
import { OrbitControls } from 'three/examples/jsm/controls/OrbitControls'

const controls = new OrbitControls( camera, renderer.domElement );
```

##### TransformControls

```JavaScript
import { TransformControls } from 'three/examples/jsm/controls/TransformControls.js';

const control = new TransformControls(camera, renderer.domElement)
// control.attach(_mesh)
```

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

##### Scene Background - CubeMap
[Convert equirectangular texture to cubemap](https://jaxry.github.io/panorama-to-cubemap/)

```JavaScript
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

  

### XR

Use WebXR emulator to develop: https://chrome.google.com/webstore/detail/webxr-api-emulator/mjddjgeghkdijejnciaefnkjmkafnnje

three.js VR setup: https://threejs.org/docs/#manual/en/introduction/How-to-create-VR-content


# Web XR API (Web XR)
[WebXR Device API](https://www.w3.org/TR/webxr/)
[WebXR Device API - Web APIs | MDN](https://developer.mozilla.org/en-US/docs/Web/API/WebXR_Device_API)

[[udemy] Learn to create WebXR, VR and AR, experiences using Three.JS](https://www.udemy.com/course/learn-webxr/)
[[YouTube] WebXR APIs and Examples](https://youtu.be/ypSkIYpJjE8)

A groups standard for immersive hardware, a wide range of devices. (VR, AR, handset, headset)
WebXR needs to work with WebGL based renderer, such as three.js

##### XRSystem and XRSession
Access WebXR API by XRmanager in renderer
`navigator` object, to check if XR is supported, is the entry point to WebXR
If WebXR is available, then it will have an xr property
Navigator.xr is an XRSystem interface

  

##### Gamepad API
-   Detecting button presses
-   Detecting Touchpad/Joystick Movement

[WebXR Gamepads Module - Level 1](https://www.w3.org/TR/webxr-gamepads-module-1/#xr-standard-heading)

Gamepad
```JavaScript
for ( const source of session.inputSources ) {
    if (source.gamepad) {
        // use gamepad information
    }
}
```

Hand
```undefined
for ( const source of session.inputSources ) {
    if (source.hand) {
        // use hand information
    }
}
```

![[xr-standard-controller.png]]

```JavaScript
inputSources = renderer.xr.getSession().inputSources[0]

// check button is pressed -> return true or false
inputSources.gamepad.buttons[4].pressed
inputSources.gamepad.buttons[5].pressed

// return -1 - 1
inputSources[0].gamepad.axes[3] // Left -1, right 1
inputSources[0].gamepad.axes[3] // Up 1, down -1
```

![[controller-event.png | 300]]

Events:
-   `connected`, `disconnect`
-   `selectedstart`, `selectedend`, `select` Tigger
-   `squeezestart`, `squeeze`, `squeeze` Grip Button

Input profile library
Library ?


WebXR Dom Overlay
Anchor
Layer

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