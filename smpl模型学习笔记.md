模型训练好的参数：

* rest pose template$\bar{\mathbf{T}}$ ———T-pose的vertices
* blend weights $W$———是一个二维的weight矩阵，$\mathbb{R}^{N\times K}$ ,有每个顶点(72)对应每个关节(23)的权重，这是用来做blend skinning时，每一个顶点都会受到关节骨骼的影响，不同骨骼影响的权重就是这个weight。
* shape blend shape$P$———类似PCA原理通过shape参数来控制人的高矮胖瘦
* pose blend shape$S$———
* Regressor from vertices to joit locations$J$———



#### 相关内容

###### Blend Skinning 

混合蒙皮：将mesh表面附着到底层的骨骼结构上。mesh表面的每个顶点是由其邻近骨骼的权重影响变换得到的，这个权重影响就是上面提到的$W$ ，详细参考LBS(Linear Blend Skinning)。这部分内容在skeletal animation部分会用到。



###### Auto-rigging

上面将骨架嵌入mesh的过程称为**rigging**，Auto-rigging是给定一个mesh的集合，推算出骨骼、关节和blend权重。



###### Blend Shapes

一下全是个人理解，可能有偏差。混合变形：将变形与一个base的shape联系起来，在一个rest pose的基础上进行变形，关键是对于特定的pose定义更正的shapes，然后加到base shape上，产生正确的shape



###### Model Formulation

* Mean template(T-pose)$\bar{\mathbf{T}} \in \mathbb{R}^{3N}$ int the zero pose,$\vec{\theta^*}$. T-pose的顶点集合
* Blend weights $W \in \mathbb{R}^{N\times K}$，最后standar blend skinning的权重矩阵

* Blend shape function $B_S(\vec\beta):\mathbb{R}^{\left|\vec{\beta}\right|} \mapsto \mathbb{R}^{3N}$  刻画object shape特征
* Regressor function $J(\vec\beta):\mathbb{R}^{\left|\vec\beta\right|} \mapsto \mathbb{R}^{3K}$ 是一个由shape参数$\beta$到joint locaion的变换矩阵，从不同的pose中学习而来。
* Pose-dependent blend shape function$B_P(\vec\theta):\mathbb{R}^\vec\theta \mapsto \mathbb{R}^{3N}$ 用来实现“姿态-依赖”的变形

上述函数生成的corrective blend shape加到rest pose上。最后一个standard blend skinning function$W(\cdot)$ 用于旋转在以各个关节为中心的顶点，并使用blend weights进行平滑。

最后总体的模型：
$$
M(\vec\beta,\vec\theta;\Phi):\mathbb{R}^{\left|\vec\theta\right| \times \left|\vec\beta\right|} \mapsto \mathbb{R}^{3N}
$$
输入只有shape参数$\beta$和pose参数$\theta$，$\Phi$是上述介绍的学到的五个参数