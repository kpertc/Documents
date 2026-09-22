#python 

[PyMel Documentation (Maya 2017)](https://help.autodesk.com/cloudhelp/2017/ENU/Maya-Tech-Docs/PyMel/)

PyMEL is not installed by default since Maya 2022 (optional installer component, not guaranteed on a studio machine or in mayapy) → prefer maya.cmds / OpenMaya 2.0 for new tools

|Pros|Cons|
|------------ | ------------|
|OOP<br/>Ref is object, not string<br/>Code is cleaner|Performance<br/>Not installed by default since Maya 2022|

Pickle / Serialization -> Transfer data lossless

[PyMel Install if needed](https://knowledge.autodesk.com/support/maya/learn-explore/caas/CloudHelp/cloudhelp/2022/ENU/Maya-Scripting/files/GUID-2AA5EFCE-53B1-46A0-8E43-4CD0B2C72FB4-htm.html)


Use `help()`
  
```Python
import pymel.core as pm
```

```Python
pm.PyNode("objectName") # get node/object
```

```Python
pm.selected() # get selection array
```

```Python
_parnetObj = _obj.getParent()
```

```Python
_obj.translateX.set( value )
```

```Python
pm.spaceLocator() # Create a locator
```

  


Ndoe Type
```python
geo_shapes = []
for i in pm.selected():
	shape = i.getShape()
	if isinstance(shape, pm.nt.GeometryShape): # getShape() returns None for non-geometry transform, so this also guards None
		geo_shapes.append(shape)
```

```Python
cam = pm.ls(type='camera')[0]
parent = pm.listRelatives(cam, p=1)[0]
trans = pm.xform(parent,q=1,t=1)

# or in PyMel
trans = pm.ls(type='camera')[0].getParent().getTranslation()
```

Math

```Python
# vector
vec = pm.dt.Vector((3,4,5))
vec = pm.dt.Vector() # vector Zero (0,0,0)

vec.x # return x value, vec.y, vec.z

normVec = vec.normal() # return the normalized vector
vec.normalize() # normalize the vector (modify)

vec.length()


```

```python
vecX = pm.dt.Vector.xAxis
vecZ = pm.dt.Vector.zAxis
vecY = pm.dt.Vector.yNegAxis
```

Matrix

![[img/PyMelMatrix.png]]