
## lil-gui

  https://lil-gui.georgealways.com

### Installation

[Installation](https://lil-gui.georgealways.com/#Guide#Installation)

```sh
$ npm install lil-gui --save-dev
```

```JavaScript
// three includes lil-gui
import GUI from 'three/examples/jsm/libs/lil-gui.module.min' // use lil-
gui
// or
import GUI from 'lil-gui';
```

```JavaScript
const gui = new GUI()
const gui = new GUI({ 
	title: "🐞 Debug GUI", 
	width: 300,
	closeFolders: true, // close all folders by default
});

gui.close() // close debug GUI
```

![[dat-gui.png | 300]]

```JavaScript
// the object, the property of the obejct
folder.add(mesh.position, 'x') // no min max will show float input
folder.add(mesh.rotation, 'x', 0 ,10)
folder.add(mesh.scale, 'x', 0 ,10)

gui.add(waterMaterial.uniforms.uColorOffset, 'value')
	.min(0)
	.max(1)
	.step(0.001)
	.name('uColorOffset') // rename

gui.add(mesh, 'visible')
gui.add(material, 'wireframe')
```

### Add Color

https://threejs-journey.com/lessons/raging-sea#

![[threejs-debugGUI-color.png|300]]

```js
gui.addColor(material, 'color')
	.onChange((value) => {
		console.log(value) // log out value
		console.log(value.getHexString()) // actual color in three.js
	}
```


``` ts
// create an object to store object
let debugObject = {
	color: "#0000ff",
};

...

// set shader uniform
const material = new ShaderMaterial({
	vertexShader: vertexShader,
	fragmentShader: fragmentShader,
	uniforms: {
		uColor: { value: new THREE.Color(debugObject.color) },
	},
});

...

// GUI
gui.addColor(debugObject, "color").onChange(() => {
	_mesh.material.uniforms.uColor.value.set(debugObject.color); // value is color, use .set()
	// _mesh.material.uniforms.uColor.value = new THREE.Color(debugObject.color);
}

```

### Function / Button

``` js
const testFunction = () =>  {}

// Funtion needs to in an object
let debugObject: any = {
	testFunction: () => {
		console.log("Hi");
	},
};

gui.add(debugObject, "testFunction");

gui.add({
	test: () => {
		console.log("test");
	},
},"test");
```

### Folder
Folders can be nested
```js
const folder = gui.addFolder('folderName')
folder.open()
folder.close()
```

### hide GUI
```js
gui.hide()

// use key to show / hide
window.addEventListener('keydown', (event) => {
	if(event.key == "x") gui.show(gui._hidden)
})
```

.onFinishedChange()

## stats.js

```js
import Stats from 'stats.js'

import Stats from 'three/examples/jsm/libs/stats.module'
```

```JavaScript
const stats = Stats()
document.body.appendChild(stats.dom)

stats.update();
```

