space to center view

### Node
[Node documentation](https://docs.quadspinner.com/Reference/GeoPrimitives/Mountain.html)

Gradient

Primitives
- Mountain
- Ridge
- range
- SlopeNoise

---

Erosion
- less volume, use shaper or clamp make bigger then erode smaller
- use erosion to fix seam
- output (optional, check Generate Masks)
	- wear - where most eroded
	- deposit - sediment
	- flow - river
![[gaea-erosion-enhance-view.gif]]

FractalTerraces

LookDev
- Shatter
- Canyonizer

Height
use height as mask to show shatter
![[gaea-height-mask.png]]

Mask
Manually painted mask

- Texture

Color
- QuickColor (Two Color)
- CLUTer (Gradient)
- SatMaps (Presets)

- sea
- river
- SnowFall
- aboreal - tree
---

- Combine - add
- Transform
	- rotation & move position

- Heal 
Low Res Satellite image 

Preview resolution
![[gaea-preview-resolution.png]]

drag to create node
![[gaea-drag-create-node.gif]]


rmb > pin
always show pinned node
pin as underlay

[Post Process Stack](https://docs.quadspinner.com/Guide/Using-Gaea/PostProcess.html)
also Fx node
- clamp
- shaper