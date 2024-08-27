Environment: Vite + TypeScript + three.js + dat.gui (optional)

Official Website: https://threejs.org/
Editor: https://threejs.org/editor/
Installation: https://threejs.org/docs/index.html#manual/en/introduction/Installation

##### Tutorial
[Three.js + Vite + TypeScript](https://www.youtube.com/watch?v=7xjHM5N7LGQ)
##### Template
Github - Vite TS Template https://github.com/pachoclo/vite-threejs-ts-template

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

### ~~dat.gui~~ (use lil-gui)
~~Install dat.gui -> `npm install dat.gui --save-dev`
Install TypeScript type support -> `npm install @types/dat.gui --save-dev`
Import: `import { GUI } from 'dat.gui'`~~

check out ☞ [[three.js - Debug GUI]]

### Shader

> [!NOTE] VScode plugin `glsl-literal`
> Using `.glsl.js` file, get syntax highlight
Put `/* glsl */` to get syntax highlight

### Vite GLSL plugin setup
[npm - vite-plugin-glsl](https://www.npmjs.com/package/vite-plugin-glsl)

``` js
// install "vite-plugin-glsl"
import glsl from "vite-plugin-glsl";
...
plugins: [glsl()],
```

use `#include` with `vite-plugin-glsl` plugin
![[threejs-shader-vite-include.png]]


### Scene Inspector
Chrome Extension
##### Spector.js 
https://spector.babylonjs.com/

##### ThreeTools
https://three.tools/

new variables
`__THREE__`
`__THREE_DEVTOOLS__`
`__THREETOOLS__SCENES__`

##### Three-tools by BACE
https://github.com/oslabs-beta/BACE
