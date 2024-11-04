
### Tutorial
[[YouTube] Complete Beginners Guide by Grant Abbitt](https://www.youtube.com/watch?v=jnj2BL4chaQ&list=PLn3ukorJv4vuU3ILv3g3xnUyEGOQR-D8J&index=1)
  
---
### Important

##### Screen Cast Keys add-on → [[Screen Cast Keys addon]]
##### Online Manual
`RMB` to Blender online manual
![[online-manual.gif]]

##### Undo Steps
System > Memory & Limits
![[undo-steps.png]]

Find recovery files
![[recover-saves.png]]

##### `.blend1` file
backup file before save, open `.blend1` in Blender ↓
![[open-blend1.png|300]]

##### Save preferences
![[preferences.png]]

---
### History

Dutch animation studio NeoGeo
1998 first public release
Blender based Game Engine → [upbge.org](https://upbge.org/#/)

---
### Window Layout

Drag corner to start a new window|Tool Bar -> Press `T`|Sidebar Press `N`
---|---|---
![[img/Blender Basics/blenderDragCorner.gif]]|![[img/Blender Basics/T.gif]]|![[img/Blender Basics/N.gif \| 100]]
`Ctrl` + `Space` Full window

`Ctrl` + `MMB` UI Scale
![[control-MMB-scale.gif]]

---
### Editing Values
##### Edit Multiple Values
Drag|Type
---|---
![[edit-multiple-values.gif]]|![[edit-multiple-values-2.gif]]

##### Perform Calculation
![[calculate.gif]]

##### Hold `Shift` to slow
![[shift-to-slow.gif]]

##### Hold `Alt` to edit multiple object
![[hold-alt-edit-multiple-value.gif]]

---
### Selection

Last selected object → Active Object
Other selected object → Selected objects

![[img/Blender Basics/activeObject.gif]]

`A` Select all  
`A` + `A` De-selected All
`L` Select parts

`Ctrl` + `L` copy attribute from active object to selected objects
![[img/Blender Basics/copy-modifier.png | 300]]

Ctrl + (Numpad) +/-
![[ctrl-num+-.gif]]

`Shift G` select similar
![[select-similar.gif]]

---

### 3D Viewport

RMB > Assign Shortcut
![[img/Blender Basics/assign-shortcut.png | 200]]

Fly/Walk Navigation
`Shift ~` 
![[Fly-Walk-Navigation.gif]]

##### Rotation

[Everything You NEED to Know About How to Rotate Objects in Blender by Brandon's Drawings](https://youtu.be/8DbqvMOo_3s?si=-kk-_hjFGiO6aBlb)

`RX20`  rotate 20 degree along X-Axis|Axis(X, Y, Z) to toggle world/object space<br>Z (Global) Z (Local) Z (Unrestricted Axis)
---|---
![[RX20.gif]]|![[rotation-space.gif]]

`-`Reverse 45 degree
`RR` Free Rotation (3D)
`RMB` to cancel

Pivot Point Comparison
![[rotation-pivotpoint-comparison.gif]]

Active Object → yellow outline object

---

<div style="display: grid; grid-template-columns: repeat(3, 2fr); grid-gap: 10px;">
	<div>
		<code>1</code>Vertex<br>
		<code>2</code>Edge<br>
		<code>3</code>Face <br>
		<code>Shift</code> Multi-select<br>
		<br>
		<code>X</code>Delete<br>
		<code>H</code>Hide<br>
		<code>Alt</code>+<code>H</code>unHide
		<br>
		<br>
		<code>F2</code> Rename<br>
		<code>F3</code> Search<br>
		<br>
		Edit Mode<br>
		<code>Ctrl F</code> Face Menu<br>
		<code>Ctrl E</code> Edge Menu<br>
		<code>Ctrl V</code> Vertex Menu<br>
	</div> 
	<div> 
		<code>G</code> Move (Grab, Translation)<br>
		<code>R</code> Rotate<br>
		<code>S</code> Scale<br>
		then X Y Z to constrain Axis
		<br>
		<br>
		<code>Alt G</code> Clear Translation<br>
		<code>Alt R</code> Clear Rotation<br>
		<code>Alt S</code> Clear Scale<br>
		<br>
		 <code>Shift</code> +  <code>Space</code> then  <code>G</code> /  <code>R</code> /  <code>S</code> will show the gizmo
		<hr>
		Hold <code>Ctrl</code> Snap
		<br>
		<br>
		<code>Ctrl</code> / <code>Command</code> + <code>A</code> apply Transformation
		<br>
		<code>Alt</code> + <code>G</code> Clear Translation
	</div> 
	<div>
		<code>Shift</code> + <code>D</code> Duplicate<br>
		<code>Ctrl M</code> Mirror<br>
		<code>Ctrl L</code> Link<br>
		<br>
		<code>F12</code> Render<br>
		<code>Ctrl</code> + <code>F12</code> Animation Render
	</div> 
	</div>

[Blender Common Shortcuts](https://docs.blender.org/manual/en/latest/interface/keymap/introduction.html)
https://www.dummies.com/article/technology/software/animation-software/blender/blender-for-dummies-cheat-sheet-208646/

Alt + G: move to world origin
Alt + G / R / S
Clear Translation Rotation Scale
![[clear-translation-rotation-scale.gif]]

##### Outliner

`C` New Collection

`Numpad -` /` Numpad +` 
Fold/Unfold outliner
  

Turn on Emulate 3 Button Mouse

`Alt` + `LMB` Rotate
`Alt` + `Ctrl` + drag `LMB` Zoom

![[img/Blender Basics/Emulate 3 Button Mouse.png | 300]]

  

Quick Favorites `Q`|Preferences > Save Preferences to save
---|---
![[img/Blender Basics/quickFavorites.gif]]|![[img/Blender Basics/save-preference.png]]

  

##### Object Mode

`Shift` + `A` -> Add|`Shift` + `Space`|SideBar -> View -> Lock Camera to View
--|--|--
![[img/Blender Basics/add.png]]|![[cursor-menu.png]]|![[img/Blender Basics/camera-to-view.png]]
  

Redo Panel will show when added

![[img/Blender Basics/addCylindar.gif]]
  

Local View `/` - Hide other object

![[img/Blender Basics/localView.gif]]


##### Collection

`C` Create Collection at outliner

###### Move to Collection
![[move-to-collection.gif]]

###### Collection Instance
will not add too much memory (optimization!)
![[collection-instance.gif]]
  

##### Edit Mode

`Tab` to Switch between Object Mode / Edit Mode
Double `Left Mouse Button` / hold `Alt` Select loop

`1` / `2` / `3` Toggle Selection Mode
Hold `Shift` + `1` `2` `3` select multiple
![[img/Blender Basics/Activate Selection Mode.gif]]

`G` `G` / `Shift V` move vertex along edge

Faces loop selected that runs perpendicular to the edge selected
![[img/Blender Basics/SelectFaceLoop.gif]]

###### Extrude
`E` Extrude
`Alt + E` Extrude along normal
![[extrude-along-normal.gif]]
Spin Tool -> 3D Cursor as pivot point

###### Separate
`P` Separate
![[img/Blender Basics/Separate.png]]

###### Loop Cut
`⌘ + R` Loop Cut
Scroll wheel to change cuts #
![[loopcut.gif]]

###### Insert
`i` insert
`i` twice insert individual
![[i-twice.gif]]

###### Bevel
Ctrl B Bevel
Ctrl ⇧ B Bevel vertex

###### Knife
`K`

###### Merge
`M`
![[merge-to-single-vertex.gif]]

###### Create Face
`F`
![[create-face.gif]]

##### 3D Cursor / Pivot Point
-   The 3D Cursor is used as the origin for any added object
-   Pivot point or reference pos


Select 3D Cursor Icon

`Shift` + `RMB` move cursor|`Shift` + `S` Selection to Cursor
---|---
![[img/Blender Basics/cursor.png]]|![[img/Blender Basics/Selection to Cursor.png]]

`Shift RMB` Move 3D Cursor
`Shift C` Center 3D Cursor

Manually move 3D Cursor
Panel > View > 3D Cursor
![[3dcursor-manual.gif]]

<br>

Pivot Point Editing

Change object pivot point by 3D cursor|Manual Edit Tool > Options > Transform > Affect Only Origins
---|---
![[img/Blender Basics/changePivotPoint.gif]]|![[img/Blender Basics/manualEditPivotPoint.gif]]

---

### Show Statistics

Statistic → show face count

Show Statistic|Show Measurement (Edit Mode)
---|---|---
![[img/Blender Basics/showStatistic.gif]]|![[img/Blender Basics/Show Measurement (Edit Mode).png]]|![[img/Blender Basics/viewport-overlay.png \| 100]]

Show Statistic & Status bar
- Show global info in Object Mode
- Show object info in Edit Mode

![[status-bar.gif]]

Default status can be set at `Preferences > Interface > status Bar` and save the Preferences

---
### Camera
align camera to view
`Ctrl Alt Numpad0`
![[align-camera-to-viewport.png]]

Camera viewport
Look from camera: `View > Cameras > Active Camera`
Select the camera object, then select camera `data > Viewport Display`
![[camera-viewport.gif]]

##### Camera Path Animation
add to `Track To` constrain to "Look At" object
![[blender-camera-trackto.png]]

add `Follow Path` constrain, in order
![[blender-camera-followPath-TrackTo.png]]

Don't forget to make interpolation set to linear

---

### Parenting

The active (Yellow) object will be the parent; (red) objects are children

Object Property > Relations
![[img/Blender Basics/Relations.png | 500]]

Select object `RMB` > Parent
  Parent: 1. Select Object 2 select Amature `Ctrl` + `P`
  Unparent: Select object `Alt` + `P` unparent
  
Hold `Shift` in Outliner to change parenting|Use Add > Empty as parent for easy control
---|---
![[img/Blender Basics/moveInHierachy.gif]]|![[img/Blender Basics/modeling_empties_draw-types.png]]
  

### Learn more about [[Blender Rigging]]
---

### View Tips

##### Isolate view
`/`
![[isolate-view.gif]]

| `L` Selecting all connected vs `A` select all | Select Mirror                            |
| --------------------------------------------- | ---------------------------------------- |
| ![[img/Blender Basics/selectAll.gif]]         | ![[img/Blender Basics/selectMirror.gif]] |

Proportional Editing (Smooth Selection)|Mouse Scrolling / `Page Up` / `Page Down`
---|---
![[img/Blender Basics/porpotionalEditing.gif]]|![[img/Blender Basics/influence.gif]]

##### Edge Slide `Shift` + `V`

  

`Ctrl` + `Tab` Change Mode
![[img/Blender Basics/mode.gif]]

##### [Duplicate Linked](https://docs.blender.org/manual/en/latest/scene_layout/object/editing/duplicate_linked.html) (Instance)
![[duplicate-linked.gif]]

#####  viewport Display as wireframe
![[img/Blender Basics/viewportDisplay.gif]]

##### Snap to Face
![[snap-to-face.gif]]

##### viewport cavity

> Highlight ridges and valleys in the scene geometry.

![[viewport-cavity.gif]]

##### viewport color

![[img/Blender Basics/color-cubes.png]]|![[img/Blender Basics/random-shading.png \| 300]]
---|---

##### Hold `Alt` for Orthographic
![[alt-snap-orthoview.gif]]

##### `Ctrl C \ V` Copy cross blender instance
![[copy-cross-blender.gif]]

---
### [[Blender Curve]]
---

### Normal

Shading Smooth / Flat|AutoSmooth (when smooth shading)
---|---
![[img/Blender Basics/ShadingFlatSmooth.gif]]|![[img/Blender Basics/autoSmooth.gif]]
  
Show Normal (in Edit Mode)|Show Face Orientation
---|---
![[img/Blender Basics/showNormal.gif]]|![[img/Blender Basics/Show Face Orientation.gif]]
  

(Edit Mode) > Mesh > Normals > Flip
![[img/Blender Basics/FlipNormal 1.gif]]


---
### [[Blender Modifier]]

---

### Outliner

<span style="color: #9FDB1D">Hide in viewport</span>
<span style="color: #F53F3F">Disable in renderer</span><br>

![[img/Blender Basics/viewport-renderer-visibility.png | 300]]

---

### Material / Shader Editor

rename material
![[rename-material.png|200]]

Change World / Object|Assign Material
---|---|
![[img/Blender Basics/world.png]]|![[img/Blender Basics/assignMat.gif]]|

Create a duplicated material
![[duplicate-material.png|300]]

Drag to apply Material|Select / Deselect Material
---|---
![[drag-applyMaterial.gif]]|![[select-deselect-material.gif]]

Select different Material Output Node to view different output
![[select-view-different-materialoutput.gif]]

`Ctrl H`
![[collpase node.gif]]

Find nodes
`Ctrl F`
![[find-nodes.gif]]

Perlin Noise Texture
[Musgrave Texture Node](https://docs.blender.org/manual/en/latest/render/shader_nodes/textures/musgrave.html)

(UV Control)
Texture Coordinate → Mapping → Texture

- Mix (Color) Blending Mode
- Color Ramp

Math 

---

### Resources

### Fake User - 保存没有使用的资源

Data Block

https://brandonsdrawings.com/blender-data/

##### 0-No User
	- will be deleted if no user

Orphan Data
> When a data block is not being used in a Blender file at all, it is referred to as “Orphan Data.”

> `Purge` button will purge all orphan data that does not have a fake user assigned. This is how we delete unused data in Blender.

Blender will purge orphan data every time when close Blender

![[orphandata.gif]] | ![[orphandata-purge.jpeg]]
---|---

##### F-Fake user
	-  save for later

Delete Images Outliner > Blender File|Unpack all media file|Set Fake User at Outliner
---|---|---
![[img/Blender Basics/deleteResource.gif]]|![[img/Blender Basics/unpack-resource.png]]|![[add-fakeuser-outliner.png]]

1. Set Fake User 
2. Save Startup File
3. Faker User Data will show at new file

---

### Clean

To clean un-used texture …
![[clean-up.png]]

Remove unused slots (material)
![[remove-unused-slots.gif]]


---

### UV Editing

[[YouTube] UV Unwrapping Blender Tutorial by Edgar Allan Yee](https://www.youtube.com/watch?v=m4mas3bNO3s)

UV Sync Selection<br>Full UV will always show|Mark Seam<br>Clear Seam
---|---
![[img/Blender Basics/UV Sync Selection.gif]]|![[img/Blender Basics/Mark Seam.gif]]

  

Hold `Ctrl` / `Command` to select

![[img/Blender Basics/Ctrl.gif | 300]]

  

Press `U` UV Unwrap Menu

Choose a suitable Unwrap Method

![[img/Blender Basics/Unwrap Method-1.png]]|![[img/Blender Basics/U.gif]]|![[img/Blender Basics/Unwrap Method-3.png]]
--|--|--

![[unwrap.png|200]]

UV >
Pack Islands = Maya Layout
Average Islands Scale = uniform UV scale

![[img/Blender Basics/UV Menu.png | 200]]

  

Live Unwrap -> unwrap UV immediately after mark seam

![[img/Blender Basics/live-unwrap.png | 300]]
  

##### UV Grid Preview

Blender没有默认的UV网格预览功能，需要创建一个网格贴图，连到材质上

Create UV Grid Texture|Grid Texture connecting to Base Color of Material
---|---
![[img/Blender Basics/UV Grid.gif]]|![[img/Blender Basics/Show UV Grid Texture.gif]]
  

The material connects to `Texture Coordinate` > `Mapping` to scale

![[img/Blender Basics/Scaling.gif]]

---

### Texture Paint

Texture Paint Mode, set an image to paint|Change Brush
---|---
![[img/Blender Basics/set an image to paint.png]]|![[img/Blender Basics/Change Brush.png]]

  

| Paint Mask (selecting in edit mode)          | Texture stencil drawing                        |
| -------------------------------------------- | ---------------------------------------------- |
| ![[img/Blender Basics/texturePaintMask.gif]] | ![[img/Blender Basics/textureDrawStencil.gif]] |

`Shift` + `RMB` Scale

`Ctrl` / `Command` + `RMB` Rotation

---
### BlendShape

Shape Keys

![[img/Blender Basics/shapeKey.gif]]

BlendShape Symmetrize

Join BlendShape
![[blender-joinBlendShape.gif]]

---

### Sculpting

`LMB` add

`Ctrl` / `Command` remove

`Shift` Smooth

---

### Animation

| Keyframe                             | Auto-Keyframe                             |
| ------------------------------------ | ----------------------------------------- |
| ![[img/Blender Basics/keyframe.gif]] | ![[img/Blender Basics/Auto-keyframe.gif]] |

Animation Frame Rate

![[img/Blender Basics/framerate.png | 300]]

  

Animation Clips in Engine (Unity)

![[img/Blender Basics/animation-clip-1.png]]|![[img/Blender Basics/animation-clip-2.png]]|![[img/Blender Basics/animation-clip-3.png]]
--|--|--

---

### Anotation

`D` + `Left Mouse`
`D` + `Right Mouse`

Manage annotation / delete all -> SideBar -> View -> Annotations

---

### Render

`F12` Render

Slot for storing multiple render images

| ![[img/Blender Basics/render-slots.png\|400]] | ![[render-slot.png]] |
| --------------------------------------------- | -------------------- |

###### Render Background

Background Lighting
![[img/Blender Basics/background-lighting.png | 500]]

HDRI

only for viewport|actual render background
---|---
![[viewport-background.png]]|![[render-HDRI-background.png]]|

Hide HDRI background Render > Film > Transparent
See screenshot at [[Blender Basics#Shadow Catcher]]

###### Composition Guides

![[img/Blender Basics/composition-guides.png \| 300]]|![[img/Blender Basics/composition-guides-preview.png]]
---|---
  

###### Shadow Catcher

Enable Shadow Catcher on the object to be the shadow catcher|Check Film > Transparent
---|---
![[img/Blender Basics/enable-shadow-catcher.png]]|![[img/Blender Basics/turnon-transparent.png]]



Holdout

Turn on Hold out in Filter

![[img/Blender Basics/hold-out-1.png]]|![[img/Blender Basics/hold-out-2.png]]|![[img/Blender Basics/hold-out-3.png \| 100]]
--|--|--

Light Visibility
![[img/Blender Basics/ray-visibility.png | 300]]

###### Pass
Depth Map → Mist Pass
![[depth-map.png]]


Render Checklist

> [50+ Blender Tips and Tricks (that take even OG blender users by surprise!) by stache](https://www.youtube.com/watch?v=_hqCXI2vUa0)
Lens Distortion?
Blur the Final Render
Match White Point and Black Point
Flip Image for New Perspective
Draw Compositional Lines to check where the viewer's attention might go
Lens Dirt
Lens Flares
Bloom
Volumetric Cube
Break the Silhouette of Boring straight Lines in the render
Is the Camera at an angle where a real camera can actually be placed?
Squint Eye to Check Render's Focal Point
Try Textured Lights/Gobos/ES Lights
Normal map Decals on any model?
Triangle Composition where the Eye is dragged to the Pointed part of the triangle
People Like Being Rewarded when they Zoom in

---
### [[Blender Compositing]]

---

Export file format

[The Superior Alternative to PNG Renders by Polyfjord](https://www.youtube.com/watch?v=-UjJqwwMJc8)
![[img/Blender Basics/image-size-comparison.png]]

### Texture Baking

| Create an image texture                  | Switch to Cycles                | Select the texture image node and click 'Bake' |
| ---------------------------------------- | ------------------------------- | ---------------------------------------------- |
| ![[img/Blender Basics/texture-node.png]] | ![[blender-switchToCycles.png]] | ![[img/Blender Basics/bake.png]]               |

Bake Normal texture -> Color Space: Non-Color

---

### [[Blender Scripting Basics]]

---

### Assets Libraries

Preferences > File Paths > Asset Libraries

---
### Unreal Engine

### Driver Expression

add `#` before expression
![[expression.gif]]

```
frame

sin(frame)

radian(frame)
```

Export, Smoothing → Face

[[Unreal Engine Blender Addons]]

---
### Houdini

Scale down

![[img/Blender Basics/export-scale.png]]
  

##### Vertex Color

[[../Houdini/Houdini Basics]]

Blender|Houdini
---|---
![[img/Blender Basics/blender-vertex-color.png]]|![[img/Blender Basics/houdini-vertex-color.png]]

![[img/Blender Basics/blender-color-attributes.png]]

---

### 踩坑

-   导入骨骼方向不对-> Amature > Automatic Bone Orient
-   MegaScan Bridge Blender Plugin需要手动zip一下文件夹才能安装。Plugin位置在Bridge的资源文件夹。
-   Mixamo的Control Rig只能在Mixamo的骨骼上生效