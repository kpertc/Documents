#Unity #UI 

##### Tutorials https://blog.csdn.net/ChinarCSDN/article/details/90313617

<br>

##### Basics

Unit 1 pixel -> 1 Unit, normally 1 Unit -> 1 meter, which makes UI huge.
Unity UI Order- > lower in hierarchy on top, higher in hierarchy on back

![[img/Unity VR img/red-top.png]]|![[img/Unity UI (UGUI)/blue-top.png]]
---|---

<br>

##### [Canvas](https://www.youtube.com/watch?v=at6gUB_-HII)

![[img/Unity UI (UGUI)/Camera (left) VS Overlay (right).png | 400]]

<br>

Camera (left) VS Overlay (right)

|Screen Space Overlay Canvas|Screen Space Camera Canvas|
|---|---|
|**Pros**: Easy to use the size is determined by the size of game viewpoint (not editable).|**Pros**: Use a perspective camera to render, can render perspective angle. Can use properly use Z-axis|
|**Cons**: Only support orthographic angle, no depth effect. | **Cons**: 3D objects can block UI in Screen Space|
|![[img/Unity VR img/Screen Space Overlay Canvas.png]]|![[img/Unity VR img/Screen Space Camera Canvas.png]]|
|The position of Screen Space Camera Canvas will be constrained at front of the camera.|3D objects can block UI in Screen Space Camera Canvas.|

"Plane Distance" setting can adjust the distance between the canvas and the camera, to minimize the error. To completely prevent the issue, use a second camera render the UI.

<br>

##### Rect Transform

2D Rectangle specified by width and height related to pivot point. (also included ability of Z axis, rotation and scale, so it can be manipulated in 3D)

<br/>

**Resources:**

<div style="display: grid; grid-template-columns: repeat(2, 2fr); grid-gap: 10px;">
		<div>
		<a href="https://www.youtube.com/watch?v=FeheZqu85WI">[YouTube] Unity Official</a><br>
		<a href="https://www.youtube.com/watch?v=y6tDqOm6xKE">[YouTube] 3DBuzz</a>
	</div>
	<div>
		<a href="https://docs.unity3d.com/Packages/com.unity.ugui@1.0/manual/UIBasicLayout.html">[[Unity Official Docs] Basic Layout</a><br>
		<a href="https://docs.unity3d.com/Packages/com.unity.ugui@1.0/manual/class-RectTransform.html">[[Unity Official Docs] RectTransform</a>
	</div>
</div>
<br/>

![[img/Unity VR img/rect-tool.png | 300]]

Recommend to use **Rect Tool** to adjust UI (Shortcut -> `T`)

![[img/Unity UI (UGUI)/Hold Shift to dragging scale proportionally.png | 500]]

Hold `Shift` to dragging scale proportionally

<br>

![[img/Unity UI (UGUI)/local.png]]|![[img/Unity UI (UGUI)/global.png]]
:-:|:-:
Local|Global

<br>

Anchor - (For Layout) (0-1)

A `Rect Transform` can be anchored to its parent if the parent also has a `Rect Transform` component. The child's position is relative to the parent's position. All UI elements are ultimately a child of a canvas. Anchor's position is limited within parent's Rect Transform's bound.

![[img/Unity UI (UGUI)/4-anchor.png]]|![[img/Unity UI (UGUI)/each-anchor.png]]
:-:|:-:
4 anchor -> 4 triangle gizmo|Each anchor -> each corner


"Single Mode"

![[img/Unity VR img/single-mode.png]]|![[img/Unity UI (UGUI)/offset-singlemode.png \| 200]]|![[img/Unity UI (UGUI)/offset.png]]
--|--|--


<div align="center" >
Pos (Anchor to Pivot Point) <br>
Width, Height -> Fixed Size
</div>

"Splited Mode"

![[img/Unity VR img/split-mode.png]]|![[img/Unity VR img/split-mode-inspector.png]]
---|---

Distance to anchored edge (Padding) -> Relative Size

<br>

![[img/Unity UI (UGUI)/Anchor to itself is fixed distance.png | 300]]


Anchor to itself is fixed distance

<br>

![[img/Unity UI (UGUI)/UI_Anchored1.gif]]|![[img/Unity UI (UGUI)/UI_Anchored2.gif]]|![[img/Unity UI (UGUI)/UI_Anchored3.gif]]
--|--|--
At Center (Follow)|At Corner (Follow)|At Edge (Stretch)

<br>

**Pivot - (For Animation [Rotation / Scale] / Movement can also manipulate [Transform])**
Pivot value is not limited by range 0 - 1

<br>

![[img/Unity UI (UGUI)/anchor-presets.png]]

<div align="center" >
Hold `Shift` to set pivot, or `Alt` to set position, or `Shift` + `Alt` to set both<br>
Red area indicates stretch
</div>

<br>

[Blueprint Mode VS Raw Edit Mode](https://www.jianshu.com/p/4ed952e2f764)

![[img/Unity UI (UGUI)/blueprint-raw-edit-mode.png | 300]]

**Blueprint mode**

![[img/Unity UI (UGUI)/blueprint-mode-1.gif]]|![[img/Unity UI (UGUI)/blueprint-mode-2.gif]]
---|---

**Raw edited mode**

![[img/Unity UI (UGUI)/raw-edit-mode-1.gif]]|![[img/Unity UI (UGUI)/raw-edit-mode-2.gif]]
---|---

<br>

##### Image

![[img/Unity UI (UGUI)/uncheck-preserve-aspect.png]]|![[img/Unity UI (UGUI)/check-preserve-aspect.png]]|![[img/Unity UI (UGUI)/preserve-aspect.png]]
--|--|--
Unchecked Preserve Aspect|Checked Preserve Aspect


Use `Sprite Editor` to slice UI border

<br>  


##### Text

[Rich Text](https://docs.unity3d.com/Packages/com.unity.ugui@1.0/manual/StyledText.html) Enable to support rich text. 

![[img/Unity UI (UGUI)/rich-text.png]]


``` html
<b></b>
<i></i>
<size></size>
<color = red></color>
...
```

 ![[img/Unity UI (UGUI)/rich-text-example.png | 500]]

Overflow

Horizontal Overflow: Wrap (Wrap to next line)|Horizontal Overflow: Overflow
---|---
![[img/Unity UI (UGUI)/Horizontal Overflow Wrap Wrap to next line.png]]|![[img/Unity UI (UGUI)/Horizontal Overflow Overflow.png]]





Vertical Overflow: Truncate (Disappear)|Vertical Overflow: Overflow
---|---
![[img/Unity UI (UGUI)/Vertical Overflow Truncate Disappear.png]]|![[img/Unity UI (UGUI)/Vertical Overflow Overflow.png]]

Best Fit: automatically set overflow base on the min-max setting

![[img/Unity UI (UGUI)/bestfit.png]]

<br>

##### Toggle Group

On `Toggle` to reference `Toggle Group`
Only one Toggle can be toggled in the group. (Behave more like a radio button than a checkbox)


![[img/Unity UI (UGUI)/toggle-group-1.png]]|![[img/Unity UI (UGUI)/toggle-group-2.png]]
---|---

![[img/Unity UI (UGUI)/toggle-group.gif]]

<br>

##### [Canvas Group](https://docs.unity3d.com/Packages/com.unity.ugui@1.0/manual/class-CanvasGroup.html)

Control whole group of UI elements from one place.
![[img/Unity UI (UGUI)/canvas-group.png]]
  

##### Masking

Rect Mask 2D

Mask

Mask Area will be determined by the Image Component on the same GameObject.

`Show Mask Graphic` -> only use the as mask area or also show the content of the image

![[img/Unity UI (UGUI)/mask.png]]

<br>

Parent: Mask -> Mask and Image (work as mask image)

![[img/Unity UI (UGUI)/parent-mask-1.png]]|![[img/Unity UI (UGUI)/parent-mask-2.png]]
---|---

Child: Image -> Image

![[img/Unity UI (UGUI)/child-image-image.png]]|![[img/Unity UI (UGUI)/child-Image-Image-2.png]]
---|---

Sprite Mask

-   On SpriteRenderer -> Mask Interaction Visible inside Mask / Visible outside Mask


UI Sprite auto-size fit for text -> https://www.youtube.com/watch?v=W_ST3nsf27Y

<br>

##### UI Effects
-   Shadow
-   Outline

Extensible for adding more effects from online resources

<br>

##### Canvas Renderer -> Cull Transparent Mesh

![[img/Unity UI (UGUI)/cull-transparent-mesh.png]]

When alpha -> 0, it will cull the mesh. Optimization

![[img/Unity UI (UGUI)/notcull.png]]|![[img/Unity UI (UGUI)/cull.png]]
---|---
Not Cull|Cull

##### [Navigation Option](https://docs.unity3d.com/Packages/com.unity.ugui@1.0/manual/script-SelectableNavigation.html) -> Navigation Direction