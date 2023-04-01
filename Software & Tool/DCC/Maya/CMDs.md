### Documents Website

[All Commands](https://download.autodesk.com/us/maya/2011help/Commandspython/)
[Modelling Commands](https://download.autodesk.com/us/maya/2011help/Commandspython/cat_Modeling.html#Polygons)

[Python Scripting for Maya Artists by Chad Vernon](https://www.chadvernon.com/python-scripting-for-maya-artists/)

### Import

```Python
import maya.cmds as cmds
from maya import cmds #as cmds

reload (ge) # reload the script
```

### Creating Object

```Python
cmds.polyCube(width=1, height=4, depth=2)
cmds.polyCube(w=1, h=4, d=2)

# NURBS plane
cmds.plane( p=(1, 1, 1), s=10 )
```

### Select

```Python
cmds.select("") # hierachy
```

### Object Type & Node Type

```Python
cmds.objectType('object')
cmds.nodeType(obj)
```

### Rename

```Python
cmds.rename('pCube1', 'abc') #Rename pCube1 to abc
```

### Delete

```Python
#检测物体存在
if cmds.objExists('pCube1'):

#删除物体
cmds.delete('pCube1')

#删除历史
cmds.delete('pCube1', constructionHistory = True)
```

### MEL in Python

```Python
import maya.mel as mel
mel.eval()
```

### Attribute

```Python
cmds.listAttr('pCube1')

cmds.getAttr('pCube1.translateX')

cmds.setAttr( objName + '.translateX', 1)
cmds.setAttr( objName + '.visibility', 0)
cmds.setAttr( objName , 1, 1, 1, type='double3') # with type

cmds.addAttr()

# check if the attribute exist on the object
cmds.attributeQuery('attributeName', node='NodeName', exists=True)
```

### Alias Attribute

```Python
cmds.aliasAttr() # get alias need e.g. Blendshape weight name
```

### Connection Info

```Python
# check exist -> return True or False
isSource = cmds.connectionInfo( f'{skydomeLight}.color', isSource=True)
isDestination = cmds.connectionInfo( f'{skydomeLight}.color', isDestination=True)

# return node
source = cmds.connectionInfo( f'{skydomeLight}.color', sourceFromDestination=True) 
destination = cmds.connectionInfo( f'{skydomeLight}.color', destinationFromSource=True) 
```

### List

```Python
selection = cmds.ls(selection=True) # Get Selection

#Get Full Path
path = cmds.ls('boot_wiper', long=True) 
#['|Car|Car_Trunk|Trunk_Body|boot_wiper'] #type List

# return specific type
Materials = cmds.ls(materials=True) # Get Materials
Joints = cmds.ls(type = "joint") # Get Joints
"blendShape"
allLights = cmds.ls( type = ['volumeLight', 'areaLight', 'spotLight', 'pointLight', 'directionalLight', 'ambientLight', 'aiLightPortal', 'aiPhotometricLight', 'aiAreaLight', 'aiSkyDomeLight' ] )
```

```Python
# list all camera
camerasList = cmds.listCameras()
```

### listRelatives

```Python
 # list all children transform
 cmds.listRelatives(_group, allDescendents=True, type="transform")

# Check parent
parent = cmds.listRelatives( "object" , parent = True )
# parent == None -> object at root
```

### Xform

```Python
cmds.xform( 'object', ro=(x, y, z) ) # set transform
cmds.xform('object', q=True, ws=True) # WS True -> World Space; False -> local Space

# query world space T R S
transform = cmds.xform( 'object', q=1, ws=1, t=1 )
rotation = cmds.xform( 'object', q=1, ws=1, ro=1 )
scale = cmds.xform( 'object', q=1, ws=1, s=1 )

matrix = cmds.xform('object', q=1, m=1)
```

### Freeze Transformation

```Python
cmds.makeIdentity('pCube1', apply=True) #ALL

cmds.makeIdentity(selected, translate=True)
cmds.makeIdentity(selected, rotate=True)
cmds.makeIdentity(selected, scale=True)
```

### Grouping

```Python
#把物体层级移到 新建的组
cmds.group( em=True, name='groupName' )
cmds.group( 'circle1', 'sphere1', n='group1' ) #n short for name

#把物体层级移到一个位置
cmds.parent( 'pCube2', 'null2' ) #物体，要到的位置
```

```Python
out = cmds.duplicate(_group)
out[0] # name of result transform
```

### File

```Python
cmds.file(BaseFile, open=1, f=1)
cmds.file(f"path", r=True) # open as reference
```

### Reference

```Python
# Remove all reference
def removeAllReferences():
    references = cmds.ls(references=True)
    for ref in references:
        referencePath = cmds.referenceQuery(ref, filename=True)
        cmds.file(referencePath, removeReference=True)
```

### Move Pivot Point to World Center

```Python
cmds.move(0, 0, 0, 'pCube1' + '.scalePivot', 'pCube1' + '.rotatePivot', absolute=True);

#选择全变
selection = cmds.ls(selection=True)

for selected in selection:
    cmds.move(0, 0, 0, selected + '.scalePivot', selected + '.rotatePivot', absolute=True);
```

### Hide

```Python
cmds.hide(BaseGeoGroup)
```

### UV

```Python
#move UV
cmds.polyEditUV(u=0.0, v=-0.1)
```

### UV Set

### LightLink

```Python
# Connect
cmds.lightlink( light=('aiSkyDomeLight1'), object=('artist_file:main_baseface') )
# Break
cmds.lightlink( b=1, light=('aiSkyDomeLight1'), object=('artist_file:main_baseface') )
```

### Combine

```Python
cmds.polyUnite(['obj1','obj2','obj3'], n=name)[0] # [0] return new object transform
```

### Create Layers

```Python
#Check if the layers exists

#Creating Layers in the order
cmds.createDisplayLayer(name='ChromePlastic_L')

#Set Color
cmds.setAttr ('int_L.color', 3) 
```

### Evaluation

```Python
cmds.polyEvaluate( b=True ) #Bouding box
cmds.polyEvaluate( t=True ) #Triangle
```

### Material

##### Create Material & Shading nodes

```Python
#Create New Material
cmds.shadingNode("phong", asShader=True, name="myMaterial")

#Create File Node
cmds.shadingNode("file", asTexture=True, name="myImageFile")

#Connect Image Node to Material Color
cmds.connectAttr('filePathImage.outColor', 'myShader.color')

#image Path -> String
imagePath = '/Users/chenjingfu/Desktop/DJI_0088.png'

cmds.setAttr('filePathImage.fileTextureName', imagePath, type="string")
```

##### Assign Material

```Python
#select Object and assign
selection = cmds.ls(selection=True)
cmds.hyperShade(selection, assign = 'blinn1') #material Name
```

```Python
#Check if the material exists
if cmds.objExists('blinn1'):
    print('Exist')
    
#Get materials
Materials = cmds.ls(materials=True)
```

https://medium.com/graphic-programming/create-texture-to-the-material-ef6f40d19e28

```Python
#Set Default Color
def setMaterialColor(materialName,r,g,b):
    
    if cmds.objExists(materialName):
        cmds.setAttr(materialName + '.color', r,g,b, type="double3")

Car_Paint_shader = ['Car_Paint_shader',0.3,0.14,0]  
Car_Leather_shader = ['Car_Leather_shader',0.34,0.12,0.1]     
Car_Cloth_shader = ['Car_Cloth_shader',0.12,0.22,0.12] 

setMaterialColor(Car_Paint_shader[0],Car_Paint_shader[1],Car_Paint_shader[2],Car_Paint_shader[3])
```

##### Select Object By Material

```Python
cmds.hyperShade(objects= materialName)
```

### BlendShape

##### Create BlendShape

```Python
# get object
ref = "pSphere1"
target = "pSphere2"

cmds.blendShape(ref, target)
cmds.blendShape(ref, ref2, target) # multiple blendShape
# target -> last object
name = ""
```

  

```Python
history = cmds.listHistory(BSobject)
blendshapes = cmds.ls(history, type="blendShape")
BSNode = blendshapes[0]
return BSNode
```

##### Query weight

```Python
# return list of weights
cmds.listAttr('blendShape1.w', m=True) 
# w for weight, m for multiple
```

##### Edit value

```Python
cmds.blendShape( 'blendShape1', edit=True, en=0.8 ) # set Envelope to 0.8
cmds.blendShape( 'blendShape1', edit=True, w=[(0, 0.6), (1, 0.1)] )
# w -> weight, set first weight to 0.6, set second weight to 0.1

mel.eval(f'setAttr "{BSNode}.{name}" 0;') # set value by attr name
```

##### Manual set BlendShape

Same amount of vertices

1.  Select the changed object first
    
2.  Select the original object
    
3.  Deform - BlendShape
    

### Deformer - Wrap

```Python
cmds.select("main_eyes_eyelash", "main_baseface") # follower , target
cmds.CreateWrap()
```

### Animation

##### Keyframe

```Python
# set Key
cmds.setKeyframe('object', v= value, at='attribute', t = time)

# Delete Keys
cmds.cutKey('object', s=True)
cmds.cutKey('object', cl = True)
```

##### Playback

```Python
cmds.currentTime( 0 )

cmds.playbackOptions( minTime=0, maxTime = 10 )
```

### Parent Constraint

```Python
cmds.aimConstraint( 'ref', 'obj' )

cmds.parentConstraint()
```

### Settings

```Python
cmds.about()

https://help.autodesk.com/cloudhelp/2019/ENU/Maya-Tech-Docs/CommandsPython/currentUnit.html

print('Lenght Unit: ' + str(cmds.currentUnit( query=True, linear=True ))) #cm

currentUnitFrameRateCoversion = {
    "game": 15, "film": 24, "pal": 25,
    "ntsc": 30, "show": 48, "palf": 50,
    "ntscf": 60,
}

frameRate = currentUnitFrameRateCoversion.get(cmds.currentUnit( query=True, time=True ))
    
print ('fps: ' + str(frameRate))

print('Playback Speed =' + str(cmds.playbackOptions( query=True, playbackSpeed=True ) ) )


# Set Time Unit
cmds.currentUnit( time ='ntsc' ) 

# Set Length Unit
cmds.currentUnit( linear='mm' ) 
cmds.currentUnit( linear='m' )
```

### Image Plane

```Python
# create image plane
creation = cmds.imagePlane( name="Foo", maintainRatio=True)
imagePlaneTransform = creation[0]
imagePlane = creation[1]

imagePath = "C:/Users/Admin/Desktop/Web 1920 – 1.jpg"
cmds.setAttr(f'{imagePlane}.imageName', imagePath, type="string")

# Query image size
imageSize = cmds.imagePlane( imagePlane , q=True, iz=True )
print(imageSize)
```

### Open Web or File

```Python
cmds.launch(web="http://www.autodesk.com")
cmds.launch(directory="C:/matemp")
```

### Unknown Plugin(删除未知插件)

```Python
cmds.unknownPlugin
```

# Arnold Render

### Set Render Quality

```Python
cmds.setAttr('defaultArnoldRenderOptions.AASamples', 6)
cmds.setAttr('defaultArnoldRenderOptions.GIDiffuseSamples', 5)
cmds.setAttr('defaultArnoldRenderOptions.GISpecularSamples', 4)
cmds.setAttr('defaultArnoldRenderOptions.GITransmissionSamples', 4)
cmds.setAttr('defaultArnoldRenderOptions.GISssSamples', 5)
```

### Render to Texture

```Python
cmds.arnoldRenderToTexture(folder='C:/Users/Admin/Desktop/', resolution=2048, aa_samples=5)
```


```Python
import mtoa.utils as mutils

# Create an arnold skydomelight
skyDomeLight = mutils.createLocator('aiSkyDomeLight', asLight=True)

# Edit aiArealight Light Shape to disk
lightShape = cmds.getAttr("aiAreaLightShape1.ai_translator")
cmds.setAttr("aiAreaLightShape1.ai_translator",'cylinder',type="string") # disk
```

  

# GameExporter

```Python
# Open GameExporter
mel.eval('gameFbxExporter;') 
```

![[img/fbx导出.png]]

```Python
# Switch Tabs  1 Model Tab  2 Animation Tab
mel.eval('gameExp_ChangeExportType(2)') # Switch to Animation Tab
```

Get Presets

```Python
# get all presets list
list = mel.eval('gameExp_GetGameFbxExporterNodeList;') # Get all Presets

# get current preset name
_p = str(mel.eval("$temp=$gGameFbxExporterCurrentNode")) # Convert MEL to Python
```

Get Animation Clips Size

```Python
animClips = mel.eval( 'int $nbAnimClips = `getAttr -size ($gGameFbxExporterCurrentNode + ".animClips")`; ' )

print animClips
```

Update Window

```Python
mel.eval('gameExp_CurrentPresetChanged;') # update window
```
