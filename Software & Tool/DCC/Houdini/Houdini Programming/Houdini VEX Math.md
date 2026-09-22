#CG 

Learn more @[[Math]]

### math.h
math.h file: `$HFS/houdini/vex/include/math.h` from hscript textport
![[Houdini VEX Math img/mathh.gif]]


[[Houdini VEX Math img/math.h|math.h]]


### [Math](https://youtu.be/xmgp53xPA9M)

```C#
radians = radians(degrees);
degrees = degrees(radians);
```

```C#
// Dot Product
f@dot = dot(normalize(V1), normalize(V2)); // must normalize, else dot leaves [-1,1] and acos → NaN
f@degree = degrees(acos(@dot)); // get angle, default unit is radian
// robust, no normalize needed: degrees(atan2(length(cross(V1,V2)), dot(V1,V2)))

// Cross Product
V3 = cross(V1,V2) // Perpendicular to V1 and V2
// 0, 180 -> length 0; 90 maxlength 270 -maxlength

// Quaternion
vector V = set (0, 1, 0);
vector4 Q = quaternion(radians(degree), V); // rotate around vector V
@P = qrotate(Q, @P);

// method2: convert quaternion to matrix
matrix3 QtoM = qconvert(Q); // qconvert() returns matrix3
@P = @P * QtoM; // rotates about the origin, handle pivot yourself

// Matrix
```


`$PI`


### Matrix
Tutorial: [[YouTube] [VEX for Algorithmic Design] E15 _ Matrix Basics 1 (Basic Transformation) Junichiro Horikawa](https://youtu.be/ScYtNmnyF9A)

##### Declare
```C#
matrix2 mat = { 1,2,3,4 } // 2x2 matrix
matrix2 mat = set(1,2,3,4); // can use variable

matrix3 mat = ... // 3x3 matrix   

matrix mat4 = {{1,2,3,4}, {5,6,7,8}, {9,10,11,12}, {13,14,15,16}}; // use vector4 decalare matrix
matrix mat4 = set( set(1,2,3,4), set(5,6,7,8), set(9,10,11,12), set(13,14,15,16)); // use vector4 decalare matrix

ident() // return an identity matrix
```
<br/>

  
##### Matrix Functions
```C#
determinant() // determinant 0 -> no invert matrix ; != 0 has an invert matrix
invert() // invert a matrix 
// no invert matrix when result is not a identity matrix
transpose()
transpose(mat1) * transpose(mat2) = transpose(mat2 * mat1)
```

> [!info] 
> $$\begin{bmatrix}a&b\\c&d\end{bmatrix}$$ 
> determinant (float) = a*d - b*c
> det -> to check if the matrix has a inverse matrix
> matrix x matrix -1 (inverse matrix) = identity matrix


> [!info] Transpose Matrix
> $$ A^T \times B^T = (B \times A)^T $$

  
##### Vector x Matrix
```C#
vector v1 = v * mat; // should do this order in math
vector v2 = mat * v; // cant do this in math
v1 = v2 // in houdini is the same
```

##### Transformation matrix
```C#
matrix mat = ident();

translate(mat, move_vector); // equal to addition @P += move_vectpr
scale(mat, scale_vector); // equal to mutiplication @P *= scale_vector
rotate(mat, angle, axis); // rotation

@P *= mat
```

```C#
maketransform(); // TRS → matrix, all lowercase, VEX is case-sensitive
// matrix maketransform(int trs, int xyz, vector t, vector r, vector s)
// trs order (math.h): XFORM_SRT 0, XFORM_STR 1, XFORM_RST 2, XFORM_RTS 3, XFORM_TSR 4, XFORM_TRS 5
// xyz rotate order (math.h): XFORM_XYZ 0 ... XFORM_ZYX 5
cracktransform(); // matrix → TRS
// need TRS order and matrix
```

  
`fit()` //remap