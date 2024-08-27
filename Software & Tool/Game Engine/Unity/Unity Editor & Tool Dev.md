#C＃ #Unity 


Unity frequently codes of commands, shortcuts, and summarized problems

### Tutorials

[Freya Homer](https://www.youtube.com/watch?v=pZ45O2hg_30&t=2674s)
[Catlike Coding Editor](https://catlikecoding.com/unity/tutorials/editor/)

[GameGrind Attribute Tutorial [Youtube]](https://www.youtube.com/watch?v=fxHOfV3yM9o&t=248s)

# Common Codings

### Attributes

Unity [PropertyDrawer](https://docs.unity3d.com/ScriptReference/PropertyDrawer.html) and [DecoratorDrawer](https://docs.unity3d.com/ScriptReference/DecoratorDrawer.html)

```C#
// MultipleAttribute
[attribute1, attribute2]

[ExecuteAlways] / [ExecuteInEditMode] // 在编辑器环境运行Mono脚本
[DisallowMultipleComponent] // Prevents MonoBehaviour of same type (or subtype) to be added more than once to a GameObject. 
[RequireComponent(typeof(Rigidbody))]
[Obsolete] / [Obsolete("此方法不可用，请使用其他方法")]//标记该方法已弃用 / 标记本文

// PropertyDrawer ↓ 
Int & Float - [Range(1, 6)] / [Range(0.2f, 0.8f)]
String - [Multiline] / [TextArea]

// DecoratorDrawer ↓ 
[Header("标题")] / [Space] or [Space(10)]

// Hiding
[ReadOnly] // Show, but not editable
[HideInInspector] // Hide, not show

// Help
[Tooltip("Any Description")] // Single Property Help
[HelpURL("http://example.com/docs/MyComponent.html")] // Class Help

// Add to Menu
[MenuItem("MyMenu/Do Something")] // add editor window / static function also can add shortcur
[AddComponentMenu("Transform/Follow Transform")] // 把component加入到菜单
[ContextMenu("")]

//Scriptable Object
[CreateAssetMenu]
```

##### Options

<br>

### Serialization

```C#
public float thing0; // serialized, visible, public
float thing1; // not serialized, hidden, private
[SerializedField] float thing2; // serialized, visible, private
[HideInInspector] public float thing3; //serialized, hidden, public

//Serializable Class or Struct
[Seriablizable]
public class MyClass {
    public Vector3 pos;
    public Color color;
}
```

Inheritance wont get serialized

Protected: A protected member is accessible within its class and by derived class instances.

<br>

### UI部分 - Layout & Styling

##### **[Immediate Mode GUI (IMGUI)](https://docs.unity3d.com/Manual/GUIScriptingGuide.html)**

```C#
//Explicit positioning using Rect
GUI
EditorGUI

//Implicit positioning, auto-layout
GUILayout
EditorGUILayout
```

Examples

```C#
//Label
GUILayout.Label("TextHere", EditorStyles.boldLabel);
//Button
if (GUILayout.Button("按钮名称", GUILayout.Height(30)))
//Space
EditorGUILayout.Space(10);
//
GUILayout.BeginHorizontal();
GUILayout.EndHorizontal();

//Tab
string[] toolbarStrings = new string[] { "初始化", "美术工具", "白模导出", "开发测试"};

toolbarInt = GUI.Toolbar(new Rect(3, 3, position.width - 6, 25), toolbarInt, toolbarStrings);

//缩进
EditorGUI.indentLevel++; //Only for EditorGUI
EditorGUI.indentLevel--;
```

##### Style [Example](https://www.xuanyusong.com/archives/3860)

  

##### UI Element (UI Toolkit)
![[img/Unity Editor & Tool Dev img/UI-Toolkit.png]]


UI Toolkit samples and Debugger

  

##### Creating Properties

```C#
public string[] stringArrayExmple; // 
public List<string> stringListExample; // 
```

<br>  


### Editor Window Operations
https://docs.unity3d.com/ScriptReference/Editor.OnInspectorGUI.html

### Editor & Window

##### Editor Template → Script Attach on GameObject [Editor Example](http://www.vmetu.com/blog/unity-editor-zi-ding-yi-chuang-kou.htmlE)

```C#
public class ExampleScript : MonoBehaviour {
    public float value = 7.0f;
}

[CustomEditor(typeof(ExampleScript))] // A tiny custom editor for ExampleScript component
public class ExampleEditor : Editor {
    
    public override void OnInspectorGUI() {
    
        var t = target as ExampleScript; // reference 
    
        base.OnInspectorGUI(); //Original Properties
        // UI Stuff Here
    }
    
    protected virtual void OnSceneGUI(){
        // do Handle Stuff
        Handles.BeginGUI();
        if (GUILayout.Button("Button", GUILayout.Width(100))) {
            // do Stuff
        }
        Handles.EndGUI();
}
```

##### EditorWindow Template → Independent Window [EditorWindow Lifecycle](http://www.4k8k.xyz/article/qq_28474981/82949820)

```C#
[MenuItem("Custom/Custom  %#]")]
public class EditorWindowExample : EditorWindow {
    static void Init() => GetWindow<CustomEditor>("The Title");
    void OnGUI() {
        // UI Stuff Here
    }
}
```

<br>

// events...

##### OnSelectionChanged

<br>

##### Window Update

```C#
EditorUtility.FocusProjectWindow(); // Focus window

OnGUI // Only event
OnInspectorUpdate()  // Update per 10 frame, less times as if it was OnGUI/Update
OnValidate() //Editor-only function that Unity calls when the script is loaded or a value changes in the Inspector.
repaint() // re-draw ?
```

##### SerializedProperty [Example](https://www.jianshu.com/p/fde1ea2c0337)

```C#
SerializedProperty theName;
theName = serializedObject.FindProperty("nameInMonoBehaviour");
```

<br>

### Draw Graphic

Gizmo, Handles, Graphics, GL ...

<br>

### Gizmo

> Gizmos are used to give visual debugging or setup aids in the Scene view. - [Unity Gizmos](https://docs.unity3d.com/ScriptReference/Gizmos.html)=

Using UnityEngine

-   OnDrawGizmos → Draw every frame
-   OnDrawGizmosSelected → Only Draw when selected

```C#
Gizmos.DrawIcon //Draw Icon, require Gzimo Folder
```

```Plaintext
//Draw Local Direction
Gizmos.DrawLine(transform.position, transform.position + transform.forward * 10);
```

<br>

### Handles

> Custom 3D GUI controls and drawing in the Scene view. - [Unity Handles](https://docs.unity3d.com/ScriptReference/Handles.html)

Using UnityEditor

```C#
//Drawing Order
Handles.zTest = UnityEngine.Rendering.CompareFunction.LessEqual;
```
[Handle.zTest](https://docs.unity3d.com/ScriptReference/Handles-zTest.html)

  
<br>
  

### Undo

```C#
Undo.RecordObject(gameobject.transform, "Layout");
```

<br>
  

### Material

material vs shared material same for mesh / shared mesh

```C#
GetComponent<MeshRenderer>().material.color = Color.Red; //Duplicate / Instance the material
GetComponent<MeshRenderer>().sharedMaterial.color = Color.Red; //Modify the material asset
```

Hideflags - To prevent material leak, and properly create material, use Hideflag

```C#
Shader shader = shader.Find("Default/Diffuse");
Material mat = new Material(shader) {hide flags = HideFlags.HideAndDontSave };
mat.hideFlags = HideFlags.HideAndDontSave;
```

Use ID access material is much faster

Material Property Block

```C#
MaterialPropertyBlock mpb;
```

  
<br>

### Assembly Definition  

```C#
#if UNITY_EDITOR
     // do something
#endif
```

<br>
  

### Raycast

https://docs.unity3d.com/ScriptReference/Camera.ScreenPointToRay.html

  

### [Event](https://docs.unity3d.com/ScriptReference/Event.html) [EventType](https://docs.unity3d.com/ScriptReference/EventType.html)

```C#
void OnGUI() {
    if (Event.current.type != EventType.Repaint && Event.current.type != EventType.Layout) {
        Debug.Log("Current event detected: " + Event.current.type);
    }
}
```

### ClearLog

```C#
public void ClearLog() {
    var assembly = Assembly.GetAssembly(typeof(UnityEditor.Editor));
    var type = assembly.GetType("UnityEditor.LogEntries");
    var method = type.GetMethod("Clear");
    method.Invoke(new object(), null);
}
```

  

# Knowledge

### [Unity Execute Order](https://docs.unity3d.com/Manual/ExecutionOrder.html)

-   Awake - when the script load even if the script is not enabled
    
-   OnEnable / OnDisable

### delegate `Action` VS `Funcs`


> [!info]
> **`Action`**
>	delegate with ==void return type==, ==no parameters==
>	
>**`Action<T>`****,** **`Action<T1, T2>`**, and so on
> delegate with ==void return type==, ==cutstom parameters==
>
>**`Func<T>`**
>delegate with ==custom return type==, ==no parameters==
>
>**`Func<T1, T2>`**, **`Func<T1, T2, T3>`**, and so on:
>delegate with ==custom return type==, ==custom parameters==

  

### Destroy() vs Destroy immediate()

> [!info]
>Destroy(): Destroy the gameobject at the end of a frame
>DestroyImmediate(): Execute destroy the gameobject immediately.

  

### AssetDatabase vs Resource.Load

> [!info]
>`AssetDatabase.LoadAssetAtPath()`. The `AssetDatabase.LoadAssetAtPath()` function came from the `UnityEditor` namespace which is only used to make Editor plugins. It won't work outside the Editor and it won't even let you build your game at-all.
>
>You using `Resource.Load` is fine but `Resource.Load` requires the use of the Resources folder which is known to slow down loading time of the game.

  <br>

### [Unity Speical Folders](https://docs.unity3d.com/Manual/SpecialFolders.html)

![[img/Unity Editor & Tool Dev img/Unity-special-folder.png]]

<br>

### Saving Data Between Sessions

Save Simple, editor value → **[PlayerPrefs](https://docs.unity3d.com/ScriptReference/PlayerPrefs.html)**
Save complex, scene → **[JSON](https://docs.unity3d.com/ScriptReference/JsonUtility.html)**
CSV or XML ？

<br>

# Practice

### Basic Useful Function

[Quaternion](https://docs.unity3d.com/ScriptReference/Quaternion.html).LookRotation

```C#
//Rad to Vector2
Vector2 AngleToDir( float angRad ) {
    return new Vector2( Mathf.Cos( angRad ), Mathf.Sin( angRad ));
}    
```

```C#
//Vector2 to Rad
float DirToAng( Vector2 v ) {
    return Mathf.Atan2( v.y, v.x );
}
```

# Advanced

### **WYSIWYG** (What You See Is What You Get) 所见即所得