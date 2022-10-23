### Create Object

```py
from maya import cmds #as cmds

cmds.polyCube(width=1, height=4, depth=2)
cmds.polyCube(w=1, h=4, d=2)

#Plane is nurb
cmds.plane( p=(1, 1, 1), s=10 )

# renaming
cmds.rename('pCube1', 'abc') #Rename pCube1 to abc

```
### List Attribute
```py
cmds.listAttr('pCube1')
```