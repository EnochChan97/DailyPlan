# Lecture 04 Transformation con

补充内容

旋转操作默认是逆时针旋转，旋转-a角度的矩阵等号旋转a角度的转置，在定义上旋转-a和旋转a正好互相逆。所以旋转矩阵是``正交矩阵``

## View/Camera transformation

什么是视图变换？简单而言确定相机的位置和摆放

- 如何进行识图变换？

- Define the camera first

    >Position \hat e
    >Look at / gaze direction \hat g
    >Up direction \hat t

我们可以把相机固定不动放在原点（约定俗成的位置），朝-z方向看，向上方向是y

如何将任意位置的相机放到上述位置？

1.平移 \hat e 到原点：做平移变换

2.旋转gaze direction 到-z ，旋转Up direction 到 Y轴
（可以使用旋转的逆变换）

## Projection transformation

图形学中的投影：3D to 2D

透视投影是在一个点投射成四棱锥形成；正交显示若将相机放于无限远，远、近平面将无限接近。

### Orthographic projection

一个简单的理解方式：相机固定在原点，朝-z方向看去，向上指向y，drop z坐标，然后平移缩放到[-1,1]的平面中

### Perspective projection

满足近大远小，从一个点往一个方向上去看，得到一个四棱锥

简单地说就是将Frustum的远平面挤压成跟近平面一样大的平面而z不变，在进行正交投影
