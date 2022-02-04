# 变换（二维与三维）
## 1. 2D transformations
### 1.1 Scale (Non-Uniform)
$\begin{bmatrix}x'\\ y'\\ \end{bmatrix}$ = $\begin{bmatrix}S_x & 0 \\ 0 & S_y\\ \end{bmatrix}$ $\begin{bmatrix}x\\ y\\ \end{bmatrix}$

### 1.2 Reflection Matrix
Horizontal reflection:

$\begin{bmatrix}x'\\ y'\\ \end{bmatrix}$ = $\begin{bmatrix}-1 & 0 \\ 0 & 1\\ \end{bmatrix}$ $\begin{bmatrix}x\\ y\\ \end{bmatrix}$

### 1.3 Shear Matrix 切变
Hints:
Horizontal shift is 0 at y=0

Horizontal shift is a at y=1

Vertical shift is always 0

$\begin{bmatrix}x'\\ y'\\ \end{bmatrix}$ = $\begin{bmatrix}1 & a \\ 0 & 1\\ \end{bmatrix}$ $\begin{bmatrix}x\\ y\\ \end{bmatrix}$ 

### 1.4 Rotation Matrix
以原点为旋转中心点
$R_\theta$ = $\begin{bmatrix}cos\theta & -sin\theta \\ sin\theta & cos\theta\\ \end{bmatrix}$ 

### 1.5 Linear Transforms = Matrices(of the same dimension)
$\begin{bmatrix}x'\\ y'\\ \end{bmatrix}$ = $\begin{bmatrix}a & b \\ c & d\\ \end{bmatrix}$ $\begin{bmatrix}x\\ y\\ \end{bmatrix}$ 

## 2. Homogeneous coordinates 齐次坐标
平移就不是Linear Transforms，为了统一形式引入齐次坐标。

Add a third coordinate (w-coordinate)

* 2D point = $(x, y, 1)^T$

* 2D vector = $(x, y, 0)^T$

### 2.1 Affine Transformations 仿射变换
Affine map = linear map + translation:
$\begin{bmatrix}x'\\ y'\\ \end{bmatrix}$ = $\begin{bmatrix}a & b \\ c & d\\ \end{bmatrix}$ $\cdot \begin{bmatrix}x\\ y\\ \end{bmatrix}$ + $\begin{bmatrix}t_x\\ t_y\\ \end{bmatrix}$

先线性变换，再平移

Using homogenous coordinates:
$\begin{bmatrix}x'\\ y'\\ \end{bmatrix}$ = $\begin{bmatrix}a & b & t_x\\ c & d & t_y\\ 0 & 0 & 1 \end{bmatrix}$ $\begin{bmatrix}x\\ y\\ 1\end{bmatrix}$ 

平移可以写成：
$T(t_x,t_y)$ = $\begin{bmatrix}1 & 0 & t_x\\ 0 & 1 & t_y\\ 0 & 0 & 1 \end{bmatrix}$

### 2.2 Composing Transforms
Sequence of affine transforms A1, A2, A3, ... 
$An(...A2(A1(x))) = An ··· A2 · A1 ·$$\begin{bmatrix}x\\ y\\ 1 \end{bmatrix}$ 
预先将n个矩阵相乘，得到一个代表组合变换的
代表组合变换的单一矩阵

### 2.3 Decomposing Complex Transforms
How to rotate around a given point c?

1. Translate center to origin

2. Rotate

3. Translate back 

Matrix representation:
$T(c) · R(\alpha) · T(c)$

## 3. 3D Transformations
Use homogeneous coordinates again:

* 3D point = $(x, y, z, 1)^T$

* 3D vector = $(x, y, z, 0)^T $

In general, (x, y, Z, W) (w != 0) is the 3D point: 

(x/w, y/w, Z/w)