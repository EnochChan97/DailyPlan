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

# Lecture 5 Rasterization1(Triangles)

## What's after MVP

Model transformation(placing objects)
View transformation(placing camera)
Projection transformation
-正交投影（搞到一个[-1，1]的立方体中）
-透视投影（先转换到正交投影，再做正交投影）

## Canonical Cube to Screen

屏幕：一个二维数组,数组中的每一个元素为每一个像素。

光栅(Raster) ：德语中的屏幕的意思

Rasterize ：Drawing onto the screen

将一个立方体“放到”屏幕上时，z坐标方向暂且不管，将x,y坐标方向由[-1,1]拉伸到[]0,width]和[0,height] (由一个变换矩阵变换)

## 光栅化（三角形）

判断三角形与像素的位置关系，更确切来说，判断像素中心点与三角形的位置关系

A Simple Apporach:Sampling

通过判断屏幕上所有的的像素的坐标中心是否在三角形内部，来决定像素的color。

![alt](https://github.com/EnochChan97/DailyPlan/blob/master/assets/sampling.png)

如何判断一个点是否在三角形内部？

利用向量叉积！对于三角形ABC和P点，判断向量AB、BC、CA和AP,BP,CP的叉积是否为同号，若为同号，则P点在三角形内部。对于在边界上的点，可以自行定义。（对于openGL和directX，落在上边和左边的点算在三角形内部：即涂上不涂下，涂左不涂右，可以保证不会漏掉也不会多涂）

单纯这样的光栅化会造成一个图形的走样：锯齿，为了解决这个问题会提出抗锯齿或反走样的方法。

![Jaggis](https://github.com/EnochChan97/DailyPlan/blob/master/assets/Jaggies.png)

# Lecture 6 Rasterization2

## 计算机图形学中的采样瑕疵(artifact)

> 在图形学里，artifacts指的是Errors / Mistakes / Inaccuracies，泛指一些不准确或者与我们预期不一样的结果

* 锯齿---空间中的采样

* 摩尔纹---下采样图片产生的瑕疵

* 车轮效应---空间中的采样

瑕疵背后的原因：`Signals are changing too fast but sampled too slowly`

### Antialiasing Idea:Blurring(Pre-Filtering) Before Sampling

一种反走样的方法是对原图信号做一个模糊处理(滤波)，然后再采样

![blurring1](https://github.com/EnochChan97/DailyPlan/blob/master/assets/blurring1.png)




## Frequency Domain(频域)

> 傅里叶级数展开：任何一个周期函数或周期信号分解成一个(可能由无穷各元素组成的)正弦函数和余弦函数表示

傅里叶变换(不理解)

![blurring1](https://github.com/EnochChan97/DailyPlan/blob/master/assets/FourierTransform.png)

## 走样

前面提到走样的原因是信号变化太快，而采样太慢。观看这句话可能不太能理解，但是结合下面的图应该就很好理解了。

可以看到有五条不同的绿色曲线，分别表示不同的信号。黑色的点表示每隔一段时间对信号采样得到的点。可以看到对于\(f_1(x)\)，因为他的频率较慢，所以我们通过连接采样得到的黑点其实大致上还是能还原出原信号的。而随着信号频率不断增加，以\(f_5(x)\)为例，此时很显然我们无法还原信号了。

![blurring1](https://github.com/EnochChan97/DailyPlan/blob/master/assets/zouyang.png)

对于高频信号的下采样，可能跟某个低频信号的采样是一样的，即不同的两个信号采样之后可能是相同的，这就是走样出现的原因。

### Filtering=**Geting rid of** certain frequency contents

> 滤波表示去除某种特定的频率（如高频、低频）信息。

下图的右边是由左边图片经过傅里叶变换得到的频谱图，中间为低频，越往外为高频。

![blurring1](https://github.com/EnochChan97/DailyPlan/blob/master/assets/6-1.png)

而如果我们把低频信息去掉，只让高频信息通过，得到下图的效果(高通滤波)。

高频信息可以理解为图片中相邻像素值之间变化剧烈的地方，一般出现在物体的边缘，反之低频就是变化不剧烈的地方。所以下图中保留了高频，就可以看到人物的轮廓很明显。
![blurring1](https://github.com/EnochChan97/DailyPlan/blob/master/assets/6-2.png)

如果把高频信息去掉，让低频信息通过，得到如下的图（低频滤波），可以看到人物的边缘不是很分明，起到了模糊的效果。

![blurring1](https://github.com/EnochChan97/DailyPlan/blob/master/assets/6-3.png)


## 卷积

在图片上（时域上）实现滤波的操作成为卷积（平均）
卷积操作不多说，即用卷积核在像素上“滑动”对相邻像素取加权平均来达到模糊的效果。

> 卷积定理
时域（spatial domain）上的卷积等价于频域（frequency domain）上的乘积；
时域上的乘积等价于频域上的卷积；
比如我对一张图片做卷积操作，等价于我们先把图片和卷积核通过傅里叶变换转化到频域上，然后在频域上将两者相乘（可以理解成乘了一个mask），最后将相乘的结果做逆傅里叶变换即可。

而时域上的卷积核大小跟频域上的频率大小关系：卷积核越大对应频域上的频率越小，越起到“模糊”的效果

## 采样

> 采样等价于重复频率信息。
Sampling = Repeating Frequency Contents

下图左侧(a,c,e)表示时域上的操作，右侧(b,d,f)表示频域上的操作。其中(a)表示时域信号，(b)表示信号在频域上的样子（这里画成三角形是为了好理解，什么样子其实无所谓，不影响理解）。

(c)表示冲激采样，即每隔一段时间就采样一次，它在频率上的其实也和冲激信号长得一样(d)。

在时域上的采样(e)其实就是信号和冲激采样相乘\(x_a(t)\times p_\delta(t)\),那么对应到频域就是二者做卷积(f)。

得到的效果可以看到在频域上其实就是对原频域信号不断的重复。

![blurring1](https://github.com/EnochChan97/DailyPlan/blob/master/assets/6-4.png)


当然上面给出的是一种比较理想的情况，如果采样间隔较长（或者说采样较慢）的话则会导致下面sparse sampling的情况，即频域信号之间在重复时发生了混叠，及导致了aliasing现象。

![blurring1](https://github.com/EnochChan97/DailyPlan/blob/master/assets/6-5.png)

（注意：上图表示的是频域上的信号表示，横轴表示频率，纵轴表示幅度，即信号强度）

## 反走样

既然走样是因为采样速率低导致的，那么解决反走样的办法就可以从提高采样速率入手，但实际上这一种方法不现实。

一种代替的方法就是对信号做截断处理，通过截断高频的信号，避免混叠现象的产生

![blurring1](https://github.com/EnochChan97/DailyPlan/blob/master/assets/6-6.png)


那么对三角形模糊处理具体是怎么做的呢？其实就是在频域上使用低通滤波将器乘以这个三角形的频域信号即可，也就是模糊操作（高通滤波的效果是保留轮廓），那对应到时域上我们可以使用一个像素大小的卷积核对单个像素做卷积操作，什么意思呢？

下图给出了单个像素内被三角形覆盖面积的不同情况：

以最左边的像素为例，黑色表示三角形覆盖的面积，可以看到大约是覆盖了1/8的面积，那么做平均之后这个像素对应的亮度值就是纯白色的7/8。

![blurring1](https://github.com/EnochChan97/DailyPlan/blob/master/assets/6-7.png)

##  Antialiasing By Supersampling (MSAA)

对像素内部做平均计算的具体方法叫做MSAA(多重采样反走样)

MSAA的大致思路是从**逻辑**上把一个像素点再细分，比如把一个像素点划分成4个child-points (a→b)。然后通过child-point覆盖的数量来计算对应的颜色(c,d)

![blurring1](https://github.com/EnochChan97/DailyPlan/blob/master/assets/6-8.png)

还有一些其他的反锯齿的方法，不多做介绍。。。累死了，这节课有点难
FXAA(Fast Approximate AA)
TAA(Temporal AA)

