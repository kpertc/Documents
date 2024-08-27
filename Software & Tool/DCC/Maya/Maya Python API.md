#python #CG 

https://help.autodesk.com/view/MAYAUL/2022/ENU/?guid=Maya_SDK_Maya_Python_API_Maya_Python_API_1_0_html

Tutorial
[Maya Math by Mathias Røyrvik](https://saihtam.com/posts/maya-math/)
  

```Python
import maya.OpenMaya as om # 1st API
import maya.api.OpenMaya as om2 # 2nd API
```

```Python
st = om.MSelectionList()
om.MGlobal.getActiveSelectionList(list)
print ( list.length() )
```

```Python
dagPaths = []

i = 0
while i < list.length():
    _dagPath = om.MDagPath()
    list.getDagPath( i, _dagPath)
    dagPaths.append(_dagPath)
    
    i += 1

print (dagPaths)
```

https://help.autodesk.com/view/MAYAUL/2022/ENU/?guid=Maya_SDK_py_ref_index_html

v2 api

Easy to work with, sometimes faster

Vector

Basics

```Python
vector = om2.MVector([0,0,0])
vector1 = om2.MVector((0,1,0))

t = cmds.getAttr('locator1.t')[0] # get a array "vector" from cmds
vector = om2.MVector(t) # convert to Maya API OpenMaya vector type

# get vector from cmds
_pos = om2.MVector(cmds.xform('object', q=1, rp=1, ws=1 )) # rp -> rotation pivot

# use xyz or 012 to access the value
vector.x | vector[0]
vector.y | vector[1]
vector.z | vector[2]

vector1 + vector2 

vector.normal()
vector.length()
```

Dot & Cross product

```Python
vector1 * vector2 # dot product
vector.angle(other_vector) # directly output angle: radians 
math.degree( ) # convert to degree

vector1 ^ vector2 # cross product
```

![[img/rotate-vector.png]]

```Python
vector.rotateBy() # euler
```

![[img/get-closestNormal-from-mesh-Pos.png]]

Get closestNormal from mesh & Pos

Matrix

Matrix in maya

![[img/Matrix in maya-1.png]]|![[img/Matrix in maya-2.png]]
---|---

multMatrix

decomposeMatrix

```Python
mat = cmds.xform( object, q=1, m=1) # query matrix from object
cmds.xform( target, m=mat ) # apply mat to target object
# both object will have the same transformation
```

  

MMatrix

Create Matrix by separate list

```Python
a = [ 1, 2, 3, 4]
b = [ 5, 6, 7, 8]
c = [ 9, 10, 11, 12]
d = [13, 14, 15, 16]

mat_lists = [ a, b, c, d]
matrix = om2.MMatrix(mat_lists)
print (matrix) 
# (((1, 2, 3, 4), (5, 6, 7, 8), (9, 10, 11, 12), (13, 14, 15, 16)))
# Type = 'OpenMaya.MMatrix'
```

Create Matrix by one list

```Python
_list = [1,2,3,4,5,6,7,8,9,10,11,12,13,14,15,16]
matrix = om2.MMatrix(_list)
```

```Python
mat1 * mat2
.inverse()
```

  
MTransformationMatrix

```Python
# Create Matrix from object transformation
float_mat = om2.MMatrix( cmds.xform('object', q=1, m=1) ) 
transformation_mat= om.MTransformationMatrix(float_mat)

# convert MMatrix-> transformation matrix
# transformation matrix can deal with space   

# get
transformation_mat.translation(om2.MSpace.kTransform) # Transform Space
transformation_mat.rotation().asVector()
transformation_mat.scale()
transformation_mat.shear()

# set 
transformation_mat.setTranslation(om2.MVector([1,1,1]), space) # Transform Space
transformation_mat.setRotation(om2.MEulerRotation(om.MVector([radianx, radiany, radianz])))
transformation_mat.setScale(om2.MVector([1,1,1]), space)
transformation_mat.setShear(om2.MVector([1,1,1]), space)

# by -> add to component
transformation_mat.translateBy()

transformation_mat.asMatrix() # transformation matrix -> MMatrix
cmds.xform('object', m = transformation_mat.asMatrix() )  # set MMatrix to object xform
```

```Python
#add to components
xform_mat.translateBy(om.MVector([1,1,1]), space)
radians_xfo_2 = om.MVector(math.radians(1), math.radians(1), math.radian(1))
xform_mat.rotateBy(om.MEulerRotation(radians_xfo_2), space)
xform_mat.scaleBy(om.Mvector([2,2,1.5]), space)
xform_mat.shearBy(om.MVector([1,1,11), space)

print '\n\n\n'
print 'translation:', translation
print 'rotation', rotation 
print 'scale', scale
print 'shear', shear
```

Matrix multi -> 1 follow 2 space