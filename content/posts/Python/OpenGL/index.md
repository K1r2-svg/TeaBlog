---
title: "openGL"
date: 2025-05-22
---

# openGL

## 基本使用

### 导入

```python
from OpenGL.GL import *
from OpenGL.GLU import *
```

### `gluPerspective()`

调用 gluPerspective 来描述我们在场景中的视角。

**实例**：

```python
gluPerspective(45, 1, 0.1, 50.0)
#45: 视线角度为45
#1: 视口的宽高比（aspect ratio）。这里宽高比为 1，意味着视口的宽度和高度相等。通常，这个值应该设置为视口的实际宽度除以高度。
#0.1: 近裁剪面的距离。任何距离相机小于这个值的物体都将被裁剪掉，不会显示在屏幕上。
#50.0: 远裁剪面的距离。任何距离相机大于这个值的物体都将被裁剪掉，不会显示在屏幕上。
```

### `glTranslatef()`

用于对当前的模型视图矩阵进行平移变换。平移变换可以将物体在三维空间中沿着指定的方向移动。

**实例**：

```python
glTranslatef(0.0, 0.0, -5)
#0.0：表示在 X 轴方向上的平移量。这里设置为 0，意味着在 X 轴方向上不进行平移。

#0.0：表示在 Y 轴方向上的平移量。这里设置为 0，意味着在 Y 轴方向上不进行平移。

#-5：表示在 Z 轴方向上的平移量。由于 OpenGL 采用右手坐标系，Z 轴正方向指向屏幕外，负方向指向屏幕内，所以这里将物体沿着 Z 轴负方向平移 5 个单位，相当于将物体向屏幕内移动 5 个单位，从而使物体离相机更远。
```

### `glRotatef()`

用于改变我们观察场景的角度。调用 glRotatef(theta, x, y, z)会将整个场景围绕向量(x, y, z)指定的轴旋转角度 theta。

**实例**：

```python
glRotatef(30, 0, 0, 1)
#绕z轴 30°
```



### `glEnable()`

用于启用特定的 OpenGL 功能。

**实例**：

```python
glEnable(GL_CULL_FACE);
#GL_CULL_FACE，表示面剔除功能。面剔除是一种优化技术，用于剔除那些背对相机的面，从而减少不必要的渲染计算。
glEnable(GL_DEPTH_TEST);
#GL_DEPTH_TEST，表示深度测试功能。深度测试是一种用于确定哪些物体应该显示在前面，哪些物体应该显示在后面的技术。确保渲染离我们最近的多边形
```

### `glCullFace()`

用于指定要剔除的面的类型。

**实例**：

```python
glCullFace(GL_BACK);
#GL_BACK：表示要剔除的面是背对相机的面。
```

### `glClear()`

主要作用是清除指定的缓冲区，将缓冲区中的数据重置为默认值。在 OpenGL 里，有多种类型的缓冲区，如颜色缓冲区、深度缓冲区、模板缓冲区等，每个缓冲区都存储着不同类型的信息。

#### 缓冲区标志

#### 1. `GL_COLOR_BUFFER_BIT`

- **含义**：清除颜色缓冲区。颜色缓冲区存储着屏幕上每个像素的颜色信息，清除该缓冲区会将所有像素的颜色设置为之前通过 `glClearColor` 函数指定的清除颜色。默认的清除颜色是黑色（RGB 值为 `(0.0, 0.0, 0.0)`），透明度为 1.0。
- **示例代码**：

```c
// 设置清除颜色为红色
glClearColor(1.0, 0.0, 0.0, 1.0);
// 清除颜色缓冲区
glClear(GL_COLOR_BUFFER_BIT);
```

#### 2. `GL_DEPTH_BUFFER_BIT`

- **含义**：清除深度缓冲区。深度缓冲区用于记录每个像素的深度值（即离相机的距离），清除该缓冲区会将所有像素的深度值设置为之前通过 `glClearDepth` 函数指定的清除深度值。默认的清除深度值是 1.0。
- **示例代码**：

```c
// 设置清除深度值为 1.0
glClearDepth(1.0);
// 清除深度缓冲区
glClear(GL_DEPTH_BUFFER_BIT);
```

#### 3. `GL_STENCIL_BUFFER_BIT`

- **含义**：清除模板缓冲区。模板缓冲区用于实现一些特殊的渲染效果，如裁剪、遮罩等。清除模板缓冲区会将所有像素的模板值设置为之前通过 `glClearStencil` 函数指定的清除模板值。默认的清除模板值是 0。

- **示例代码**：

  ```C
  // 设置清除模板值为 0
  glClearStencil(0);
  // 清除模板缓冲区
  glClear(GL_STENCIL_BUFFER_BIT);
  ```

使用按位或运算符 `|` 组合多个缓冲区标志，一次性清除多个缓冲区。例如，同时清除颜色缓冲区和深度缓冲区：



### `glBegin()`&`glEnd()` 

* 用于定义图元（基本图形元素）的函数对。

* `glBegin` 函数用于开始定义一组图元，而 `glEnd` 函数用于结束这组图元的定义。

* 在 `glBegin` 和 `glEnd` 之间，可以使用 `glVertex` 等函数来指定图元的顶点信息。
  
**实例**：

```python
    glClear(GL_COLOR_BUFFER_BIT | GL_DEPTH_BUFFER_BIT);

    # 开始定义三角形图元
    glBegin(GL_TRIANGLES);
    # 指定第一个三角形的三个顶点
    glColor3f(1.0, 0.0, 0.0); # 设置颜色为红色
    glVertex3f(-0.5, -0.5, 0.0);
    glVertex3f(0.5, -0.5, 0.0);
    glVertex3f(0.0, 0.5, 0.0);
    # 结束定义三角形图元
    glEnd();
    # 刷新缓冲区，将绘制结果显示到屏幕上
    glFlush();
```

### `glVertex`

#### `glVertex3f`

用于指定三维顶点坐标的函数

```python
glVertex3f(x, y, z);
```

#### `glVertex3fv` 

用于指定三维顶点坐标的函数

```python
v = (1,2,3)
glVertex3fv(v);
```

### `glColor`

用于指定当前绘图颜色，后续使用 OpenGL 进行图形绘制（如绘制点、线、多边形等）时，就会使用这个设置好的颜色。

#### `glColor3f()`

用于指定当前绘图颜色

```python
# 设置绘图颜色为红色
glColor3f(1.0, 0.0, 0.0)
```

#### `glColor3fv()`

用于指定当前绘图颜色

```python
rgb = (1,0,0)
glColor3fv(v);
```

