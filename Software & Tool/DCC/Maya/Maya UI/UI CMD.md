#python #UI

Using PySide in Maya → [[PyQT-PySide]]

[Maya Python Interface PySide](https://bytedance.feishu.cn/docx/Ba2ZdRpRbovkvLxvVSecP89fnbh)

https://help.autodesk.com/view/MAYAUL/2020/ENU/index.html?contextId=COMMANDSPYTHON-INDEX

### New Window Template

```python
from maya import cmds

winName = 'windowName'

# check window exist base on window
if cmds.window(winName, exists = True) == True:
    cmds.deleteUI(myWindow)
    
# create window
myWindow = cmds.window(winName, resizeToFitChildren=True)

cmds.rowColumnLayout(numberOfColumns=1)

# add UI Content Here

cmds.setParent( '..' )

cmds.showWindow(myWindow)
```

### Common Components Samples

```python
Python Variables
# create the UI
# get the Value

cmds.text(label = 'This is a label')
cmds.button(label = 'This is a button', command = functionName)
cmds.separator(height=5)

most of these component types has Grp option that include a prefix text

checkBox = cmds.checkBox(label = 'This is a CheckBox')
cmds.checkBox(checkBox, query=True, value = True)

intField = cmds.intField()
cmds.intField(intField, query=True, value = True))

textField = cmds.textField(text = 'Sample Text')
cmds.textField(textField, query = True, text = True )

scrollField = cmds.scrollField( editable=False, wordWrap=True, text='Non editable with word wrap' )
cmds. scrollField(scrollField, query = True, text = True ) # query
cmds.scrollField(scrollField , edit=True, text = "Edited Text") # 

int / float slider

intSlider = cmds.intSlider(minValue=1, maxValue=6, value=0 )
cmds.textField(intSlider, query = True, text = True )
```

Float slider
![[UI CMD img/float-slider.png]]

```python
# Create
_slider = cmds.floatSlider( minValue=0, maxValue=1, w=100, value=initValue, dragCommand= lambda x: customFunction() )

# Read value
sliderValue = cmds.floatSlider( _slider, q=1, v=1 )
```

```python
# control attribute value
cmds.attrControlGrp( attribute=f'{BSNode}.{name}' )
```

```python
cmds.progressBar(maxValue=10, width=300)
```

### FilePath

```python
path = ''

def getPath():
    print(*args)
    global path
    path = cmds.fileDialog2(fileMode=2, dialogStyle=1, caption="Choose Data Path")[0].replace('\\', '/')
    #print(path)

    # check the folder
    if os.path.isdir(imageFolderPath): # check folder is correct
        for folder in os.listdir(path):
           ...
    else:
        print (f"Path is not correct")
```

```python
fileText = cmds.text(label=path, align='left')
cmds.button(label='Set Data Path', command= lambda: getPath())
```

### Layout

[ColumnLayout](https://help.autodesk.com/cloudhelp/2020/ENU/Maya-Tech-Docs/CommandsPython/columnLayout.html)
[RowColumnLayout](https://help.autodesk.com/cloudhelp/2020/ENU/Maya-Tech-Docs/CommandsPython/rowColumnLayout.html)

```python
# Horizontal
cmds.rowColumnLayout(numberOfColumns=3)

cmds.button(label='照片', width=winWidth / 3, command=web_carPhoto_Page)
cmds.button(label='车系', width=winWidth / 3, command=web_serise_Page)
cmds.button(label='3D', width=winWidth / 3, command=web_3Dview_Page)

cmds.setParent('..')
```

Tab Layout

```python
# Tab layout
cmds.tabLayout( tabs, edit=True, tabLabel=((child1, 'Full Spherical'), (child2, 'Latitude Range')))
```

### Finished Code
[Maya UI Layout Example](http://patrickvfx.blogspot.com/2017/07/maya-ui-layout-example.html)

https://sodocumentation.net/maya/topic/7627/creating-maya-ui

[Maya窗口UI汇总 – 小静的博客](https://smilejing.cn/archives/98)

### UI Showcase
component|Image|Code
---|---|---
textScrollList||`cmds.textScrollList( _textScrollList, q=1, selectItem=1)`
canvas|![[UI CMD img/canvas.png \| 100]]|
componentBox|![[UI CMD img/componentBox.png \| 100]]|
falloffCurve|![[UI CMD img/falloffCurve.png \| 100]]|
gradientControl|![[UI CMD img/gradientControl.png \| 100]]|
CommandLine|![[UI CMD img/CommandLine.png \| 100]]|
cmdShell|![[UI CMD img/cmdShell.png \| 100]]|
layerButton|![[UI CMD img/layerButton.png \| 100]]|
Helpline|![[UI CMD img/Helpline.png \| 100]]|
palettePort|![[UI CMD img/palettePort.png \| 100]]|
radioButton|![[UI CMD img/radioButton.png \| 100]]|`cmds.radioButton( label='One' )`
radioButtonGrp|![[UI CMD img/radioButtonGrp-1.png \| 100]]<br><br>![[UI CMD img/radioButtonGrp-2.png \| 100]]|
shelfButton|![[UI CMD img/shelfButton.png \| 100]]|
switchTable|![[UI CMD img/switchTable.png \| 100]]|
scriptTable|![[UI CMD img/scriptTable.png \| 100]]|
separator|![[UI CMD img/separator.png \| 100]]|
<br> |![[UI CMD img/unknown.png \| 30]]| <br>
symbolButton|![[UI CMD img/symbolButton.png \| 30]]|`cmds.symbolButton( image='circle.png' )`
symbolCheckBox|![[UI CMD img/symbolCheckBox.png \| 30]]|`cmds.symbolCheckBox( image='circle.png' )`
soundPopup|![[UI CMD img/soundPopup.png \| 15]]|`cmds.soundPopup()`
timeField|![[UI CMD img/timeField.png \| 100]]|`cmds.timeField()`
treeLister|![[UI CMD img/treeLister.png \| 100]]|
hudSlider<br>hudButton|![[UI CMD img/hudSlider.png \| 100]]|



