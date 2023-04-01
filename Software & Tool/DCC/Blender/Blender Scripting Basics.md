#python 

### Some readings:

Blender is written in C/C++/Python, learn more about: [Reference/FAQ - Blender Developer Wiki](https://wiki.blender.org/wiki/Reference/FAQ)

[[Blender Scripting Operator & Add-on]]

---

### Shortcuts

`Alt` / `Option` + `P` Run Script

`F3` Search Bar

Run Blender thru terminal `/Applications/Blender.app/Contents/MacOS/Blender`

Also allow open multiple Blender on MacOS

---

### Intro

Enable Settings | Tooltips
---|---
![[img/Blender Scripting Basics/Enable Settings.png]]|![[img/Blender Scripting Basics/Tooltips.png]]


Modules are shown on console|`Tab` Auto-Complete| | 
---|---|---
![[img/Blender Scripting Basics/Modules are shown on console.png]] | ![[img/Blender Scripting Basics/Auto-Complete-1.png]] | ![[img/Blender Scripting Basics/pythonConsoleAutoComplete.gif]]

Use Convenience Variable `C` & `D`

  

##### Python console

Windows
![[img/Blender Scripting Basics/Windows-Python-Console.png | 300]]

[Mac](https://www.youtube.com/watch?v=25yvAUhFIoI)

`bpy.app.binary_path`

![[img/Blender Scripting Basics/Blender Module.png]]

---

### Common APIs

`import bpy`

##### Access Objects

  

-   `bpy.data` - all data in your blend file.
    
-   `bpy.context` - data in the current active view. (useful for getting current selecting / active objects)


  

bpy.context

```Python
bpy.context.active_object
bpy.context.selected_objects
bpy.context.scene
bpy.context.selected_pose_bone
...

bpy.context.scene.objects.get('objectName')

for obj in bpy.context.selected_objects:
    print(obj.name)
```

bpy.data

```Python
bpy.data.objects['objectName']
```

Create Primitives

```Python
# Add primitive object
bpy.ops.mesh.primitive_cube_add()
bpy.ops.mesh.primitive_monkey_add(location=(0,0,0))
```

Transform Object

```Python
# Move X = 5
bpy.context.active_object.location[0] = 5

# Rotate X 45 degree
bpy.context.active_object.rotation_euler[0] += radians(45)
```

##### Degree to Radians

```Python
from math import radians
print (radians(45)) # 0.7853981633974483
```

##### Add Modifier

```Python
# Add Subdivision Surface Modifier named 'My Modifier' 
bpy.context.active_object.modifiers.new("My Modifier", "SUBSURF")

# change Levels Viewport
# Require Searching-> inefficient
bpy.context.active_object.modifiers['My Modifier'].levels = 3
```
![[img/Blender Scripting Basics/Add-Modifier.png]]


##### Shade Smooth

```Python
# 1
bpy.ops.object.shade_smooth()

# 2
object = bpy.context.active_object.data
mesh = object.data
for face in mesh.polygons:
    face.use_smooth = True
```

Img-1 Blender default view layer | Img2 <br/>C.scene.collection -> <br/> Scene Collection # Img-2 2
--|--
![[img/Blender Scripting Basics/img-1.png]] | ![[img/Blender Scripting Basics/img-2.png]]


```Python
# list Scene Objects
list(C.scene.objects)
# [bpy.data.objects['Cube'], bpy.data.objects['Light'], bpy.data.objects['Camera']]

# List collection objects
list(D.collections['Collection'].objects)
# [bpy.data.objects['Cube'], bpy.data.objects['Light'], bpy.data.objects['Camera']]
```

```Python
# create new collection
D.collections.new('collectionName')
collectionVar = D.collections.new('collectionName')
collectionVar.name = 'new name' # change the collection name to New Name

#Link & unlink
C.scene.collection.children.link(collectionVar) # Img-2 1
# Parent link to the child
```

  

##### Export

```Python
# MacOS
bpy.ops.export_scene.fbx(filepath = '/Users/bytedance/Desktop/test.fbx') 
```

  

##### Render

```Python
# Change current frame
bpy.context.scene.frame_current = 0

# Switch Camera
bpy.context.scene.camera = cam

# Change Material
_material = bpy.data.materials['materialName']
_object.active_material = _material
```

Hide & UnHide objects

```Python
# hide in Viewport globally
bpy.data.objects['Cube'].hide_set(True) # For Eye icon
bpy.data.objects['Cube'].hide_viewport = True # For monitor icon

bpy.data.objects['Cube'].hide_render = True # hide in Render
```

  

Material

Checking log

  

Render settings and save to file

```Python
# save by render
bpy.context.scene.render.image_settings.file_format = 'PNG' #'EXR'
bpy.context.scene.render.filepath = '/Users/chenjingfu/Desktop/render.png'
bpy.ops.render.render(use_viewport=True, write_still=True)

#save by image ops, save multiple images
bpy.ops.render.render()
image = bpy.data.images['Render Result']
bpy.data.images["Render Result"].save_render("C:/Users/Admin/Desktop/image.jpg")
```

Output

```Python
bpy.context.scene.render.resolution_x = 2048
bpy.context.scene.render.resolution_y = 2048
bpy.context.scene.cycles.samples = 1024
```

  

---

### Custom Properties

bpy.types.Scene.mass_import = bpy.props.StringProperty() # Create a new attribute

  

# Test in Console will show

C.scene.mass_import

C.scene,mass_import = "1111"

![[img/Blender Scripting Basics/Custom Properties.png | 300]]