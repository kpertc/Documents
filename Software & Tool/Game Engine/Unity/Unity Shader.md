#Unity #CG 

- [Writing a custom shader in ShaderLab and HLSL](https://docs.unity3d.com/6000.0/Documentation/Manual/SL-landing.html)
### GitHub Repository
[Shader Test](https://github.com/kpertc/ShaderTest)

### URP Unlit Shader Template

Unity Shading Language CG → HLSL

``` HLSL
Shader "Examples/ShaderSyntax"
{
    //CustomEditor = "ExampleCustomEditor"

    Properties
    {
        // ShaderLab: defining material properties
        _ExampleTex("Example Texture", 2D) = "white" {}
        _ExampleColor("Example Colour", Color) = (1,1,1,1)
        _ExampleRange("Example Float Range", Range(0.0, 1.0)) = 0.5
        _ExampleFloat("Example Float", Float) = 1.0
        _ExampleVector("Example Vector", Vector) = (0,0,0,0)
        
        [Enum(Off,0,On,1)]_ZWrite ("ZWrite", Float) = 1.0
        [Enum(UnityEngine.Rendering.CompareFunction)] _ZTest("ZTest", Float) = 4 //"LessEqual"
        [Enum(UnityEngine.Rendering.CullMode)] _Culling ("Culling", Float) = 0
        
    }
    SubShader //一个shader 至少一个Sub Shader，一个Pass
    // 为了支持不同渲染管线，不同GPU等
    {
    
        ZWrite [_ZWrite]
        ZTest [_ZTest]
        Cull [_Culling]
        Blend
    
        Tags{
            "RenderType" = "Opaque" 
            "RenderPipeline" = "UniversalRenderPipeline" 
            "IgnoreProjector" = "True"
        }
        
        LOD 300
        
        HLSLPROGRAM // 如果是用HLSL语言写，或者CGPROGRAM ｜ GLSLPROGRAM
        
        //common URP libraries
        #include "Packages/com.unity.render-pipelines.universal/ShaderLibrary/Core.hlsl"
        
        #pragma vertex UnlitPassVertex
        #pragma fragment UnlitPassFragment
        
        //顶点着色器数据结构
        struct Attributes {
                float4 positionOS   : POSITION;
                float4 normalOS     : NORMAL;
                float2 uv           : TEXCOORD0;
                float2 lightmapUV   : TEXCOORD1;
                float4 color        : COLOR;
                //UNITY_VERTEX_INPUT_INSTANCE_ID
        };
        
        //顶点着色器数据结构
        struct Varyings {
            float4 positionCS   : SV_POSITION;
            float3 clipNornal : TEXCOORD1;
        };
        
        CBUFFER_START(UnityPerMaterial)
            float4 _ExampleTexture_ST; // Tiling & Offset, x = TilingX, y = TilingY, z = OffsetX, w = OffsetY
            float4 _ExampleTexture_TexelSize; // x = 1/width, y = 1/height, z = width, w = height.
            float4 _ExampleColor;
            float _ExampleRange;
            float _ExampleFloat;
            float4 _ExampleVector;
        CBUFFER_END
        
        ...
        ENDHLSL

        Pass
        {
           // The code that defines the Pass goes here
        }
        
        // use URP shadow pass
        UsePass "Universal Render Pipeline/Lit/ShadowCaster"
    }
    Fallback "ExampleFallbackShader"
}
```

>SRP中特殊的Tag: RenderPipeline - 指定用哪个渲染管线:
	URP：UniversalPipeline
	HDRP：HDRenderPipeline
	SPR：自定义的标签

>URP也支持CG语言。如果你给Shader添加“CGPROGRAM/ENDCGPROGRAM”块，Unity会自动include内饰渲染管线的代码库，此时如果你再include SRP shader代码库，可能会有一些宏或者函数和内置渲染管线的代码库冲突。此外，使用CG语言无法支持SRP Batcher *Unlit是可以直接用

>The word ==pragma== comes from Greek and refers to an action, or something that needs to be done. It's used in many programming languages to issue special compiler directives.

### Shader data types and precision

-   High precision `float`
-   Medium precision `half`
-   Low precision `fixed`

### HLSL
``` hlsl


```

### Functions
[HSLS固有函数](http://www.cppblog.com/lai3d/archive/2008/10/23/64889.html)

```HLSL
remap

saturate() // clamp value 0-1
frac() // Returns the fractional (or decimal) part of input 
lerp

sign() //value is 1 when f is positive or zero, -1 when f is negative.
floor() //Returns the greatest integer which is less than or equal to.
```

HLSL requires all variables and functions to be defined before use.

### Unity (Offical Docs)

-   **[Unity URP Shader Docs](https://docs.unity3d.com/Packages/com.unity.render-pipelines.universal@13.1/manual/writing-custom-shaders-urp.html)**
-   **[Unity Shader commands](https://docs.unity3d.com/Manual/shader-shaderlab-commands.html)**


Cyan Tutorial (URP Shader Template)
https://www.cyanilux.com/tutorials/intro-to-shaders/#properties
https://www.cyanilux.com/tutorials/urp-shader-code/

### Build-in转URP 命令参考

`SPR Batcher` - All materials using the same shader variant use a single draw call
Core.hlsl does not contain default structs use as `appdata` or `v2f`
Core.hlsl does not contain pre-coded vertex or fragment functions


> [!info] URP new naming convention
> `Appdate` 🠒 `Attribute`
> `v2f` 🠒 `Varyings`

> [!info] URP new naming convention
> **[From Built-in to URP](https://teodutra.com/unity/shaders/urp/graphics/2020/05/18/From-Built-in-to-URP/)** 英文原版
> **[内置管线Shader升级到URP详细手册](https://www.jianshu.com/p/3fef69e2efb6)** 中文
>1.  Add render pipeline tag `"RenderPipline" = "UniversalPipline"`
2.  Replace `CGPROGRAM` by `HLSLPROGRAM`
3.  Replace `UnityCG.cginc` with URP `Core.hlsl`
4.  Create `Attribute` & `Varyings`
5.  Replace legacy functions `UnityObjectToClipPos` by new functions `TransformObjectToHClip`
6.  Replace `fixed` type with `half`

<br>

### [Unity Material Property Drawer](https://docs.unity3d.com/ScriptReference/MaterialPropertyDrawer.html)

URP 多Pass [LWRP/URP/HDRP中的多Pass shader，以描边效果为例](https://zhuanlan.zhihu.com/p/354190065)

### Other Resources:

-   **[URP 基本光照模版](https://www.zhihu.com/column/c_1355113121934114816)**
-   **[CatLike](https://catlikecoding.com/)**
-   **[Freya Holmér (YouTube)](https://www.youtube.com/channel/UC7M-Wz4zK8oikt6ATcoTwBA)**
-   **[ShaderToy (实时Shader网站)](https://www.shadertoy.com/)**
-   **[蛮牛教育 (BiliBili)](https://www.bilibili.com/video/BV1CX4y1F7pW?p=16)**
-   **[火星时代](https://shenjun4shader.github.io/shaderhtml/)**
-   **[千锋 (YouTube)](https://www.youtube.com/playlist?list=PLwDQt7s1o9J6xa44xhckRdwoAEilNeiKc)**
-   **[Ned Makes Games (URP Shaders) (YouTube)](https://www.youtube.com/c/NedMakesGames/playlists)**
-   **[ShaderLab (YouTube)](https://www.youtube.com/channel/UCDk9-aPr8zQzwi4ylnuoJ6w)**
-   **[WalkingFat](http://walkingfat.com/)**

[LearnOpenGL CN](https://learnopengl-cn.github.io)

[The Book of Shaders](https://thebookofshaders.com/)

[[OpenGL]]

<br>

唐福幸 Universial RP 书中配套资源： https://zhuanlan.zhihu.com/p/421389748

[GitHub - candycat1992/Unity_Shaders_Book: 书籍《Unity Shader入门精要》源代码](https://github.com/candycat1992/Unity_Shaders_Book)

<br>

##### 后期处理 Post-Processing

[XPL: Unity引擎的高品质后处理库](https://github.com/QianMo/X-PostProcessing-Library)

<br>

### Compute Shader

[Minimal Compute Shader Examples](https://github.com/cinight/MinimalCompute)

[URP管线的自学HLSL之路 第二十九篇 ComputeShader释义](https://www.bilibili.com/read/cv6995587?spm_id_from=333.999.0.0)

<br>

### 帮助链接

[URP](https://bytedance.feishu.cn/docx/doxcnKHLgO0keEzErLhPPZwjwtc)

计算机图形学 [Computer Graphics](https://bytedance.feishu.cn/docs/doccnTXFU206kM53Wegm9dsL1Qd)

Unity Editor 工具编写 [Unity Editor](https://bytedance.feishu.cn/docx/doxcndejxg5SOoqTBnSU2V8wJhg)

<br>

### Experience

Flip UV
```hlsl
(1 - i.uv.x) // Flip Horizontal
(1 - i.uv.x) // Flip Vertical
```