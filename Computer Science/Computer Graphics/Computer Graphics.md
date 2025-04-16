#CG

[[OpenGL]]

[[Math]] Matrix Calculation
[acegikmo.notion.site](https://acegikmo.notion.site/Math-for-Game-Dev-1f3269e5af544ac9a8c92964a5f508c2)
[[Games 101]]

> [!note] Realtime Graphics
> Realtime → at least 30FPS
VR Realtime → at least 90 FPS
Correctness: no tolerance to (uncontrollable failure)

### Pipeline
> [!NOTE]- Graphic Pipeline Image
>![[graphic-pipline.png]]
>![[graphic-pipline-2.png]]

### Coordinates System

> [!NOTE]
> Model coordinates → World coordinates
World coordinates → Camera coordinates
Camera coordinates → View Plane

| ![[XYZ RGB.png \| 300]] | ![[lefthand-righthand.png]] |
| ----------------------- | --------------------------- |
|                         |                             |

> **w** component affects the scale of the image with respect to the projection.

Clip Space
`ClipCoord.xyz / ClipCoord.w → x, y, z [-1, +1]`
**NDC (Normalized Device Coordinates)**
[Homogeneous Coordinates, Clip Space, and NDC | WebGPU](https://carmencincotti.com/2022-05-02/homogeneous-coordinates-clip-space-ndc/)

FBO (Frame Buffer Object)
GPGPU stands for **General-Purpose computing on Graphics Processing Units**.

### PBR related Topics
![[PBR-topics.png]]

### TBN 
TBN: Tangent, Bitangent, Normal
Object Space Normal vs Tangent Space Normal
![[Object Space Normal vs Tangent Space Normal.png]]
![[object-word-space-normal-calculation.png]]

<br>

### Super Sampling
> [!NOTE]- Super Sampling
>![[super-sampling.png]]

### Shading
![[flat-gouraud-phong.png]]

non-PBR shading
Gouraud → in vertex shader
Phong → in fragment shader

```glsl
vec3 light = vec3(0.0);

// ambient light
light += 
ambient
* ambientColor
;
```

``` glsl

```
 
##### Cubemap
shortcut for performance for realtime rendering
to bake cubemap, set 6 90 degree FOV cameras, and aspect ratio to `1:1`
`.dds` format for UE

##### Reflection & Refraction
![[reflection-refraction-vector.jpg]]

##### BXDF, Bidirectional XXX Distribution Function, 双向XX分布函数
求积分 -> 蒙特卡洛积分
-   BRDF，Reflection，双向反射分布函数
-   BSSDF，Subsurface Scattering，次表面散射
-   BTDF
-   BSDF

[[Unity Shader]]

### Curve

1. **Bézier curve**
	Pierre Bezier 1910 - 1999
	Paul de Casteljau 1930 - (算法)
	Sergei N. Bernstein 伯恩斯坦

	**Convex hull - 凸包**
	
	Bezier curve is within convex hull of control points
	贝塞尔曲线在控制点的凸包内
	
	High-order / Low-order Bezier Curve
	
	Piecewise Bezier Curve (分段贝塞尔曲线)
	
	C0 连续 点位置一致 an = b0
	C1 连续 切线连续 （一阶导数连续）an = b0 = 1/2(an-1 + b1)
	C2 连续 倒数第一控制点怜恤（二阶导数连续）

2. Spine 样条
- B-splines -> basis splines B样条 奇函数
- NURBS, Non-Uniform Rational B-Spines 非均匀有理样条

### [[Geometry]]

<br>

### Rasterizing Render - Fast (realtime)

##### Shadow Mapping (阴影映射)

Image-space Algorithm

Aliasing artifacts

![[shadow-mapping.jpg | 300]]


精度偏差问题 - Use "Bias" to control value to be shadow

![[bias0.png]]|![[bias01.png]]|![[bias08.png]]
--|--|--
(EHI) Shadow Bias

Hard Shadow - Point Light

<br>

### Animation & Simulation

> [!NOTE] Mass Spring System 质点弹簧系统 布料
> **Damping force**
>**FEM (Finite Element Method) 有限元 车辆碰撞 （力传导）**

##### Blend Shape -> interpolate between surfaces, no skeleton

![[essentials.jpeg]]

<br>

### Axis-Aligned Bounding Box (AABB) 轴对其==包围盒==

<br>

### Slerp vs Lerp

Slerp: Spherical interpolates between two vector
Lerp: Linear Interpolate