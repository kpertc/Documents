#VR 

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