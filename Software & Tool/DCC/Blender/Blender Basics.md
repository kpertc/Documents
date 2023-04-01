
[[Blender Modifier]]


### Tutorial
[[YouTube] Complete Beginners Guide by Grant Abbitt](https://www.youtube.com/watch?v=jnj2BL4chaQ&list=PLn3ukorJv4vuU3ILv3g3xnUyEGOQR-D8J&index=1)

##### Screen Cast Keys addon → [[Screen Cast Keys addon]]
  
---

### History

Dutch animation studio NeoGeo
1998 first public release
[upbge.org](https://upbge.org/#/)
---

  

### Window Layout

Drag corner to start a new window|Tool Bar -> Press `T`|Sidebar Press `N`
---|---|---
![[img/Blender Basics/blenderDragCorner.gif]]|![[img/Blender Basics/T.gif]]|![[img/Blender Basics/N.gif \| 100]]
`Ctrl` + `Space` Full window

---

### Selection

Last selected object -> Active Object

Other selected object -> Selected objects

![[img/Blender Basics/activeObject.gif]]|

`Ctrl` + `L` copy attribute from active object to selected objects
![[img/Blender Basics/copy-modifier.png | 300]]

---

### 3D Viewport

RMB > Assign Shortcut
![[img/Blender Basics/assign-shortcut.png | 200]]

<div style="display: grid; grid-template-columns: repeat(3, 2fr); grid-gap: 10px;">
	<div>
		<code>1</code>Vertex<br>
		<code>2</code>Edge<br>
		<code>3</code>Face <br>
		<code>Shift</code>Multi-select<br>
		<br>
		<code>X</code>Delete<br>
		<code>H</code>Hide<br>
		<code>Alt</code>+<code>H</code>unHide
	</div> 
	<div> 
		<code>G</code>Move (Grab, Translate)<br>
		<code>R</code>Rotate<br>
		then X Y Z to constrain Axis
		<br>
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
		Select<br>
		<code>A</code> Select all<br>
		<code>A</code> + <code>A</code> De-selected All<br>
		<code>Shift</code> + <code>D</code> Duplicate<br>
		<br>
		<code>F12</code> Render<br>
		<code>Ctrl</code> + <code>F12</code> Animation Render
	</div> 
	</div>

Extra

![[img/Blender Basics/color-cubes.png]]|![[img/Blender Basics/random-shading.png \| 300]]
---|---


##### Outliner

`C` New Collection

  

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
![[img/Blender Basics/add.png]]|![[img/Blender Basics/cursor-menu.png]]|![[img/Blender Basics/camera-to-view.png]]
  

Redo Panel will show when added

![[img/Blender Basics/addCylindar.gif]]
  

Local View `/` - Hide other object

![[img/Blender Basics/localView.gif]]
  

##### Edit Mode

`Tab` to Switch between Object Mode / Edit Mode
Double `Left Mouse Button` / hold `Alt` Select loop

`1` / `2` / `3` Toggle Selection Mode
Hold `Shift` + `1` `2` `3` select multiple
![[img/Blender Basics/Activate Selection Mode.gif]]

Faces loop selected that runs perpendicular to the edge selected
![[img/Blender Basics/SelectFaceLoop.gif]]


`E` Extrude

`P` Separate
![[img/Blender Basics/Separate.png]]
  

##### 3D Cursor / Pivot Point

-   The 3D Cursor is used as the origin for any added object
    
-   Pivot point or reference pos

  

Select 3D Cursor Icon

`Shift` + 🖱️`Left` move cursor|`Shift` + `S` Selection to Cursor
---|---
![[img/Blender Basics/cursor.png]]|![[img/Blender Basics/Selection to Cursor.png]]

  
<br>
Pivot Point Editing

Change object pivot point by 3D cursor|Manual Edit Tool > Options > Transform > Affect Only Origins
---|---
![[img/Blender Basics/changePivotPoint.gif]]|![[img/Blender Basics/manualEditPivotPoint.gif]]

---

Show Statistic|Show Measurement (Edit Mode)
---|---|---
![[img/Blender Basics/showStatistic.gif]]|![[img/Blender Basics/Show Measurement (Edit Mode).png]]|![[img/Blender Basics/viewport-overlay.png \| 100]]


---

##### Parenting

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

##### Extra Tips

`L` Selecting all connected vs `A` select all|Select Mirror
---|---
![[img/Blender Basics/selectAll.gif]]|![[img/Blender Basics/selectMirror.gif]]

Proportional Editing (Smooth Selection)|Mouse Scrolling / `Page Up` / `Page Down`
---|---
![[img/Blender Basics/porpotionalEditing.gif]]|![[img/Blender Basics/influence.gif]]

Edge Slide `Shift` + `V`

  

`Ctrl` + `Tab` Change Mode
![[img/Blender Basics/mode.gif]]

  

Display as wireframe in viewport
![[img/Blender Basics/viewportDisplay.gif]]

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

### Outliner

<span style="color: #9FDB1D">Hide in viewport</span>
<span style="color: #F53F3F">Disable in renderer</span><br>

![[img/Blender Basics/viewport-renderer-visibility.png | 300]]

---

### Shader Editor

Change World / Object|Assign Material
---|---
![[img/Blender Basics/world.png]]|![[img/Blender Basics/assignMat.gif]]

---

### Resources

### Fake User - 保存没有使用的资源

-   0-No User
-   F-Fake user

Delete Images Outliner > Blender File|Unpack all media file
---|---
![[img/Blender Basics/deleteResource.gif]]|![[img/Blender Basics/unpack-resource.png]]
  

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


![](https://bytedance.feishu.cn/space/api/box/stream/download/asynccode/?code=MWUyN2U1MmU3YzQ4NWRjMmQ3ZjBjYjU0YjQ4MjY4ZjRfcXVrNENwV2JZeHhwMDg2RENoa3hXNEZCME5yNmh1NUVfVG9rZW46Ym94Y25CVks1cEdlREtRenhxdUFDbFpMWDNkXzE2NzgwMTkxODA6MTY3ODAyMjc4MF9WNA)

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

  

Paint Mask (selecting in edit mode)|Texture stencil drawing
---|---
![[img/Blender Basics/texturePaintMask.gif]]|![[img/Blender Basics/textureDrawStencil.gif]]

`Shift` + `RMB` Scale

`Ctrl` / `Command` + `RMB` Rotation

---

### BlendShape

Shape Keys

![[img/Blender Basics/shapeKey.gif]]

BlendShape Symmetrize

---

### Sculpting

`LMB` add

`Ctrl` / `Command` remove

`Shift` Smooth

---

### Animation

Keyframe|Auto-Keyframe
---|---
![[img/Blender Basics/keyframe.gif]]|![[img/Blender Basics/Auto-keyframe.gif]]

  

Animation Frame Rate

![[img/Blender Basics/framerate.png | 300]]

  

Animation Clips in Engine (Unity)

![[img/Blender Basics/animation-clip-1.png]]|![[img/Blender Basics/animation-clip-2.png]]|![[img/Blender Basics/animation-clip-3.png]]
--|--|--

---

### Anotation

`D` + `Left Mouse`

`D` + `Right Mouse`

Manage annotation / delete all -> SideBar -> View -> Anotations

---

### Render

`F12` Render

Slot for storing multiple render images

![[img/Blender Basics/render-slots.png]]

Background Lighting
![[img/Blender Basics/background-lighting.png | 500]]

Composition Guides

![[img/Blender Basics/composition-guides.png \| 300]]|![[img/Blender Basics/composition-guides-preview.png]]
---|---
  

Shadow Catcher

Enable Shadow Catcher on the object to be the shadow catcher|Check Film > Transparent
---|---
![[img/Blender Basics/enable-shadow-catcher.png]]|![[img/Blender Basics/turnon-transparent.png]]


Holdout

Turn on Hold out in Filter

![[img/Blender Basics/hold-out-1.png]]|![[img/Blender Basics/hold-out-2.png]]|![[img/Blender Basics/hold-out-3.png \| 100]]
--|--|--

Light Visibility
![[img/Blender Basics/ray-visibility.png | 300]]

### [[Blender Compositing]]


Export file format

[The Superior Alternative to PNG Renders by Polyfjord](https://www.youtube.com/watch?v=-UjJqwwMJc8)
![[img/Blender Basics/image-size-comparison.png]]

### Texture Baking

Create an image texture|Select the texture image node and click 'Bake'
---|---
![[img/Blender Basics/texture-node.png]]|![[img/Blender Basics/bake.png]]

Bake Normal texture -> Color Space: Non-Color

---

### [[Blender Scripting Basics]]

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