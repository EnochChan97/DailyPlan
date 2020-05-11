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

* mean template(T-pose)$\bar{\mathbf{T}} \in \mathbb{R}^{3N}$ int the zero pose,$\vec{\theta^*}$
* Blend weights $W \in \mathbb{R}^{N\times K}$

* blend shape 

