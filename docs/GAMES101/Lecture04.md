# Viewing (观测) transformation
## 1. View (视图) / Camera transformation
Also known as ModelView Transformation

* Define the camera first
    - Position $\hat e$
    - Look-at / gaze direction $\hat g$
    - Up direction $\hat t$, (assuming perp. to look-at)

* Transform objects together with the camera

* Until camera’s at the origin, up at Y, look at -Z

Transform the camera by $M_{view}$
- So it’s located at the origin, up at Y, look at -Z

#### $M_{view}$ in math?

    - Translates e to origin
    - Rotates g to -Z
    - Rotates t to Y
    - Rotates (g x t) To X


- $M_{view} = R_{view}T_{view}$

- $T_{view}$ = $\begin{bmatrix} 1 & 0 & 0 & -x_e \\ 0 & 1 & 0 & -y_e\\ 0 & 0 & 1 & -z_e \\ 0 & 0 & 0 &1 \end{bmatrix}$

- $R_{view}$ = $\begin{bmatrix} x_{\hat g \times \hat t} & y_{\hat g \times \hat t} & z_{\hat g \times \hat t} & 0 \\ x_t & y_t & z_t & 0\\ x_{-g} & y_{-g} & z_{-g} & 0 \\ 0 & 0 & 0 &1 \end{bmatrix}$

!!! Note "why do we need this?"
    For projection transformation!
## 2. Projection(投影)  transformation
- 3D to 2D

- Orthographic projection 正交投影

- Perspective projection 透视投影

### 2.1 Orthographic (正交) projection
* ==We want to map a cuboid [l, r] x [b, t] x [f, n] to
    the “canonical (正则、规范、标准)” cube [-1, 1]$^3$==   

* Center cuboid by translating

* Scale into “canonical” cube

> Translate (center to origin) first, then scale (length/width/height to 2)

$M_{ortho}$ = $\begin{bmatrix} \frac {2}{r-l} & 0 & 0 & 0 \\ 0 & \frac {2}{t-b} & 0 & 0\\ 0 & 0 & \frac {2}{n-f} & 0 \\ 0 & 0 & 0 &1 \end{bmatrix}$ $\begin{bmatrix} 0 & 0 & 0 & -\frac{r+l}{2} \\ 0 & 0 & 0 & -\frac{t+b}{2}\\ 0 & 0 & 0 & -\frac{n+f}{2} \\ 0 & 0 & 0 &1 \end{bmatrix}$

!!! Warning "Caveat"
    - Looking at / along -Z is making near and far not intuitive (n > f)
    - FYI: that’s why OpenGL (a Graphics API) uses left hand coords

### 2.2 Perspective (透视) projection
多见于计算机图形学、美术、视觉系统

越远的物体越小

平行线不平行，收敛到单点

!!! Note "Recall: property of homogeneous coordinates"
    - $(x, y, z, 1), (kx, ky, kz, k != 0), (xz, yz, z^2, z != 0)$ all represent
    the same point $(x, y, z)$ in 3D
    - e.g. (1, 0, 0, 1) and (2, 0, 0, 2) both represent (1, 0, 0)

#### How to do perspective projection ?
1. First “squish” the frustum into a cuboid (n -> n, f -> f) ($M_{persp->ortho})$
2. Do orthographic projection ($M_{ortho}$, already known!)
3. 通过挤压后的$x,y$得到挤压后的点，根据相似三角形特性，推出点$(nx,ny,unknown,z)$,可得矩阵的1，2，4行。（==n未知,为挤压后的点在z轴上距原点的距离==）
4. 通过以下两个特点，通过代入两个特殊点近平面$(x,y,n,1)$，远平面$(0,0,f)$得到第三行。
    - Any point on the near plane will not change
    - Any point’s z on the far plane will not change

最终矩阵结果如下：
$M_{persp->ortho}$ = $\begin{bmatrix} n & 0 & 0 & 0 \\ 0 & n & 0 & 0\\ 0 & 0 & n+f & -nf \\ 0 & 0 & 1 & 0 \end{bmatrix}$

### 一些转换
1. vertical field-of-view (fovY) 垂直视角，视野
2. aspect ratio 宽高比 ==(assume symmetry i.e. l = -r, b = -t)==

!!! Note "How to convert from fovY and aspect to l, r, b, t"
    $tan \frac{fovY}{2} = \frac{t}{|n|}$
    
    $aspect = \frac{r}{t}$

