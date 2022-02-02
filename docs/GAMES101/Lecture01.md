# 计算机图形学概述 
## Course Topics (mainly 4 parts)
- Rasterization
- Curves and Meshes
- Ray Tracing
- Animation / Simulation

## 1.Rasterization 光栅化
- Project geometry primitives (3D triangles / polygons) onto the screen 将几何基元（三维三角形/多边形）投影到屏幕上
- Break projected primitives into fragments (pixels) 将投射的基元分解为碎片（像素）。
- Gold standard in Video Games (Real-time Applications) 视频游戏（实时应用）的黄金标准

## 2.Curves and Meshes 曲线和网格
如何在计算机图形学中表示几何图形
- Bezier Curve
- Catmull-Clark subdivision

## 3.Ray Tracing
- Shoot rays from the camera though each pixel

    Calculate intersection and shading 计算交叉点和阴影

    Continue to bounce the rays till they hit light sources 继续反弹光线，直到它们击中光源

- Gold standard in Animations / Movies (Offline Applications)

## 4.Animation / Simulation
- Key frame Animation 关键帧动画
- Mass-spring System

## 5.Most recommended reference
- Steve Marschner and Peter Shirley, "Fundamentals of Computer Graphics", 3rd or later edition.

## 6.Dot Product in Graphics
$\overrightarrow {x} \cdot \overrightarrow {y} = ||\overrightarrow {x}||||\overrightarrow {y}||cos\theta$

点积结果是一个数

- Find angle between two vectors

    (e.g. cosine of angle between light source and surface)

- Finding ==projection投影== of one vector on another 几何意义：投影

- Measure how close two directions are
    
    Decompose a vector

    Determine forward / backward

## 7.Cross Product in Graphics 
$\overrightarrow {x} \times \overrightarrow {y}  = -\overrightarrow {y} \times \overrightarrow {x}$

$\overrightarrow {x} \times \overrightarrow {y} = ||\overrightarrow {x}||||\overrightarrow {y}||sin\theta$

- 叉积与两个初始向量正交

- 由右手定则确定的方向

- 用于构建坐标系

叉乘结果是一个向量

Determine left / right

Determine inside / outside