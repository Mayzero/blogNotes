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

* $M_{view}$ in math?
    - Translates e to origin
    - Rotates g to -Z
    - Rotates t to Y
    - Rotates (g x t) To X
    - Difficult to write!

- $M_{view} = R_{view}T_{view}$

- $T_{view}$ = $\begin{bmatrix} 1 & 0 & 0 & -x_e \\ 0 & 1 & 0 & -y_e\\ 0 & 0 & 1 & -z_e \\ 0 & 0 & 0 &1 \end{bmatrix}$

- $R_{view}$ = $\begin{bmatrix} x_{\hat g \times \hat t} & y_{\hat g \times \hat t} & z_{\hat g \times \hat t} & 0 \\ x_t & y_t & z_t & 0\\ x_{-g} & y_{-g} & z_{-g} & 0 \\ 0 & 0 & 0 &1 \end{bmatrix}$

!!! Note "why do we need this?"
    For projection transformation!
## 2. Projection(投影)  transformation
- 3D to 2D

- Orthographic projection 正交投影
    * We want to map a cuboid [l, r] x [b, t] x [f, n] to
    the “canonical (正则、规范、标准)” cube [-1, 1]$^3$
    * Center cuboid by translating
    * Scale into “canonical” cube

> Translate (center to origin) first, then scale (length/width/height to 2)

$M_{ortho}$ = $\begin{bmatrix} \frac {2}{r-l} & 0 & 0 & 0 \\ 0 & \frac {2}{t-b} & 0 & 0\\ 0 & 0 & \frac {2}{n-f} & 0 \\ 0 & 0 & 0 &1 \end{bmatrix}$ $\begin{bmatrix} 0 & 0 & 0 & -\frac{r+l}{2} \\ 0 & 0 & 0 & -\frac{t+b}{2}\\ 0 & 0 & 0 & -\frac{n+f}{2} \\ 0 & 0 & 0 &1 \end{bmatrix}$

- Perspective projection 透视投影

### 2.1 Orthographic (正交) projection
### 2.2 Perspective (透视) projection