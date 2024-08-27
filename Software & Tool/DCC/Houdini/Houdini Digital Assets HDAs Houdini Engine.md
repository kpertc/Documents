#Unity 

数字资产和Houdini Engine

# HDA

Turning your node graph into one custom node called digital asset

### Tutorial

[[YouTube] Houdini Digital Assets by Houdini](https://www.youtube.com/watch?v=ybk8XWBnO4o&list=PLXNFA1EysfYnnm2-UZmxrd-MWC7LTWEVl)
[[YouTube] HOUDINI 101 - 09 - Digital Assets & Unreal by EHoudiniAcademy](https://www.youtube.com/watch?v=xz3Vvy5X58U&list=PLd959VTYXCB551P4atiY52iA14JyLsaI7&index=12)

---

### Asset Type in Houdini

![[img/Houdini-Digital-Assets-HDAs-Houdini-Engine/lock-icon.png | 200]]
-   Native Nodes: C++, VEX, cannot be changed
-   Native Assets: 🔒 Lock Icon -> Digital Asset
-   Custom Assets

---

### HDA Asset Type: Geometry Asset VS Object Asset

**Geometry Asset**

<div style="display: grid; grid-template-columns: repeat(2, 2fr); grid-gap: 10px;">
	<div>
	+ Pros<br>
	Can link to other SOPs, working as Utility Assets / Functional Assets<br>
	SOP assets can have multiple inputs & output dots<br>
	</div>
	<div>
	- Cons<br>
	Have to merge everything into one node<br>
	SOP Assets have trouble merging conflicting Attribute Classes for Unreal<br>
	</div>
<div>    

<br>

Object Asset

<div style="display: grid; grid-template-columns: repeat(2, 2fr); grid-gap: 10px;">
	<div>
	+ Pros<br>
	OBJ Digital Assets can easily separate data into different GEO Containers.<br>
	Best for final container for complex Asset<br>
	</div>
	<div>
	- Cons<br>
	Hard to integrate into SOP asset<br>
	</div>
<div>    

OBJ Assets output unique meshes per Geometry Container inside Unreal

---

### HDA Create / Save / Manage

**Create**: Assets > Create New Digital Asset
**Import HDAs:** File > Import > Houdini Digital Asset

**Edit**, Select the node, `RMB` > Allow Editing of Contents
==Unlocked HDA stores their modified definitions locally in the Scene file==

**Save:** `RMB` > Save Node Type
The instance of HDA can sync content by "Match Current Definition"


`RMB` > Show in Asset Manager

-   `LMB` > uninstall -> remove the Definition from Scene file    
-   `LMB` > delete -> delete will delete the file
<br>

-   Scanned Asset Library Directory - automatically loads HDA from here
-   Configuration > Asset Bar

---

### Operator Type Properties

##### Edit Interface

**Edit Interface** (select the HDA) :
	-   Assets > Edit Asset Properties
	-   RMM > Type Properties
-   Operator Path -> External node reference

> [!info] 
> Use Edit Operator Type Properties to create interface
"Editor Parameter Interface" -> Spare Parameters
  

Basic > Minimum Inputs
Basic > Maximum Inputs


Change node color

```Python
node = kwargs["node"]
# print node

node.setColor(hou.Color((1,1,1)))
```

  

Edit Icons

![[img/Houdini-Digital-Assets-HDAs-Houdini-Engine/edit-icon-1.png]]|![[img/Houdini-Digital-Assets-HDAs-Houdini-Engine/edit-icon-2.png]]|![[img/Houdini-Digital-Assets-HDAs-Houdini-Engine/edit-icon-3.png]]
--|--|--

---

Check current HDA path
![[img/Houdini-Digital-Assets-HDAs-Houdini-Engine/Check current HDA path.png]]

Embedded HDA - Asset Definitions that were Backed Up into the Scene File

Keep node editable even when it is locked

![[img/Houdini-Digital-Assets-HDAs-Houdini-Engine/Keep node editable even when it is locked.png]]

---

##### `TAB` menu path

Interactive > ShelfTools > TAB Submenu Path

![[img/Houdini-Digital-Assets-HDAs-Houdini-Engine/sub-menu1.png]]|![[img/Houdini-Digital-Assets-HDAs-Houdini-Engine/sub-menu2.png]]
---|---

---

##### Add Houdini HDA Path - [Houdini - 添加HDA扫描路径]

---

### File

-   HDA - Commercial License
    
-   HDALC - Indie License
    
-   HDANC - Non-Commercial License
    

---

# Houdini Engine

Recook -> Refresh
`RMB` > Reimport
Rebuild -> Update
Bake -> bake to static mesh

### Unity Plugin #Unity
[Houdini Engine for Unity: Main Page](https://www.sidefx.com/docs/unity/index.html)

  

Path : `C:\Program Files\Side Effects Software\Houdini Engine\Unity\xxxxxx`
[Houdini Engine for Unity | Session Sync](https://www.youtube.com/watch?v=kzKGZnimYlo)
[Unity Starter Kit](https://www.sidefx.com/tutorials/unity-starter-kit/)

---

[[YouTube] Houdini Engine for Unity | Session Sync by Houdini](https://www.youtube.com/watch?v=kzKGZnimYlo)

  

Houdini Engine - Session Sync

\+ > New Pane Tab Type > Misc > Houdini Engine SessionSync

![[img/Houdini-Digital-Assets-HDAs-Houdini-Engine/SessionSync.png | 500]]

1.  In Houdini Engine SessionSync, Start Connection
2.  In Unity Houdini Engine, Connect to Houdini    
3.  Global Nodes appear in object context in Houdini

![[img/Houdini-Digital-Assets-HDAs-Houdini-Engine/globalnodes.png | 200]]


---

Create Material in Houdini

Plugin Settings > Advanced | Create Attribute in Houidini
---|---
![[img/Houdini-Digital-Assets-HDAs-Houdini-Engine/Plugin Settings-Advanced.png]]|![[img/Houdini-Digital-Assets-HDAs-Houdini-Engine/create-attribute.png]]
