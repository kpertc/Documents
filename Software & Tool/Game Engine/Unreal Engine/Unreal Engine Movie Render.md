
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

---
### OCIO Settings 
Color pipeline

[Unreal to Davinci Resolve Workflow - ACES & sRGB by William Faucher](https://youtu.be/Bo3BvhGdaUo?si=s84bbiCbsnwq9P-a)

> [!NOTE] Workflow
> Unreal Engine Movie Render Queue → Davinci Resolve color grading

> [!info]
OCIO, OpenColorIO → Color Dictionary 
Repo: [https://github.com/colour-science/OpenColorIO-Configs/tree/feature/aces-1.2-config](https://github.com/colour-science/OpenColorIO-Configs/tree/feature/aces-1.2-config)

##### Unreal Engine

Create a ==OpenColor Configuration== in content browser

RMB > Miscellaneous > OpenColor Configuration

- set config file
- color space
    - Utility - Linear - sRGB
    - ACEScg

Movie Render Queue

- Color Output
    - OCIO Configuration
        
        - is Enable ✓
        - ==Configuration file==
        - Source Color Space - Utility - Linear - sRGB
        - Destination Color Space ACES - ACEScg
    - Disable Tone Curve (To get full range image data)

##### DaVinci Resolve

Project Settings
Set ACES
File > Project Settings > Color Management > 
- Color science > ACEScct
- ACES version > ACES 1.2
- ACES Output Transform > Rec.709

RMB on image sequence media
ACES Input Transform > Color Space Conversion > ACEScct - CSC 
sRGB Linear if not set to ACES in unreal

---

Alt-s Create New Corrector Node
Ctrl D Disable/Enable Node

Lift: Mainly Shadows/Blacks
Gamma: Midtones/Exposure
Gain: Highlights/Whites
Offsets: Shifts the values evenly

Effects:
- Curve
- Glow (Bloom)
- Aperture Diffraction (Paid)
- Mask
- Chrome Aberration (Layer mixer)
	- Only in high contrast area
- film grain (Paid)
- Vignetting
- Lens Flare

### Cinematic
- Framerate
- 24 fps → Motion Blur 18 Shutter

##### FOV
Filmback → Sensor size
↑ (Bigger) Film back  ↑ (Wider) FOV
↑ (Closer) to the object ↑ More Blur of the background

Aperture
