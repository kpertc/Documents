https://github.com/yomotsu/camera-controls?tab=readme-ov-file

``` js
// disable the camera control at first to control the native camera
cameraControl.enabled = false;
camera.position.x = 20;
```

Move Camera
```js
centralVariables.cameraControl.setLookAt(
	// camera position
	startPos.x,
	startPos.y,
	startPos.z,
	// look at
	0,
	0,
	0,
	// is smooth transition
	false
);
```

Camera Path
``` js

```