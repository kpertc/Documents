### Intro WebGPU
> https://www.youtube.com/watch?v=oIur9NATg-I
- access from graphic card (even not from an JS, browser, has C++ and Rust Application)
- wrapper native graphic API (Vulkan, DirectX, Metal)
- 2 - 8x faster than WebGL
- running computation on GPU 
- WebGPU → WGSL as shader language
---

Upate to WebGPU
require three ==r167+==, (update three and @types/three by `npm i three@latest`)
import webgpu module from three
``` ts
import * as THREEGPU from "three/webgpu";
import * as THREETSL from "three/tsl";
```

if can not resolve the "three/webgpu" or "three/tsl",  edit `tsconfig.json`, update `moduleResolution` to "bundler"
https://discourse.threejs.org/t/how-to-import-three-three-webgpu-js-when-using-vite/70618
```
"moduleResolution": "bundler"
```

---

Check WebGPU available
> [How to Create a Liquid Raymarching Scene Using Three.js Shading Language]( https://tympanus.net/codrops/2024/07/15/how-to-create-a-liquid-raymarching-scene-using-three-js-shading-language/)
``` js
import WebGPUCapabilities from 'three/examples/jsm/capabilities/WebGPU.js'
const webGPUAvailable = WebGPUCapabilities.isAvailable()

// set renderer
const renderer = new WebGPURenderer({
  canvas: canvas,
  antialias: true,
  alpha: true,
  forceWebGL: !webGPUAvailable,
})
```

---
### TSL - Three.js Shading Language

- support tree shake shader codef
[Three.js Shading Language Git Wiki](https://github.com/mrdoob/three.js/wiki/Three.js-Shading-Language)
https://threejs.org/playground/
Convert GLSL cod to TSL: → https://threejs.org/examples/?q=tsl#webgpu_tsl_transpiler
[three.js PhysicalLightingModel (TSL)](https://github.com/mrdoob/three.js/blob/9d4c2918ae86c67f079a8c7c2830551171f4a430/src/nodes/functions/PhysicalLightingModel.js#L131)

https://github.com/brunosimon/three.js-tsl-sandbox
https://boytchev.github.io/tsl-textures/
Nodes: https://github.com/mrdoob/three.js/blob/423f285d5d868dd128d6f143dc8ec31154018f57/src/nodes/Nodes.js#L42
``` ts
import { vec4, vec3, vec2, Fn, uv, uniform, normalLocal, mul, positionLocal, pass, overlay, refract, positionWorld, cameraPosition, normalize, length, screenUV, normalWorld, textureBicubic, negate, smoothstep, sin, cos, mat2, mat3, mat4, div, modelWorldMatrix, transformedNormalWorld, cameraProjectionMatrix, cameraViewMatrix, Loop, float, If, texture } from "three/tsl";
```

``` ts
const material = new NodeMaterial();

const material = new MeshPhysicalNodeMaterial({
	wireframe: true,
});

material.colorNode = vec4(1.0, 0.0, 0.0, 1.0); // equivalent to diffuse color 
material.outputNode = vec4(0.0, 1.0, 0.0, 1.0); // equivalent to gl_FragColor

material.colorNode = Fn(()=> {

	// condition and discard
	If(textureColor.r.greaterThan(0.2), () => {
		Discard();
	});
	
	return vec4(1,0,0,1)
})()
```
##### uv
`uv()`, `uv().x`, `uv().y`
```ts
material.colorNode = vec4(uv(), 0.0, 1.0); // equivalent to diffuse color
```
##### Texture
``` ts
const textureColor = texture(uTexture, uv());
material.colorNode = vec4(textureColor);
```
##### attribute
```ts
attribute(``)

const position = positionGeometry; // raw position
const normal = normalGeometry; // normal
// check
```

uniform
``` ts
uTime: uniform(0)

Fn(() => {
	return sin(_this.uTime));
})
```

Varying
``` js
const vNoise = varying(float());
const vPosition = varying(vec3());


const vertexFunc = Fn(() => {
	vColor.assign(positionGeometry);
});

const colorFunc = Fn(() => {
	return vec4(vColor.rgb, 1);
});
```

Node
``` ts
material.positionNode // positionLocal
material.scaleNode

material.geometryNode
material.normalNode

vertexNode
fragmentNode

material.colorNode
material.outputNode
```

Fn
> https://codepen.io/nik-lever/pen/MYgwXMJ?editors=0010
```ts
// with argument
const spherize = Fn(({ outputNormal }) => {
const sphereNormal = positionGeometry.normalize();
const pos = mix(positionGeometry, sphereNormal.mul(0.6), deltaUniform);
const norm = mix(normalGeometry, sphereNormal, deltaUniform);

	return select(outputNormal, norm, pos); // select -> ternay operation
});

material.positionNode = spherize({
	outputNormal: true
});
```

### React-Three-Fiber Setup
- https://github.com/verekia/r3f-webgpu/
renderAsync work around 
- https://github.com/pmndrs/react-three-fiber/issues/3403

https://codesandbox.io/p/sandbox/patient-lake-9sh577
``` tsx
// set to "never", and set to "always" when renderer init
const [frameloop, setFrameloop] = useState("never");

<Canvas
	frameloop={frameloop}
	gl={(canvas) => {
		const renderer = new WebGPURenderer({
			canvas,
			powerPreference: "high-performance",
			antialias: true,
			alpha: true,
		});
		renderer.init().then(() => setFrameloop("always"));
		renderer.xr = { addEventListener: () => {} };
		return renderer;
	}}
>
	...
</Canvas>
```


### WebGPU Inspector
https://chromewebstore.google.com/detail/webgpu-inspector/holcbbnljhkpkjkhgkagjkhhpeochfal?hl=en-US
https://github.com/brendan-duncan/webgpu_inspector