#CG 

Learn more @[[Math]]

### math.h
math.h file: `$HFS/houdini/vex/include/math.h` from hscript textport
![[Houdini VEX Math img/mathh.gif]]


[math.h](./Houdini VEX Math img/math.h)


### [Math](https://youtu.be/xmgp53xPA9M)

```C#
radians = radians(degrees);
degrees = degrees(radians);
```

```C#
// Dot Product
f@dot = dot(V1, V2);
f@degree = degrees(acos(@dot)); // get angle, default unit is radian

// Cross Product
V3 = cross(V1,V2) // Perpendicular to V1 and V2
// 0, 180 -> length 0; 90 maxlength 270 -maxlength

// Quaternion
vector V = set (0, 1, 0);
vector4 Q = quaternion(radians(degree), V); // rotate around vector V
@P = qrotate(Q, @P);

// method2: convert quaternion to matrix
matrix QtoM = qconvert(Q);
@P = @P * QToM;

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
makeTransform(); // TRS → matrix
cracktransform(); // matrix → TRS
// need TRS order and matrix
```

  
`fit()` //remap