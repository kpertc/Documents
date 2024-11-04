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
	    position: [-4, 3, 6] // set init position for camera
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

``` js
import { OrbitControls } from 'three/examples/jsm/controls/OrbitControls.js'

extend({ OrbitControls: OrbitControls })
extend( { OrbitControls }) // if same name
```

``` jsx
 <OrbitControls args={ [camera, gl.domElement] } /> // set argument
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

Load model
```jsx
import { useLoader } from '@react-three/fiber'
import { GLTFLoader } from 'three/examples/jsm/loaders/GLTFLoader.js'

// use useLoader to use three.js loader

// normal gltf model
const model = useLoader(GLTFLoader, './test.glb')

// gltf model require specific Loader
import { DRACOLoader } from 'three/examples/jsm/loaders/DRACOLoader.js'

const model = useLoader(
	GLTFLoader,
	'./test.glb',
	(loader) => {
		const dracoLoader = new DRACOLoader()
		dracoLoader.setDecoderPath('./draco/')
		loader.setDRACOLoader(dracoLoader)
	}
)

...

<primitive object={ model.scene } />
<Clone object={ model.scene } /> // instance?
```

[[React#`<Suspense />`]] Use `<Suspense />` to implement lazy loading

❮optimization❯ use meshBounds as raycast object
``` jsx
<mesh 
	raycast={ meshBounds }
>
```

```jsx
// mesh
<mesh
	castShadow
	receiveShadow
	position = { [1, 1, 1] }
	rotation-x = { 0.3 } 
	scale = { 0.2 }
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
##### Animation
```JavaScript
const animations = useAnimation(fox.animations, fox.scene)

useEffect(() => {
    const action = animations.actions.Run
    action.play()
},[])

// use levy to controll animation
```

play camera track frame
``` js
const { actions } = useAnimations(animations, group);

// levy ui to manual set animation value
const { _time } = useControls("Experience-Test", {
	_time: 0,
});

useEffect(() => {
	console.log(actions["CameraAction"]);
	actions["CameraAction"].play().paused = true;
}, []);

useFrame(() => {
	actions["CameraAction"].time = THREE.MathUtils.lerp(
		actions["CameraAction"].time,
		actions["CameraAction"].getClip().duration * _time,
		0.05
	);
});
```

blendshape / morph target
```js
morphTargetInfluences={[_time]}
```
##### Pointer Events
```JavaScript
// mouse -> right button click
// touchscreen -> long pressing
onContextMenu

onDoubleClick
onPointerUp
onPointerDown

// --- events on each frame, performance cost

onPointerOver
onPointerEnter

onPointerOut
onPointerLeave

onPointerMove // when hover on the object

// --- events on each frame, performance cost

onPointerMissed

// occluding
// on blocking object
event => {
    event.stopPropagation()
}
```

```
visible={false} can be detected
```

Change Cursor Style
```JavaScript
onPointerEnter={ () => { document.body.style.cursor = "pointer" } }
onPointerLeave={ () => { document.body.style.cursor = "default" } }
```

Shader Uniform with `useRef()`
``` js
// declare uniforms in the component
const uniformsRef = useRef({
	uTime: { value: 0 },
});

// update uniform value
useFrame(() => {
	uniformsRef.current.uTime.value = threeData.clock.getElapsedTime();
});

// use uniform in shader
const RGBmaterial = new THREE.ShaderMaterial({
	uniforms: {
		uTime: uniformsRef.current.uTime,
	},
	...
})
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
##### TransformControls
``` jsx
<TransformControls mode={"rotate"}>
	...
</TransformControls>
```

##### Load Texture
``` js
const texture = useTexture("./textures/key-decal.png");
```
##### Load Model
```JavaScript
import { useGLTF } from '@react-three/drei'

const model = useGLTF('./model.glb') // will load when the component is 

useGLTF.preload('./model.glb') // pre-load
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

useKeyboardControls
##### Merge
```js
export const MergeModel = (props) => {
	const { nodes, materials, scene } = useGLTF("./models/key.glb");
	return (
		<Merged
			castShadow
			receiveShadow
			meshes={[nodes.keycap, nodes.Key_Variation_contact]}
			{...props}
        >		
			{(Keycap, Key_Variation_contact) => (
				<>
					<Key_Variation_contact />
					<Keycap />
				</>
			)}
		</Merged>
	);
};
```
##### Instance
``` jsx
export const InstanceModel = () => {
const { nodes, materials, scene } = useGLTF("./models/key.glb");
	return (
		<Instances
			geometry={nodes.keycap.geometry}
			material={nodes.keycap.material}
     .  >				
			<Instance position={[[0, 0, 0]]} />
		</Instances>
	);
};
```
##### Decal
``` jsx
<mesh position={[0, 0, 0]}>
	<boxGeometry args={[1, 1, 1]} />
	<meshStandardMaterial color="lightgrey" />
	<Decal
		debug // debug mode
		position={[0, 0, 0.5]} // Decal position on the surface
		rotation={[0, 0, 0]} // Decal orientation
		scale={[0.5, 0.5, 0.5]} // Decal size
    >
		<meshStandardMaterial
			map={texture}
			color="white"
			polygonOffset
			polygonOffsetFactor={-1}
		/>
	</Decal>
</mesh>
```

### use Custom Shader Material
![[three.js - Shader#R3F]]

### Post-Processing

##### three.js → use `postprocessing` lib
![[three.js - Intro#Post-Processing]]

##### R3F → `React-postprocessing` lib

- Git: https://github.com/pmndrs/react-postprocessing
- Documentation: https://react-postprocessing.docs.pmnd.rs/introduction

```sh
npm i @react-three/postprocessing # will include a postprocessing lib
npm i postprocessing # install for referencing
```

```jsx
import { EffectComposer } from '@react-three/postprocessing'
import { ToneMappingMode } from 'postprocessing'

// ...

return <>
    <EffectComposer
        multisampling={8} // default is 8, 0 -> disable
    >
        <ToneMapping mode = {ToneMappingMode.ACES_FILMIC} />
        <Vignette />
    </EffectComposer>
</>
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

### Physics
original physics lib → `Rapier`
`React Three Rapier` by PMNDRS

Rapier: https://rapier.rs/

React Three Rapier
Git: [react-three-rapier](https://github.com/pmndrs/react-three-rapier)
Demos: https://react-three-rapier.pmnd.rs/

``` sh
npm i @react-three/rapier
```

```jsx
<Physics 
	debug
	gravity = {[0, -9.8, 0]}
>	
	<RigidBody
		type="fixed"
		// false
		colliders="ball" // 
		/*
			false → no colliders
			ball → sphere
			hull → convex hull
			trimesh → generated, trimesh is empty inside, could cause bug
		*/
>										
		<mesh>
	<RigidBody />
<Physics />
```

addForce
applyImpulse

gravityScale

InstancedMesh arges






使用 depth drawcall x2