
### Gauss’s Method

Theorem

If a linear system is changed to another by one of these operations

1.  an equation is swapped with a another
2.  an equation has both sides multiplied by a nonzero constant
3.  an equation is replaced by the sum of itself and a multiple of another then the two systems have the same set of solutions

Definition The three operations from Theorem are the elementary reduction operations, or row operations, or Gaussian operations. They are swapping, multiplying by a scalar (or rescaling), and row combination

### Matrices and Vectors

_Definition_

An m x n matrix is a rectangular array of numbers with m rows and n columns. Each number in the matrix is an entry.

_Example_ This is a 2 x 3 matrix

$$
B=
\begin{pmatrix}
1  & -2 & 2 \\
4 &  -5 & 6 \\
\end{pmatrix}
$$

It has 2 rows and 3 columns. The entry in row 2 and column 1 is

$$
b_{2,1}=4
$$

_Definition_

A column vector, often just called a vector, is a matrix with a single column. A matrix with a single row is a row vector. The entries of a vector are sometimes called components. A column or row vector whose components are all zeros is a zero vector.

$$
\vec{v} =
\begin{pmatrix}
-1 \\ 0.5 \\ 0
\end{pmatrix}
$$

_Example:_ This row vector has three components

$$
\vec{w} =
\begin{pmatrix}
-1 & 0.5 & 0
\end{pmatrix}
$$

_Example:_ This is the two-component zero vector

$$
\vec{0} =
\begin{pmatrix}
0 \\  0
\end{pmatrix}
$$

### Vector Operations

The vector sum of u and v is the vector of the sums

$$
\vec{w} + \vec{v} =
\begin{pmatrix}
u_1 \\ \vdots \\ u_n
\end{pmatrix} +
\begin{pmatrix}
v_1 \\ \vdots \\ v_n
\end{pmatrix} = 
\begin{pmatrix}
u_1 + v_1 \\ \vdots \\ u_n + v_n
\end{pmatrix}
$$

The scalar multiplication of the real number r and the vector v is the vector of the multiples

$$
r \cdot \vec{v} = r \cdot
\begin{pmatrix}
v_1 \\ \vdots \\ v_n
\end{pmatrix} = 
\begin{pmatrix}
rv_1 \\ \vdots \\ rv_n
\end{pmatrix}
$$



 | 
---|---|---
Linear Combination|线性组合|add multiple vectors
Span||The span of a set of vectors is **the set of all linear combinations of the vectors**


<br>

### Dot product

满足交换率(commutative)和结合律(Associative property)

Length by 勾股定理
Length to product

$\lVert \vec a \rVert = \sqrt{ a ^ 2 _1 + a ^ 2 _2 + ... + a ^ 2 _n}$

$\lVert \vec a \rVert = \sqrt{ \vec a \cdot \vec a}$

$\lVert \vec a \rVert ^2 = \vec a \cdot \vec a$

<br>

##### Cauchy-Schwarz Inequality (柯西-施瓦茨不等式)
$\vec x$, $\vec y \in ℝ^n$,
$\vec x$, $\vec y$ non zero

dot product of x y is ≤ to product of length x and length y

$|\vec x \cdot \vec y| \le \lVert \vec x \rVert \lVert \vec y \rVert$
when $\vec x = c \vec y$, $|\vec x \cdot \vec y| = \lVert \vec x \rVert \lVert \vec y \rVert$

$$ \vec x \cdot \vec y \le |\vec x \cdot \vec y| $$

$\vec x \cdot \vec y < |\vec x \cdot \vec y|$ could be negative, → less than

##### Triangle Inequality
由Cauchy-Schwarz Inequality推导出来

$||\vec x + \vec y|| \le ||\vec x|| + ||\vec y||$