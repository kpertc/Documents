#C＃ #Unity #CG 

Clean Scripting and performance optimization

### Profiling/Debug Tools

##### Unity Tools:

-   Profiler
-   Memory Profiler (Separate Package)
-   Frame Debugger → Draw Call

##### Extra Tools:

-   Instruments XCode
-   Visual Studio
-   Intel Graphics Performance Analyzer (GPA)
-   Intel VTune Profiler
-   RenderDoc
-   Unity Build Report Tool
-   Android Debug Bridge (adb)

##### Memory Leak:

In computer science, a memory leak is a type of resource leak that **occurs when a computer program incorrectly manages memory allocations in a way that memory which is** **no longer needed is not released**. A memory leak may also happen when an object is stored in memory but ==cannot be accessed by the running code==.

**Stack**

Stack overflow

**Heap**

``` csharp
New Object();
Destroy();
```

-   Constantly creating and destroying objects will leave unused memory to Garbage Collector after one update.
    

### General Tips

1.  ##### 
    
    Choosing the right data structure
    
2.  ##### 
    
    Object Pooling
    
    1.  Not creating / deleting objects constantly
        
    2.  Instantiate objects before using
        
    3.  Recycle objects → hide and restore
        
    4.  The size of the pool
        
3.  ##### 
    
    Scriptable Objects
    
    1.  MonoBehaviour → Every data is unique
        
    2.  Scriptable Object → Share the same data even with thousands of copy


```
public class EnemyConfiguration : ScriptableObject
{
    public float m_MaxSpeed;
    public float m_RadiusAttack;
}

public class Enemy : MonoBehaviour
{
    public EnemyConfiguration m_EnemyConfigurationl;
}

```

4.  ##### Define Symbol / Preprocessing Directive
    
    1.  Development Build → Can get Variables or Properties
    2.  Other Build → Can not for optimization purpose
		![[Define Symbol.png | 400]]

5.  ##### The Resources folder
    
    1.  Every file in Resources folder will bundle increasing `<header>` → slow start time
    2.  Use the Addressable Assets package instead
6.  ##### Remove empty Unity Events
    

``` csharp
// Start is called before the first frame update
void Start()
{

}

//Update is called once per frame
void Update()
{

}
```

1.  Empty function consumes resource

7.  ##### Avoid heavy logic on Start() / Awake()
    
    1.  default script template can be changed
8.  Hash the value instead

<br>

## Dots → Data Oriented Technology Stack

AKA (Jobs System)

Boost performance by Multi threads

>[!info]
>- C# Jobs system → for easy multi-threads code
>- Entity Component System → Better Memory Management
>- Handle logic and Data separately
>- Component holds data, and system process function all together?
>- Burst Compiler → compiles to optimized machine code

<br>

## Asset importing Tips

##### Texture Import Settings

-   Max Size to Minimum
-   POT or Atlas
-   Remove Alpha Channel
-   Read/Write Enable []
-   16bit Color Format over 32bit
-   Disable Mipmaps for UI

##### Mesh Import Settings

-   Mesh Compression
-   Read/Write Enable []
-   Rig []
-   Blendshapes []
-   Normals and Tangents

<br>

# Graphics

In the Quality Setting reduce some samples/quality/resolution

Light Hard Shadow → Soft Shadow

## Bake/Generate Dynamic → Static

>[!info]
>- Reflection Probe
>- Light Probe
>- Lightning Map
>- Occlusion

Generate compress texture
Culling distance / occlusion

<br>

## Shadow / Light

>[!info]
>- Shadow Setting, resolution / Distance
>- Shadow mapping technique - shadow map -> resolution

## Texture Compression + Mip Maps

On texture setting, generate Mip map of a smaller version of the texture

## Combine Meshes/Enable Batching

<br>

### Get Component
`GetComponent<T>()` > ≈ `GetCompnent(typeof(T))` > `GetComponent(String)`

<br>

### Avoiding frequent accessing

``` csharp
_transform = transfrom;
_originalPosition = _transform.position;
_originalRotation = _transform.rotation;
```

Cache all info in Awake() Binding
Then Execute in Start() Configuration

<br>

`gameObject.tag == "Player"`
Much less memory: `gameObject.CompareTag("Player")`

<br>

Slow: `If (gameObject != null)`
Faster: `If (! System.Object.ReferenceEquals( gameObject, null ))`

Guard Clause, exit condition early, avoiding

```csharp
if (!condition) return;  
```

<br>

## Code

Reduce update / fixed update / late update

<br>

## Anti-Aliasing 抗锯齿

_Sample_

* SSAA 超级采样
* MSAA 多重采样 -> 只在边缘
* CSAA CFAA

…

_Post 后期处理（模糊）_

## * FXAA 快速近似抗锯齿

<br>

Flat
Gouraud (平均计算polygon内，在边缘会出现 artifact
Phong (interpolate表面normal，所以最smooth)



Frame Buffer

Depth Buffer / Z-buffer

Smaller number -> Closer to the screen

Unity draws from front object to far (small number to large number)

Render Queues

G-buffer (Geometry buffer)

Forward Render – each object calculate light -

Deferred Render – calculate light all together (good for when there are a lot of lights, but can not render transparent objects)

<br>

## Stencil buffer -> Mask

<br>

## _Draw Call_ -> CPU调用图像接口

(命令缓冲区的一种)

Draw Call多影响性能

减少Draw Call的方法

批次（Batch）， 调用一次渲染API的绘制接口来向GPU提交使用相同渲染状态来渲染物体的行为称为一个渲染批次。

批处理 (Draw Call) Batching

* Dynamic batching // 符合条件的共享同一材质

* Static batching 静态批处理//Static in Unity

优先级：静态>GPU Instancing>动态

先执行了高级，低级的设置会失效

Batching -> Draw Call

减少Draw Call的方法：减少网格，减少材质

<br>

## Mesh.CombineMeshes //Unity 自带combine mesh

Unity uses shadow mapping
Cull Cull Back / Front / Off 剔除模式/剔除背面/正面/关闭剔除
Fixed Function Pipeline 固定管线（不能编程？）