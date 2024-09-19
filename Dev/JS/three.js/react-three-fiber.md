#web-dev 

react-three-fiber → R3F
- https://pmnd.rs/
- [[React]]
- [[Zustand]] state management

```tsx
import "./style.css";
import { createRoot } from "react-dom/client";
import { Canvas } from "@react-three/fiber";

// overwrite existing html body content
// document.body.innerHTML = '<div id="app"></div>';

const root = createRoot(document.getElementById("app"));
root.render(
  <>
    <Canvas>
      <mesh>
        <torusKnotGeometry />
        <meshNormalMaterial />
      </mesh>
    </Canvas>
  </>
);
```

`Scene`, `WebGLRenderer`, `PerspectiveCamera`, `Resize` are handled by default

```jsx
<mesh>
    <boxGeometry />
    <meshBasicMaterial color='red'>
</mesh>
```

`boxGeometry` will automatically attach to `mesh.geometry`
`meshBasicMaterial` will automatically attach to `mesh.material`
No need to specify attach=`geometry`

- Native elements → camelCase
- Custom components → PascalCase

> [!NOTE] Title
> R3F implements all classes automatically

### tips
##### Canvas

```jsx
<Canvas
	camera = { {
	    fov: 45,
	    near: 0.1,
	    far: 200,
	    position: [-4, 3, 6]
	} }
	
	// set init settings on `onCreated` callback
	onCreated = { e => {} }
	
	// enable shadow
	shadows // shadows = { true }
>
	...
<Canvas />
```

##### Scene background color
Assign color to scene background
The parent of `<color />` is "scene", so it can be attached to "scene.background"

```jsx
<color args={ ['#ff0000'] } attach='background'>
```

useHelper()

### `extend`
`extend` convert to declarative version
```js
 import { extend } from '@react-three/fiber'
```

### Hooks
##### useFrame
```jsx
const cubeRef = useRef()

// update
useFrame((state, delta) => {
	// cubeRef.current → native three.js object
    cubeRef.current.rotateion.y += 0.01

	// create sin movement
	const time = state.clock.elapsedTime
	cube.current.position.x = Math.sin(time)
})

return (
    <>
        <mesh ref={ cubeRef } ... >
    </>
)
```
##### useThree
```js
const { camera, gl } = useThree() // get camera and renderer from useThree()
```

### Elements
```jsx

// mesh
<mesh
	castShadow
	receiveShadow
>
	<meshStandardMaterial 
		color="red" 
		envMapIntensity = { 1 } // work with <Environment />
	/>
</mesh>

// lights
<directionalLight 
    position={ [1, 2, 3] }
    intensity={ 2 }
    castShadow // enable shadow
    shadow-mapSize // deeper properties using "-"
/>
```

### drei
Git Repo: https://github.com/pmndrs/drei
Documentation: https://drei.docs.pmnd.rs/getting-started/introduction
Storybook: https://drei.pmnd.rs/?path=/docs/staging-accumulativeshadows--docs

```sh
npm install @react-three/drei
```
##### OrbitControls
``` jsx
import { OrbitControls } from "@react-three/drei";
...
<OrbitControls />
```

```jsx
<RandomizedLight />
```
##### Shadows
###### BakeShadows
``` jsx
import { BakeShadows } from "@react-three/drei";
...
<BakeShadows /> // render shadow once, then use static shadow
```
###### Percent Closer Soft Shadows (PCSS)
`three.js` example: https://threejs.org/examples/?q=pcss#webgl_shadowmap_pcss
``` js
import { softShadows } from "@react-three/drei";

// run once, not in <></>
// will send params to shaders, and re-compile shaders
softShadows({
	...
})
```
###### AccumulativeShadow
``` jsx
<AccumulativeShadow /> // rendered on plane only, depended on three.js shadow
```
###### ContactShadow
on plane only, not depend on three.js shadow, and light, shadow camera recorded from below
```jsx
<ContactShadow />
<ContactShadow 
	frames={ 1 } // only render on the 1st frame -> baked
/>
```
##### Sky
```jsx
<Sky />

// set a directional light with same direction
<Sky sunPosition={ sunPosition } />
<directionalLight position={ sunPosition } castShadow>
```
##### Environment
``` jsx
// cubemap
<Environment
	files={ [
		'... px.jpg',
		'... nx.jpg',
		'... py.jpg',
		'... ny.jpg',
		'... pz.jpg',
		'... nz.jpg',
	] }
	background // show the texture as background
	ground = { ... } 

// HDRI
<Environment files={ './sky.hdr' } /> // use .hdr not .exr

// use presets
<Environment presets= "sunsets" /> // find names ↓ https://github.com/pmndrs/drei/blob/master/src/helpers/environment-assets.ts
```

Add custom lighting & elements in Environment by adding into `<Environment />`
``` jsx
<Environment>
	{/* <color /> to modify the default color of <Environment /> */}
	<color args={[ 'blue' ] attach="background" }>
	
	<mesh>
		<planeGeometry />
		<meshBasicMaterial color="red" />
		{/* color value can be set beyond 1.0 */}
		<meshBasicMaterial color={ [ 10, 0, 0 ] } />
	</mesh>
</ Environment>
```
###### LightFormer
``` jsx
<Environment> 
	<Lightformer 
		...
	/>
</ Environment> 
```
##### Stage
quickly setup environment, lighting, shadow ...
``` jsx
<Stage
	shadows={ { type: 'contact', opacity: 0.2, blur: 3 } }
	environment = "sunset"
	...
>
	<mesh>
</ Stage>
```

### Tools
React developer tool

##### Leva
https://github.com/pmndrs/leva
Debug UI
```shell
npm i leva
```

``` js
const { color, opacity, position } = useControls('group-name', {
	color: "#000000", // color
	opacity: { value: 0.5, min: 0, max: 1}, // slider
	position: { value: [ 1, 2, 3] } // vec3
})
```

##### r3f-perf
https://www.npmjs.com/package/r3f-perf/v/1.0.0-beta

``` sh
npm i r3f-perf
```

```js
import { Perf } from "r3f-perf";
```

add into `<Canvas>`
``` jsx
<Canvas>
	...
	<Perf />
	<Perf position="top-left" />
	...
</Canvas>
```