#CG 

### Represent Geometry

> [!NOTE]- Ways to Represent Geometry
> ![[Many Ways to Represent Geometry.jpg]]

1. Implicit 隐式几何

-   点的关系 比如函数表达 (更数学);
-   容易判断 例如判断点是否在几何内;
-   不容易可视化

	Distance Functions (Implicit) 用距离描述
	Blend
	Signed Distance Field
	Level Set Methods
	Fractals (分形)

	**Constructive Solid Geometry (CSG) (Implicit)**
	-   Boolean Operations
	-   ∩ - Union
	-   ∪ - Intersection
	-   \ - Difference

2.  Explicit 显式几何 - 用参数设定

---

### Mesh
-   Structured Mesh
-   UnStructured Mesh

> [!NOTE]- OBJ Format by Wavefront
v - vertex
vt - texture coordinate
vn - vertex normal
vp -
f - face

![[mesh-types.png]]

##### **Mesh** **Operations: Geometry Processing 几何处理**

-   **Mesh subdivision 细分**
			
> 		degree 点连边的数量
> 		Extraordinary vertex degree != 4; 度不为4

Loop(人名)|Catmull(人名)-Clark(人名) Subdivision
---|---
(先细分，再调整) 必需是三角形网格|(General Mesh 不必需是三角形网格) (一次变换后全转换成四边形，第一次的非四边形面变成奇异点)

![[Pasted Graphic 1.jpg | 200]]
<br>

-   **Mesh** **simplification 简化**
    -   Edge Collapsing
    -   Quadric Error 二次度量误差

<br>

-   **Mesh Regularization 正规化**

### Dual Mesh
![[Dual Mesh.png]]