
[[Algebra]]
[[Linear Algebra]]

[[Statistics Math]]
[[Probability]]
[[Calculus]]


3D
[[Python math]]
[[Houdini VEX Math]]

<br>

##### Math Learning
**[3Blue1Brown](https://www.youtube.com/channel/UCYO_jab_esuFRV4b17AJtAw)**
**[Calculus Blue - Prof Ghrist Math](https://www.youtube.com/c/ProfGhristMath)**

<br>

基础

英文|符号|中文
---|---|---
Denominator||分母
Factorial|$!$<br>$5! = 5 \times 4 \times 3 \times 2 \times 1 = 120$|阶乘


<br>

英文<img width="150px" />|标志<img width="20px" />|中文<img width="100px" />|详解<img width="350px" />
---|---|---|---
Vector|$$\vec a$$|向量/矢量|
Magnitude ==(Length of the Vector)==|$$\lVert a \rVert$$|模|向量/矢量的长度
Normalized Vector|$$\hat a$$ (hat)|归一化矢量|
norm||范数|
Dot (==Scalar==) product (Inner Product)||点乘，内积|返回比例，（Normalize）用Cos可得到角度$$a·b = a_x · b_x + a_y · b_y$$$$a·b = a_x · b_x + a_y · b_y + a_z · b_z$$
Cross Product (Outer Product)|$$\times$$|叉乘，叉积|算垂直法向量， 判断垂直，内外，旋向性$$\begin{bmatrix}x_1\\y_1\\z_1\end{bmatrix} \times \begin{bmatrix}x_2\\y_2\\z_2\end{bmatrix} = \begin{bmatrix}y_1z_2 -z_1y_2\\z_1x_2-x_1z_2\\x_1y_2-y_1x_2\end{bmatrix}$$
Homogeneous coordinates||齐次坐标|
Linear Transformation||线性变换|Rotation, Scale, Orthographic Projection, Reflection, Shearing<li>All lines remains on line</li><li>Origin -> fixed</li><br>Paralleled & Even space<br>Transform is not linear transformation
[Affine Transformation](https://www.youtube.com/watch?v=E3Phj6J287o)||仿射变换|平移 + 线性变换
Upright Space||直立空间|World Space ⇌ Upright Space ⇌ Object Space<br>&nbsp&nbsp&nbsp&nbsp&nbsp&nbsp&nbsp&nbsp&nbsp&nbsp&nbsp&nbsp&nbsp&nbsp&nbsp&nbsp&nbsp&nbsp&nbsp&nbsp&nbsp平移 &nbsp&nbsp&nbsp&nbsp&nbsp&nbsp&nbsp&nbsp&nbsp&nbsp&nbsp&nbsp&nbsp&nbsp&nbsp&nbsp&nbsp&nbsp&nbsp&nbsp&nbsp&nbsp旋转
Eigenvector||特征向量|only scale not rotate ![[eigenvector.png\|200]]
Eigenvalue||特征值|Scale factor → Eigenvalue
Polar coordinates||极坐标系|(r,θ)

<br>

### 数学常量


|<span style="font-weight:normal">Radian (rad)</span>|<img width="50px" />|<span style="font-weight:normal">弧度</span>|<span style="font-weight:normal">1 Radian = 57.295 degree</span>
--|--|--|--
Tau|τ| |1Tau = 2π _≈_ 6.28
Euler's number|e||2.71828182846...<br>$e = \mathop {\lim }\limits_{n \to \infty } \left( {1 + \frac{1}{n}} \right)^n$


<br>

**英文**<img width="100px" />|**中文**<img width="100px" />
---|---
Polynomial|多项式
Integral|积分
Anisotropy|各向异性
Isotropy|各项同性
Orthogonal|直角的，矩形的
Orthonormal|正交规范的
Convolution|卷积
Manifold|流形
Commutative|交换律

<br>

### 图形计算器

图形计算器 https://www.desmos.com/calculator?lang=zh-CN
Geogebra 3D计算器 https://www.geogebra.org/3d


### Matrix

Row x Column<br>行 x 列

1x3 matrix|$$\begin{bmatrix}1&2&3\end{bmatrix}$$1x3 matrix
---|---

3x1 matrix|$$\begin{bmatrix}1\\2\\3 \end{bmatrix}$$
---|---

<mark style="background-color: #F53F3F">1</mark>x==3 3==x<mark style="background-color: #F53F3F">1</mark> 
==3x3== 
Result <mark style="background-color: #F53F3F">1x1</mark>



<br>

|<span style="font-weight:normal">Square Matrix</span>|<img width="50px" />|<span style="font-weight:normal">方形矩阵</span>|<span style="font-weight:normal">same number of rows and columns.<br/>具有相同行数和列出的矩阵</span>
--|--|--|--
Diagonal Matrix||对角矩阵|非对角元素均为0<br>$$\begin{bmatrix}1&0&0\\0&2&0\\0&0&3\end{bmatrix}$$
Identity Matrix||单位矩阵|$$\begin{bmatrix}1&0&0\\0&1&0\\0&0&1 \end{bmatrix}$$==任何矩阵与单位矩阵相乘都等于本身==<br>如同数的乘法中的1
Inverse matrix||逆矩阵|一个矩阵和另一个矩阵相乘结果为单位矩阵
Determinant||行列式|仅当行列式 ≠ 0 时，矩阵才可逆。
Transposed Matrix|T<br>$$m^\intercal$$|转置矩阵|$$\begin{bmatrix}1&2&3\\4&5&6\\7&8&9\\10&11&12\end{bmatrix}\rightarrow\begin{bmatrix}1&4&7&10\\2&5&8&11\\3&6&9&12 \end{bmatrix}$$$$A^\intercal \times B^\intercal = (B \times A)^\intercal$$
Orthogonal Matrix||正交矩阵|



Matrix x Vector
matrix column # match vector #

$$ 
A = \begin{bmatrix} a_{11}&a_{22}&\dots&a_{1n}\\ a_{21}&a_{22}&\dots&a_{2n}\\ \vdots&\vdots&\vdots&\vdots\\ a_{m1}&a_{m2}&\dots&a_{mn}\\ \end{bmatrix}
\begin{bmatrix} x_1\\ x_2\\ \vdots\\ x_m\\ \end{bmatrix}
=
\begin{bmatrix} a_{11}x_1&a_{22}x_2&\dots&a_{1n}x_n\\ a_{21}x_1&a_{22}x_2&\dots&a_{2n}x_n\\ \vdots&\vdots&\vdots&\vdots\\ a_{m1}x_1&a_{m2}x_2&\dots&a_{mn}x_n\\ \end{bmatrix} 
$$


2x2 square matrix
$$
\begin{bmatrix}
a & b \\
c & d  
\end{bmatrix} + 
\begin{bmatrix}
e & f \\
g & h  
\end{bmatrix}=
\begin{bmatrix}
ae+bg & af+bh \\
ce+dg & cf+dh  
\end{bmatrix}
$$

<br>

Transformation: Transform, Rotation, Scale matrix, orders matters


> [!NOTE]- Zero
> ![[zero.png]]

> [!NOTE]- Rotation
> ![[rotation.png]]

> [!NOTE]- Rotation & Translation
![[Rotation & Translation.png]]

> [!NOTE]- Scale
>![[scale.png]]

> [!NOTE]- Shear
>![[shear.png]]

A coordinate space for point/vectors (Local Value)
![[matrix-multiplication.png]]