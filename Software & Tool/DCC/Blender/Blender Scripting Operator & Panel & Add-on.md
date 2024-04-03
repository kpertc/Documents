#python 
### Tutorial
- [YouTube - Operator - Scripting for Artist by Blender](https://www.youtube.com/watch?v=xscQ9tcN4GI)
### Operator
https://docs.blender.org/api/current/bpy.types.Operator.html

```Python
class HelloWorldOperator(bpy.types.Operator):
    """The Tooltip"""
    bl_idname = "mesh.hello_world" # change the ID address
    bl_label = "Minimal Operator"
    
    bl_options = { 
	    'REGISTER', 
	    'UNDO', # for undo
	    'DEFAULT_CLOSED' # panel default -> closed
	}

	bl_parent_id = "" # put this panel inside of the parent panel
    
    # Property Definitions ↓
    count_x: bpy.props.IntProperty(
        name = "Int",
        description = "Number of Int",
        #default = 1,
        #min = 1,
        #max = 10 # limit on slider and type
        #soft_max = 10 # # limit on slider, but still can type any value
    )
    
    count_y: bpy.props.FloatProperty(
        name = "Float",
        description = "Number of Float",
        default = 1.0
    )
    
    # for execute in certain area
    @classmethod
    def poll(cls, context):
        return context.area.type == "VIEW_3D" # show only in 3D Viewport area
        # return boolean

    def execute(self, context):
	    # use this context instead of use bpy.context
        bpy.ops.mesh.primitive_cube_add()
        print("Hello World" + str(self.count_y))
        return {'FINISHED'} # Tell Blender
```


``` python
return {'FINISHED'}
return {'RUNNING_MODAL'}
return {'CANCELLED'}
```
##### Modal
https://docs.blender.org/api/current/bpy.types.Event.html

Operator needs, Add-on doesn't **↓**
```Python
if __name__ == '__main__':
    register()
```
### Panel (UI)
```Python
class VIEW3D_PT_HelloWorld(bpy.types.Panel):
    bl_space_type = "VIEW_3D"
    bl_region_type = 'UI' 
    bl_category = "category" #
    bl_label = "label"

    def draw(self, context):
        pass
```

draw ()
``` python
def draw(self, context):
	layout = self.layout
	
	row = layout.row()
	col = layout.column()

	column.separator() # separator

	col.props(obj, "scale") # show obj's scale property in here

	
```

##### Preference
https://docs.blender.org/api/current/bpy.types.AddonPreferences.html

### Register & Unregister

```Python
def register():
    bpy.utils.register_class(HelloWorldOperator) # operator
    bpy.utils.register_class(VIEW3D_PT_HelloWorld) # UI
    
def unregister():
    bpy.utils.unregister_class(HelloWorldOperator) # operator
    bpy.utils.unregister_class(VIEW3D_PT_HelloWorld) # UI

### or Create a list of classes   
blender_classes = [ HelloWorldOperator, HelloWorldOperator ]
    for blender_class in blender_classes:
       bpy.utils.register_class(blender_class)
```

Console type -> `bl_idname` | `F3` Search Bar
---|---
![[img/Blender Scripting Operator & Add-on/hello-world-operator.png]] |![[img/Blender Scripting Operator & Add-on/search-bar.png]] 

Add Input | `bl_options = { 'REGISTER', 'UNDO' }`
---|---
![[img/Blender Scripting Operator & Add-on/add-input.png]]|![[img/Blender Scripting Operator & Add-on/bl_options.png]]


Run the script onload -> usable even when Blender restarted
![[img/Blender Scripting Operator & Add-on/register.png | 300]]

### Interface
open a Text Editor on the side, RMB > `Edit Source` on any UI to show the source code
![[img/Blender Scripting Operator & Add-on/editSource.gif]]

Icon -> find in Icon Viewer (require enable in preference)


``` python
# 
col = self.layout.column(align=True)

# refer other property's UI
self.layout.prop(context.scene.cycles, "preview_samples")

# label
self.label(text="title")
```

### [Props.property](https://docs.blender.org/api/current/bpy.props.html)

`:` Variable Annotation

```Python
myInt : bpy.props.IntProperty()
myFloat : bpy.props.FloatProperty()

myString : bpy.props.StringProperty()
myBool : bpy.props.BoolProperty()

myIntVector : bpy.props.IntVectorProperty()
myFloatVector : bpy.props.FloatVectorProperty()
myBoolVector : bpy.props.BoolVectorProperty()
```

![[img/Blender Scripting Operator & Add-on/Variable Anotation.png | 300]]
  

User Python Mixin class for info that is used in multiple classes
![[img/Blender Scripting Operator & Add-on/User Python Mixin class for info that is used in multiple classes.png]]


### Add ons
Add ons file can be a single `.py` or `.zip` file

##### [YouTube - From Script to Add-on | Scripting for Artists [9]](https://youtu.be/nKt6CtMH0no?si=rW1TlGw3Dha1kj0x)

Save script as to file | Image 2 | Install thru Preference
---|---|---
![[img/Blender Scripting Operator & Add-on/Save script as to file.png]]|![[img/Blender Scripting Operator & Add-on/text-py.png]]|![[img/Blender Scripting Operator & Add-on/Install thru Preference.png]]

| Can use function after enabling the add-on <br/> `import` `fileNameShowAsinImage2`          | Reload script after editing the script                                                  |
| ------------------------------------------------------------------------------------------- | --------------------------------------------------------------------------------------- |
| ![[img/Blender Scripting Operator & Add-on/Can use function after enabling the add-on.png]] | ![[img/Blender Scripting Operator & Add-on/Reload script after editing the script.png]] |


##### Add-on Meta Data (Add-on Only)
[Blender # Add-on Tutorial](https://docs.blender.org/manual/en/latest/advanced/scripting/addon_tutorial.html)

```Python
bl_info = {
    "name": "My Test Add-on",
    "blender": (2, 83, 0),
    "category": "Object",
    ...
    # more info can be found on ↓
    # bl_info https://developer.blender.org/docs/handbook/addons/addon_meta_info/
    
} 
```