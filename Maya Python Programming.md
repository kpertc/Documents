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
### Object Path

```py
path = cmds.ls('boot_wiper', long=True)
print path
#['|Car|Car_Trunk|Trunk_Body|boot_wiper'] #type List
```
### Control Cube

```py
myCube = 'pCube1'

cmds.getAttr('pCube1.translateX')
cmds.setAttr('pcube1' + '.translateX', 1)

cmds.xform( 'object', ro=(x, y, z) )
```

### Radians Degrees Convert

```py
degrees = math.degrees(radians)
radians = math.radians(degrees)
```

### Grouping

```py
https://download.autodesk.com/us/maya/2009help/commandspython/group.html

#把物体层级移到 新建的组
cmds.group( em=True, name='groupName' )
cmds.group( 'circle1', 'sphere1', n='group1' ) #n short for name

#把物体层级移到一个位置
cmds.parent( 'pCube2', 'null2' ) #物体，要到的位置
```

### Move Pivot Point to World Center

```py
cmds.move(0, 0, 0, 'pCube1' + '.scalePivot', 'pCube1' + '.rotatePivot', absolute=True);

#选择全变
selection = cmds.ls(selection=True)

for selected in selection:
    cmds.move(0, 0, 0, selected + '.scalePivot', selected + '.rotatePivot', absolute=True);
```

### Freeze Transformation

```py
#根据物体名字 Freeze
cmds.makeIdentity('pCube1', apply=True)

#选择物体 Freeze
selection = cmds.ls(selection=True)

for selected in selection:
    cmds.makeIdentity(selected, apply=True) #ALL
    
    
  # cmds.makeIdentity(selected, translate=True)
  # cmds.makeIdentity(selected, rotate=True)
  # cmds.makeIdentity(selected, scale=True)
```

### UV

```py
#move UV
cmds.polyEditUV(u=0.0, v=-0.1)
```

### UV Set

### Delete

```py
#检测物体存在
if cmds.objExists('pCube1'):

#删除物体
cmds.delete('pCube1')

#删除历史
cmds.delete('pCube1', constructionHistory = True)
```

### MEL in Python

```mel
import maya.mel as mel
mel.eval()
```

### Create Layers

```py
#Check if the layers exists

#Creating Layers in the order
cmds.createDisplayLayer(name='ChromePlastic_L')

#Set Color
cmds.setAttr ('int_L.color', 3) 
```

### Select Object By Material

```py
def selectObjectbyMaterial (materialName)
    cmds.hyperShade(objects= materialName)
```

### Animation Keys

```py
# set Key
cmds.setKeyframe('object', v= value, at='attribute', t = time)

# Delete Keys
cmds.cutKey('object', s=True)

cmds.cutKey('object', cl = True)
```

### Current Unit

```py
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

### Linear Unit

```


https://help.autodesk.com/cloudhelp/2019/ENU/Maya-Tech-Docs/CommandsPython/currentUnit.html
```

### Playback

```py
cmds.currentTime( 0 )

cmds.playbackOptions( minTime=0, maxTime = 10 )
```

### Evaluation

```py
print (cmds.polyEvaluate( b=True )) #Bouding box

print (cmds.polyEvaluate( t=True )) #Triangle
```

### Material

```py
#Create New Material
cmds.shadingNode("phong", asShader=True, name="myMaterial")

#Create File Node
cmds.shadingNode("file", asTexture=True, name="myImageFile")

#Connect Image Node to Material Color
cmds.connectAttr('filePathImage.outColor', 'myShader.color')

#image Path -> String
imagePath = '/Users/chenjingfu/Desktop/DJI_0088.png'

cmds.setAttr('filePathImage.fileTextureName', imagePath, type="string")


#select Object and assign
selection = cmds.ls(selection=True)
cmds.hyperShade(selection, assign = 'blinn1') #material Name

#Check if the material exists
if cmds.objExists('blinn1'):
    print('Exist')
    
#Get materials
Materials = cmds.ls(materials=True)
```

https://medium.com/graphic-programming/create-texture-to-the-material-ef6f40d19e28

```py
#Set Default Color
def setMaterialColor(materialName,r,g,b):
    
    if cmds.objExists(materialName):
        cmds.setAttr(materialName + '.color', r,g,b, type="double3")

Car_Paint_shader = ['Car_Paint_shader',0.3,0.14,0]  
Car_Leather_shader = ['Car_Leather_shader',0.34,0.12,0.1]     
Car_Cloth_shader = ['Car_Cloth_shader',0.12,0.22,0.12] 

setMaterialColor(Car_Paint_shader[0],Car_Paint_shader[1],Car_Paint_shader[2],Car_Paint_shader[3])
```

### Open Web or File

```py
cmds.launch(web="http://www.autodesk.com")
cmds.launch(directory="C:/matemp")
```

# Arnold Render

### Render to Texture

```py
cmds.arnoldRenderToTexture(folder='C:/Users/Admin/Desktop/', resolution=2048, aa_samples=5)
```

# GameExporter

```py
# Open GameExporter
mel.eval('gameFbxExporter;') 
```

![](https://bytedance.feishu.cn/space/api/box/stream/download/asynccode/?code=YWFkZmYzZTI3NDE1YTI1NzQ5NWIyZmQ3MDFmMjE4NGJfcVcyUjQyd1dPNmlzM1ZFc1lxZTA3NksxZW50YU12Z1FfVG9rZW46Ym94Y25lbzNoZ0F4NlBFOEw3NzBVMThJdnZBXzE2NjY1MDY3ODg6MTY2NjUxMDM4OF9WNA)

```py
# Switch Tabs  1 Model Tab  2 Animation Tab
mel.eval('gameExp_ChangeExportType(2)') # Switch to Animation Tab
```

Get Presets

```py
# get all presets list
list = mel.eval('gameExp_GetGameFbxExporterNodeList;') # Get all Presets

# get current preset name
_p = str(mel.eval("$temp=$gGameFbxExporterCurrentNode")) # Convert MEL to Python
```

Get Animation Clips Size

```py
animClips = mel.eval( 'int $nbAnimClips = `getAttr -size ($gGameFbxExporterCurrentNode + ".animClips")`; ' )

print animClips
```

Update Window

```py
mel.eval('gameExp_CurrentPresetChanged;') # update window
```