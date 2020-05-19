# 2020/5/19

* 日常满课。。。

* 完成了明天开会的报告

  

### To Do

* 阅读骨骼蒙皮动画的原理解析的博客
* 看Pinocchio的论文

# 2020/5/17

最近真的每天连轴转赶作业。。工程数学真的好顶！

这几天在科研上，配好了代码环境，代码输入的关节数是15，如果要用自己的keypoints数据，需要根据关节数量，用二维骨架三角化得到内嵌的三维骨骼，以及用Pinocchio重新生成骨骼和顶点的对应关系。其次代码的model没有用smpl模型，所以开完组会之后，周的的代码方案暂时先搁置。下一步的工作是，尝试另外的思路就是简单地直接通过每一帧的pose参数$\theta$ 来驱动smpl变化移动。参数theta可以尝试minimalIK solver，给定keypoints得到预测的smpl 参数。

### To Do

* 周一需要定下通过pose参数驱动smpl转圈的方案，最好周二出结果。
* 周三汇报的ppt

# 2020/5/12

* 主要将snapshot的keypoints从hdf5格式转换为json格式的文件。关节点为coco输出格式(18个关节点)

### To Do

* 配代码的环境
* 找到代码的输入骨架的格式。



# 2020/5/11

* smpl论文，研究模型。

### To Do

- smpl模型的操作，如何通过beta、theta生成模型的pose和shape
- 研究周代码，IK solver 给定pose生成对应的参数



# 20205/9

- 使用OpenGL+pygame成功加载带有纹理的obj模型，可以调整好相机和object的位置，但是目前还不能使物体旋转起来。。待解决
- blender可以完美运行，再找方法把每一帧保存就好了。相机参数暂时不知道需不需要考虑。
- OpenGl学习笔记。



### To Do

- OpenGL+pygame 将模型旋转起来以及转换成image保存的方法
- 进展报告周报
- 法语作业



# 2020/5/8

* 机器学习大作业搞完

## To do

* 研究学习OpenGL是否可以做animation
* GAMES101

# 2020/5/6

> 这几天没有好好写日志。。该打**今天发现了一个巨好用的markdown editor** 写笔记的动力更足了呢！

* 机器学习平时作业---GAN综述
* 机器学习大作业---20%
* animation方案之一，用blender来手动render一个video sequences

## To do

* 继续写ML大作业
* 研究学习OpenGL是否可以做animation
* 法语作业

# 2020/4/27

* Lecture 6 Rasterization(反走样)
* 调研数据集
* 法语作业

## To do

* **看keras手册，分析octopus代码！！！**
* 电商系统设计文档

# 2020/4/25

* GAMES101 Lecture5 Rasterization

## To do

* 调研数据集

# 2020/4/23

* 跑出了带纹理的模型，面部细节不是很好。纹理贴图不是很懂，需要学习一下纹理坐标和顶点坐标的对应关系是如何得到的

# 2020.4.21

* 跑octopus的pipeline，结果很奇怪

* 结合keras中文文档，阅读octopus源码。

## To do

* 分析octopus的代码模块结构

* 法语课文，单词 & 作业4，5，6

* 设计模式9-12章课后题

# 2020.4.20

GAMES101 4.Transformation Cont.

TF 第二章
