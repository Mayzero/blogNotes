# 计算机图形学概述 
# Course Topics (mainly 4 parts)
- Rasterization
- Curves and Meshes
- Ray Tracing
- Animation / Simulation

# Rasterization 光栅化
- Project geometry primitives (3D triangles / polygons) onto the screen 将几何基元（三维三角形/多边形）投影到屏幕上
- Break projected primitives into fragments (pixels) 将投射的基元分解为碎片（像素）。
- Gold standard in Video Games (Real-time Applications) 视频游戏（实时应用）的黄金标准

# Curves and Meshes 曲线和网格
如何在计算机图形学中表示几何图形
- Bezier Curve
- Catmull-Clark subdivision

# Ray Tracing
- Shoot rays from the camera though each pixel

    Calculate intersection and shading 计算交叉点和阴影

    Continue to bounce the rays till they hit light sources 继续反弹光线，直到它们击中光源

- Gold standard in Animations / Movies (Offline Applications)

# Animation / Simulation
- Key frame Animation 关键帧动画
- Mass-spring System

# Most recommended reference
- Steve Marschner and Peter Shirley, "Fundamentals of Computer Graphics", 3rd or later edition.