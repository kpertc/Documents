
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

### TSL - Three.js Shading Language

[Three.js Shading Language Git Wiki](https://github.com/mrdoob/three.js/wiki/Three.js-Shading-Language)
https://threejs.org/playground/
Convert GLSL cod to TSL: → https://threejs.org/examples/?q=tsl#webgpu_tsl_transpiler

``` ts
import { attribute, texture, vec4, uv } from "three/tsl";
```

``` ts
const material = new NodeMaterial();

const material = new MeshPhysicalNodeMaterial({
	wireframe: true,
});

material.colorNode = vec4(1.0, 0.0, 0.0, 1.0); // equivalent to diffuse color 
material.outputNode = vec4(0.0, 1.0, 0.0, 1.0); // equivalent to gl_FragColor

material.colorNode = Fn(()=> {
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
```

### React-Three-Fiber Setup
- https://github.com/verekia/r3f-webgpu/
renderAsync work around 
- https://github.com/pmndrs/react-three-fiber/issues/3403

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