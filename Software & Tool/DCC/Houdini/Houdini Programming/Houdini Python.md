#python 

### **Python** **Shell**
|New Tab > New Plane Tab Type|Windows > Python Shell`Alt` + `Shift` + `P`|Up arrow -> last command|
|-|-|-|
|![[Houdini-Python-img/PythonShell-NewTab.png]]|![[Houdini-Python-img/PythonShell-Windows.png]]|![[Houdini-Python-img/PythonShell.png]]

---

Python Expression

---

### `hou` module

[[YouTube] Introduction to Python in Houdini || Exploring Houdini](https://www.youtube.com/watch?v=59vetivUGes)

[[YouTube] Houdini 18 - Intro to Python by Indie-Pixel](https://www.youtube.com/watch?v=c4O0mtUTJdk&list=PL5V9qxkY_RnJstgKRPN8cCErK4oYB8Fax&index=1)

[hou.Node](https://www.sidefx.com/docs/houdini/hom/hou/Node.html)

Develop PySide UI → [[PyQT-PySide]]

---

### Execute in Python Shell
Python Source Editor -> variables are available for expression
`hou.session. ...`

##### Python in HDA
1.  Create a python module in HDA
	![[Houdini-Python-img/HDA-1.png | 500]]
2.  Call in Callback Script `hou.pwd().hdaModule().functionName()`
	![[Houdini-Python-img/HDA-2.png]]
	`hou.phm()` `= hou.pwd().hdaModule() = hou.pwd().hm()`
3. Execute
	![[Houdini-Python-img/executeHDAPython.gif | 300]]

`hou.pwd().path()` # HDA node path

---

### Basics
```python
Common help
dir()
help()
```

### Get Node
```Python
_node = hou.node("/obj") # get node
_node.createNode("geo","My_Geo") # create node: Create a "Geo" node in obj

_node.type() # get type of the node

# check node is exist -> == None
if hou.node('/obj/MY_GEO') == None:
```

![[Houdini-Python-img/show-node-type.png | 200]]
Show the node type

### Manipulate params

```Python
node
_node.parm("execute").pressButton() # press button

_node.parm('group').set('') # set Group
# Set Expression
_node.parm("f1").setExpression( "$RFSTART", language = hou.exprLanguage.Hscript )

# get parameter value
_node.parm("soppath").eval()
```

### Set Input, (Connect wire)

```Python
setInput(input_index, item_to_become_input, output_index=0)
_node.setInput(0, _node, 0)
```

### Get Input

```Python
_node = hou.pwd()
_node.input(0) # the first input
```

### Delete all nodes in a node

```Python
children = _node.children()
for child in children:
    child.destroy() 
```

### Geometry

```Python
_geo = _node.geometry()
_attribute = geo.findGlobalAttrib('attributeName') # GlobalAttrib -> Detail Attrib
```

### Set DisplayFlag

```Python
_node.setDisplayFlag(True)
_node.setRenderFlag(True)
```

### Set Keyframe

```Python
_node.parm('parm').deleteAllKeyframes() # delete all keyframe

# Creaet a keyframe
key = hou.Keyframe()
key.setFrame(30)
key.setValue(100)

# Set Slope
key.setInSlopeAuto(1) # add slope base on curve
key.setSlopeAuto(1)
    
# Set Keyframe
_node_stemBand.parm('bend').setKeyframe(key)
```

### Pop Message box
``` python
hou.ui.displayMessage('Hello World')
```

![[Houdini-Python-img/pop-message.png | 200]]

### [Flipbook](https://www.sidefx.com/docs/houdini/hom/hou/FlipbookSettings.html)

```Python
cur_desktop = hou.ui.curDesktop()
scene_viewer = hou.paneTabType.SceneViewer
scene = cur_desktop.paneTabOfType(scene_viewer)
scene.flipbookSettings().stash()
flip_book_options = scene.flipbookSettings()

flip_book_options.output('$HOME/Desktop/test.png') # Provide flipbook full path with padding.
flip_book_options.frameRange((0, 10)) # Enter Frame Range Here in x & y
flip_book_options.useResolution(1)
flip_book_options.resolution((1080, 720)) # Based on your camera resolution
scene.flipbook(scene.curViewport(), flip_book_options)
```