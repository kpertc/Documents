#PCG 

### Tutorials
|YouTubers|Pros|
|---|---|
|[Indie-Pixel](https://www.youtube.com/c/IndiePixel3D)|PCG modelling / Python|
|[Junichiro Horikawa](https://www.youtube.com/c/JunichiroHorikawa)|VEX & Algorithm|
|[EHoudiniAcademy](https://www.youtube.com/c/EHoudiniAcademy)|Foundation and Building PCG|
|[Tim van Helsdingen](https://www.youtube.com/c/TimvanHelsdingen)|Foundation and Plant|
|[Simon Houdini](https://www.youtube.com/channel/UCvuT2bzBB0kzne16DBAtmLQ)|Fast Phase & Tips Tricks|

Tutorial Archives
[Magic Market | Procedural Rocks 1 | Geometry Generation](https://www.youtube.com/watch?v=2oC9TOgQ3KE)

Viewport Lighting Setup
[[YouTube] Lights In The Viewport || Houdini Beginner Tutorial by Simon Houdini](https://www.youtube.com/watch?v=ORMDBOOsGBY)


大教程网盘地址（仅供内部学习）
https://bytedance.feishu.cn/drive/folder/fldcnxsvxAjOCYTVqG6XfzCAnOf

---
MacOS can not find licence server:
[Why have my licenses stopped working on Mac OSX? | SideFX](https://www.sidefx.com/faq/question/osx-and-the-licenses-have-stopped-working/)

---

### Houdini History

PRISMS -> Houdini (1996)

SideFX - Toronto based

-   **Pros**: Procedural
-   **Cons**: Expensive, steep learning curve

---

### Topics

**[[Houdini UI Tips]]**
**[[Houdini Channel & Parameters]]**
[[Houdini Digital Assets HDAs Houdini Engine]]
[[Houdini Group and VEX]]

[[Houdini L-System]]
[[Houdini UV]]
[[Houdini Noise]]
[[Houdini Mantra Render]]

[[Houdini Programming/Houdini Programming]]
[[Houdini Programming/Houdini Vector Expression Language, VEX]]
[[Houdini Programming/Houdini VEX Math]]
[[Houdini Programming/Houdini Python]]

---
### Key-Mappings

Edit > Hotkey Manager

<div style="display: grid; grid-template-columns: repeat(2, 2fr); grid-gap: 10px;">
	<div>
		<code>S</code> Select<br>
		<code>Enter</code> Handle<br>
		<code>D</code> Display Options<br>
	</div>
	<div>
		<code>SPACE</code> + <code>H</code>  Frame all objects<br>
		<code>SPACE</code> + <code>Z</code>  set new view pivot<br>
		Hold <code>Ctrl</code>to create at center<br>
	</div>
</div>

<br>

<div style="display: grid; grid-template-columns: repeat(2, 2fr); grid-gap: 10px;">
	<div>
		In View<br>
		<code>1</code> Persp<br>
		<code>2</code> Top<br>
		<code>3</code> Front<br>
	</div>
	<div>
		<code>2</code> Points<br>
		<code>3</code> Edges<br>
		<code>4</code> Primitives<br>
	</div>
</div>

<br>

<div style="display: grid; grid-template-columns: repeat(2, 2fr); grid-gap: 10px;">
	<div>
		In View<br>
		<code>E</code> Scale<br>
		<code>R</code> Rotation<br>
		<code>S</code> Translate<br>
	</div>
	<div>
		Node<br>
		<code>Q</code> or <code>B</code> ByPass<br>
		<code>Q</code>, <code>W</code>, <code>E</code>, <code>T</code> hotkeys depend on the network
	</div>
</div>

G Home view
Holding X on viewport Grid Option

---

<div style="display: grid; grid-template-columns: repeat(3, 2fr); grid-gap: 10px;">
	<div>Point -> multiple vertexes</div>
	<div>Point -> modelling</div>
	<div>Vertex -> shading</div>
</div>

---

[Expressions in file names](https://www.sidefx.com/docs/houdini/render/expressions.html)
[Network types and node flags](https://www.sidefx.com/docs/houdini/network/flags.html)


### Nodes

-   [Object nodes](https://www.sidefx.com/docs/houdini/network/flags.html#obj)
-   [Geometry nodes (SOPs)](https://www.sidefx.com/docs/houdini/network/flags.html#sop)
-   [Dynamics nodes (DOPs)](https://www.sidefx.com/docs/houdini/network/flags.html#dop)
-   [Compositing nodes (COPs)](https://www.sidefx.com/docs/houdini/network/flags.html#cop)
-   [Render nodes (ROPs)](https://www.sidefx.com/docs/houdini/network/flags.html#out)
-   [VOP nodes](https://www.sidefx.com/docs/houdini/network/flags.html#vop)
-   [Channel nodes (CHOPs)](https://www.sidefx.com/docs/houdini/network/flags.html#chop)
-   [Task nodes (TOPs)](https://www.sidefx.com/docs/houdini/network/flags.html#top)


Performance monitor
https://www.sidefx.com/docs/houdini/model/attributes.html#intrinsic

SOPs
<div style="display: grid; grid-template-columns: repeat(2, 2fr); grid-gap: 10px;">
	<div>
		Transform<br>
		Soft Transform<br>
		<br>
		Switch<br>
		Scatter<br>
		Resample<br>
		Polyframe (output TBN direction)
	</div>
	<div>
		Null<br>
		Output<br>
		Merge<br>
		Subnet → folder<br>
		Join (join into a single primitive)
	</div>
</div>

<br>
<br>

<div style="display: grid; grid-template-columns: repeat(2, 2fr); grid-gap: 10px;">
	<div>
		Copy (Copy Transform)<br>
		CopyToPoints<br>
		<br>
		Edit (Manually edit)<br>
		Blast (Delete)<br>
		Delete<br>
		Facet<br>
	</div>
	<div>
		Modelling<br>
		Divide (get Dual Mesh or triangulate mesh) <br> 
		Bevel<br>
		Remesh<br>
		Fuse<br>
		<br>
		Boolean
	</div>
</div>

<br>

-   AttributeCreate
-   AttributeRandomize
-   AttributeNoise
-   AttributePaint
-   AttribtueFromMap
-   AttributeTransfer
-   AttributeRename
-   AttributePromote
-   AttributeRemap
-   AttributeCast - change attr precision

<br>

-   Group promote

<br>

-   Line
-   Curve
-   Grid
-   Polywire
-   Ray

<br>

-   [Compile Block](https://www.sidefx.com/docs/houdini/model/compile) - Performance optimization (Multi-Thread for Loops)
    
    -   Turn on compile badge display to see
    -   Non compile nodes: polyExtrude, attribute transfer, findshortestpath, uv quick shade
    -   No `$` Local Variable, use VEX instead
    -   No 0, no referenc("../xxx"), use spare input instead
    - ![[img/Houdini Basics img/compile-block.png]]


Labs
-   Turntable
-   WFC

---
### Animation & Simulation
[[Houdini Animation & Simulation]]

---
[Environment variables](https://www.sidefx.com/docs/houdini/basics/config_env.html)

Include Building Generator

https://www.sidefx.com/tutorials/game-development-toolset-overview/

<iframe width="560" height="315" src="https://www.youtube.com/embed/ohUEXxIKAWI" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" allowfullscreen></iframe>


---
### VAT
[[Houdini VAT Vertex Animation Texture]]

---
### Volume

Voxel

Fog / SDF

`Volume`
`Volume Visualization`
`Volume Wrangle`

---
### [SOP Solver](https://www.sidefx.com/docs/houdini/nodes/sop/solver.html)

Prev_Frame (always update)
Input -> constant

---

### [Half-edge](https://www.sidefx.com/docs/houdini/vex/halfedges)






