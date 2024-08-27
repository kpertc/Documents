#python 
### Tutorial
- [YouTube - Operator - Scripting for Artist by Blender](https://www.youtube.com/watch?v=xscQ9tcN4GI)
- [YouTube - Addon - Scripting for Artist by Blender](https://youtu.be/nKt6CtMH0no?si=rW1TlGw3Dha1kj0x)
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
        # return boolean
        return context.area.type == "VIEW_3D" # show only in 3D Viewport area
        return context.active_object is not None

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

##### Use Operator
1. In Script
```python
bpy.ops.{bl_idname()}
```
3.  In command, press `F3` type `bl_idname`
	![[blender-search-operator.png|200]]
2. In Panel
	 ![[blender-operator-panel.png|200]]
``` python
# operator
class PE_OT_test(bpy.types.Operator):
	bl_idname = "pe.test" # 小写
	...

# panel
class VIEW3D_PT_pixel(bpy.types.Panel):
	bl_space_type = 'VIEW_3D'
	bl_region_type = 'UI' # side bar
	...
	
	def draw(self, context):
		...
		self.layout.operator("pe.test", text="operator button") # operator Id in string
```

Custom UI Properties → Property Definitions 
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

	# 
	col = self.layout.column(align=True)
	
	# refer other property's UI
	self.layout.prop(context.scene.cycles, "preview_samples")
	col.props(obj, "scale") # show obj's scale property in here
	
	# simple label
	self.label(text="title")
	
	# separator
	column.separator()

	split

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
```

For script
```python
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


User Python Mixin class for info that is used in multiple classes
![[img/Blender Scripting Operator & Add-on/User Python Mixin class for info that is used in multiple classes.png]]


### Add ons
Add ons file can be a single `.py` or `.zip` file
to create a package addon (`.zip`), rename the entry python file to `__init__.py` and zip the path
single script addon named `__init__.py` with not work

| Save script as to file                                                  | Image 2                                                  | Install thru Preference                                                  |
| ----------------------------------------------------------------------- | -------------------------------------------------------- | ------------------------------------------------------------------------ |
| ![[img/Blender Scripting Operator & Add-on/Save script as to file.png]] | ![[img/Blender Scripting Operator & Add-on/text-py.png]] | ![[img/Blender Scripting Operator & Add-on/Install thru Preference.png]] |
|                                                                         |                                                          |                                                                          |

Installed addons directory: `addon_dir="${HOME}/Library/Application Support/Blender/${version}/scripts/addons"`

| Can use function after enabling the add-on <br/> `import` `fileNameShowAsinImage2`          | Reload script after editing the script                                                  |
| ------------------------------------------------------------------------------------------- | --------------------------------------------------------------------------------------- |
| ![[img/Blender Scripting Operator & Add-on/Can use function after enabling the add-on.png]] | ![[img/Blender Scripting Operator & Add-on/Reload script after editing the script.png]] |

##### Add-on Meta Data (Add-on Only)
[Blender # Add-on Tutorial](https://docs.blender.org/manual/en/latest/advanced/scripting/addon_tutorial.html)

plugin name showed at Add ons list is `{bl_info.category} {bl_info.name}`

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


Update Add-on
```python
# uninstall addon
bpy.ops.preferences.addon_remove(module='blender-test') # dir name

# install addon
installFilePath = '/Users/userName/Desktop/blender-test.zip'
bpy.ops.preferences.addon_install(overwrite=True, filepath=installFilePath)
bpy.ops.preferences.addon_enable(module='blender-test')
```


### Property Definitions
[Blender Docs - Props.property](https://docs.blender.org/api/current/bpy.props.html)

 pop up properties when run the operator

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

```python
text = bpy.props.StringProperty(name="default text", default="default name")
...
object.name = self.text
```

![[img/Blender Scripting Operator & Add-on/Variable Anotation.png | 300]]
  