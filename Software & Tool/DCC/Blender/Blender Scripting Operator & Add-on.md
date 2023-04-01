#python 

### [Operator](https://docs.blender.org/api/current/bpy.types.Operator.html) & Add-on

[Tutorial](https://www.youtube.com/watch?v=xscQ9tcN4GI)

 Run code snippet

`import bpy`

##### Add-on Metal Data (Add-on Only)

```Python
bl_info = {
    "name": "My Test Add-on",
    "blender": (2, 83, 0),
    "category": "Object",
} 
```

##### Operator Class

```Python
class HelloWorldOperator(bpy.types.Operator):
    """The Tooltip"""
    bl_idname = "mesh.hello_world" # change the ID address
    bl_label = "Minimal Operator"
    bl_options = { 'REGISTER', 'UNDO' }
    
    Property Definitions ↓
    count_x: bpy.props.IntProperty(
        name = "Int",
        description = "Number of Int",
        #default = 1,
        #min = 1,
        #max = 10
    )
    
    count_y: bpy.props.FloatProperty(
        name = "Float",
        description = "Number of Float",
        default = 1.0
    )
    
    ''' for execute in certain area
    @classmethod
    def poll(cls, context):
        return context.area.type == "VIEW_3D" // only in 3D Viewport area
    '''

    def execute(self, context):
        bpy.ops.mesh.primitive_cube_add()
        print("Hello World" + str(self.count_y))
        return {'FINISHED'} # Tell Blender
```

Operator needs, Add-on doesnt **↓**

```Python
if __name__ == '__main__':
    register()
```

##### UI Class (Optional)

```Python
class VIEW3D_PT_HelloWorld(bpy.types.Panel):
    bl_space_type = "VIEW_3D"
    bl_region_type = 'UI' 
    bl_category = "category" #
    bl_label = "label"

    def draw(self, context):
        pass
```

##### Register & Unregister

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


### [Create an Add-on](https://www.youtube.com/watch?v=nKt6CtMH0no)

Save script as to file | Image 2 | Install thru Preference
---|---|---
![[img/Blender Scripting Operator & Add-on/Save script as to file.png]]|![[img/Blender Scripting Operator & Add-on/text-py.png]]|![[img/Blender Scripting Operator & Add-on/Install thru Preference.png]]

Can use function after enabling the add-on <br/> `import` `fileNameShowAsinImage2` | Reload script after editing the script
---|---
![[img/Blender Scripting Operator & Add-on/Can use function after enabling the add-on.png]] |   ![[img/Blender Scripting Operator & Add-on/Reload script after editing the script.png]]



### Interface

Edit Source to check UI
![[img/Blender Scripting Operator & Add-on/editSource.gif]]

Icon -> find in Icon Viewer (require enable in preference)

  

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