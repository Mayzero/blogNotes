# 光栅化（三角形的离散化） Rasterization 1 (Triangles)
1. vertical field-of-view (fovY) 垂直视角，视野
2. aspect ratio 宽高比

!!! Note "How to convert from fovY and aspect to l, r, b, t"
    $tan \frac{fovY}{2} = \frac{t}{|n|}$
    $aspect = \frac{r}{t}$

## MVP
1. Model transformation (placing objects)
2. View transformation (placing camera)
3. Projection transformation
    - Orthographic projection (cuboid to “canonical” cube [-1, 1]$^3$)
    - Perspective projection (frustum to “canonical” cube)

## 1. Canonical Cube to Screen
#### What is a screen?
- An array of pixels
- Size of the array: resolution
- A typical kind of raster display 

#### Raster == screen in German
- Rasterize == drawing onto the screen

####　Pixel (FYI, short for “picture element”)
- For now: A pixel is a little square with uniform color
- Color is a mixture of (red, green, blue)

### 步骤
1. Irrelevant to z
2. Transform in xy plane: [-1, 1]2 to [0, width] x [0, height]
3. Viewport transform matrix:
$M_{viewport}$ = $\begin{bmatrix} \frac{width}{2} & 0 & 0 & \frac{width}{2} \\ 0 & \frac{heigst}{2} & 0 & \frac{heigst}{2}\\ 0 & 0 & 1 & 0 \\ 0 & 0 & 0 & 1 \end{bmatrix}$
4. Rasterizing Triangles into Pixels

## 2. Drawing to Raster Displays