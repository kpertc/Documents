#python 

Check out templates
![[templates.png|300]]
### Some readings:

Blender is written in C/C++/Python, learn more about: [Reference/FAQ - Blender Developer Wiki](https://wiki.blender.org/wiki/Reference/FAQ)

[[Blender Scripting Operator & Panel & Add-on]]

---
### Shortcuts

`Alt` / `Option` + `P` Run Script
`F3` Search Bar

---
### Command line

Run Blender thru terminal `/Applications/Blender.app/Contents/MacOS/Blender`
Also allow open multiple Blender on MacOS

[Blender Documentation - Command Line](https://docs.blender.org/manual/en/latest/advanced/command_line/index.html#)

Video Tutorial: [YouTube - Running Blender from the Terminal on macOS by CG Python](https://youtu.be/eoQX_Q1IGzg?si=uylYo-c4WRQNvfDI)

``` shell
cd /Applications/Blender.app/Contents/MacOS

./Blender # run Blender normally
./Blender --help # Run Blender with commands
```

Run Blender & Delete default cube & load a `.glb` mode from terminal
using typescript
``` ts
const blenderProcess = spawn(blenderPath, [
"--python-expr",
// keep python code unindented !!
`
import bpy
bpy.ops.object.delete() # delete the default cube
bpy.ops.import_scene.gltf(filepath='${modelPath}') # load glb model

`,]);

blenderProcess.stdout.on("data", (data) => {
	console.log(`Blender STDOUT: ${data}`);
});
```

Close the terminal will also close the Blender

``` shell

```

---
Python Version
![[Blender-Python-version.png]]

---
### Intro

| Enable Settings                                       | Tooltips                                       |
| ----------------------------------------------------- | ---------------------------------------------- |
| ![[img/Blender Scripting Basics/Enable Settings.png]] | ![[img/Blender Scripting Basics/Tooltips.png]] |

| Modules are shown on console                                       | `Tab` Auto-Complete                                   |                                                                 |     |
| ------------------------------------------------------------------ | ----------------------------------------------------- | --------------------------------------------------------------- | --- |
| ![[img/Blender Scripting Basics/Modules are shown on console.png]] | ![[img/Blender Scripting Basics/Auto-Complete-1.png]] | ![[img/Blender Scripting Basics/pythonConsoleAutoComplete.gif]] |     |
Use Convenience Variable `C` & `D`

##### Python console

Windows
![[img/Blender Scripting Basics/Windows-Python-Console.png | 300]]

[Mac](https://www.youtube.com/watch?v=25yvAUhFIoI)

1. `bpy.app.binary_path` to show current Blender path
2. Make alias (快捷方式, 替身) for future use

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

Hide & UnHide objects
```Python
# hide in Viewport globally
bpy.data.objects['Cube'].hide_set(True) # For Eye icon
bpy.data.objects['Cube'].hide_viewport = True # For monitor icon

bpy.data.objects['Cube'].hide_render = True # hide in Render
```

Texture
```python
# Create Texture (distortd noise) 
new_texture = bpy.data.textures.new("My Texture", "DISTORTED_NOISE")

# Edit texture property
new_texture.noise_scale = 2.0
```

Material
```python
_material = bpy.data.materials['materialName']

# Create Material
_material = bpy.data.materials.new(name = "My Material")

_obj.active_material = _material

# add & append material to object
_obj.data.materials.append(_material)
```

Material - node
```python
# material node
_material.use_nodes = true
nodes = _material.node_tree.nodes

# get node
material_output = nodes.get("Material Ouput") # get node name

# create a node
node_emission = nodes.new(type="ShaderNodeEmission") # Create a emission node

# Edit Node value
# node → array
node_emission.input[0].default_value = ( 0.0, 0.3, 1.0, 1.0 ) # color
node_emission.input[1].default_value = 500.0

#
links = _material.node_tree.links

# create a link
links.new(node_emssion.output[0], material_ouput.input[0]) 
```
##### Add Modifier
```Python
# Add Subdivision Surface Modifier named 'My Modifier' 
_obj.modifiers.new("My Modifier", "SUBSURF")

_obj.modifiers.new("My Modifier", "DISPLACE") # displacement modifier

# change Levels Viewport
# Require Searching-> inefficient
_obj.modifiers['My Modifier'].levels = 3
```
![[img/Blender Scripting Basics/Add-Modifier.png|200]]
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

##### Mesh
https://docs.blender.org/api/current/bpy.types.Mesh.html#bpy.types.Mesh

```Python
obj.name
obj.data # mesh data

obj.data.vertices
obj.data.loops
obj.data.polygons
```

```Python
face_count = len(obj.data.polygons)
triangle_count = len(obj.data.loop_triangles)

print(f'name: {obj.name}, face:{face_count}, triangle: {triangle_count}')
```
###### BMesh
https://docs.blender.org/api/current/bmesh.html

``` python
import bmesh

# create a bmesh
me = obj.data
bm = bmesh.new()

bm.from_mesh(me)


for v in bm.verts:
    v.link_edges
    v.link_loops
    v.link_faces
    
    v.index
```
##### Export

```Python
# MacOS
bpy.ops.export_scene.fbx(filepath = '/Users/userName/Desktop/test.fbx') 
```

### Render
```Python
# Change current frame
bpy.context.scene.frame_current = 0

# Switch Camera
bpy.context.scene.camera = cam
```
  
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


### Math
##### Degree to Radians
```Python
from math import radians
print (radians(45)) # 0.7853981633974483
```

---
### Custom Properties
```python
bpy.types.Scene.mass_import = bpy.props.StringProperty() # Create a new attribute
```


  

# Test in Console will show

C.scene.mass_import

C.scene.mass_import = "1111"

![[img/Blender Scripting Basics/Custom Properties.png | 300]]

### Command Line
https://docs.blender.org/manual/en/latest/advanced/command_line/index.html#


Change viewport shading type
```python
# 切换窗口到material模式
for window in bpy.context.window_manager.windows:
	for area in window.screen.areas: # iterate through areas in current screen
		if area.type == 'VIEW_3D':
			for space in area.spaces: # iterate through spaces in current VIEW_3D area
				if space.type == 'VIEW_3D': # check if space is a 3D view
					space.shading.type = 'MATERIAL'
```