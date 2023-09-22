
Project Setting
- Disable Auto Exposure
- Hardware Ray Tracing
	- Support Hardware Ray Tracing
	- Path Tracing

### Post Process
firefly
post process > max path exposure → 1.0 - 3.0
Translucency > Ray Tracing

### HDRI Backdrop
.HDR format, not .EXR
set to Camera projection
cube map resolution

### Movie Render Queue
Plugins to enable:
- Movie Render Queue
- Movie Render Queue Additional Render Passes

Window > Cinematics > Movie Render Queue

### Variant Manager
Plugins to enable:
- Variant Manager
- Variant Manager Content
![[level-variant-sets.png]]

Switch Actor

### Volume 
ExponentialHeightFog
- Check Volumetric Fog


### Light Channel
Light Channel
Every object has default Channel 0
set Cube Channel 1

![[lightchannel-pointlight.png]]|![[lightchannel-cube.png]]
---|---

### Color Calibrator
1. Show Engine Content
2. Engine > Content > EditorMeshes > Color Calibrator
![[color-calibrator.png]]