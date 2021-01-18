# Novel View Synthesis

> or Image-based Rendering

![image-20201224092542124](ideas.assets/image-20201224092542124.png)

## NeRF

> Neural networks as a volume representation, using volume rendering to do view synthesis
>
> A method that achieves state-of-the-art results for synthesizing novel views of complex scenes by optimizing an underlying continuous volumetric scene function using a sparse set of input views.
>
> [NeRF](https://www.matthewtancik.com/nerf)

- Key points

  - continuous neural network as a volumetric scene representation (5D = xyz + direction)

    - ![image-20201223204837563](ideas.assets/image-20201223204837563.png)
    - neural network replaces large N-d array
    - MLP使用8个完全连接层（ReLU激活，每层256个通道）处理输入，输出σ和256维特征向量。然后，将此特征向量与摄像机视角连接起来，传递到4个附加的全连接层（ReLU激活，每层128个通道），以输出视点相关的RGB颜色。

  - use volume rendering model to synthesize new views, optimize using rendering loss for one scene (no prior training)

    - ![image-20201224195814043](ideas.assets/image-20201224195814043.png)

    - generate views with traditional volume rendering

    - <img src="ideas.assets/image-20201224201050048.png" alt="image-20201224201050048" style="zoom:50%;" />

      <img src="ideas.assets/image-20201224202439992.png" alt="image-20201224202439992" style="zoom: 67%;" />

      - Sigma parameterization for continuous opacity, 沿着camera ray 的每一步步长可以不一样, 步长会影响到分辨率
      - 分两步

    - optimize with gradient descent on rendering loss

      <img src="ideas.assets/image-20201224201553776.png" alt="image-20201224201553776" style="zoom:50%;" />

- position embedding 在实验中发现假如只是输入position, 输出会很模糊(over smooth), 因为好像神经网络只能学到低频的东西. 所以NeRF把输入做了embedding. 就是将3d的输入映射到一个高维的空间去

  - 将每个输入的坐标映射到一个更高的维空间中，这使得我们能够成功地优化神经辐射场，以表示高频场景内容。

- 用神经网络来拟合一个类似voxel的模型

- 体模型由3D grid中的每个格点(体素voxel)构成, 每个体素有颜色(RGB值)+透明度(α值)属性, NeRF的想法就是用一个全连接神经网络来<u>拟合出一个连续的体素表示</u>. 这个全连接网络输入想要的位置(x, y, z), 以及看的角度(φ, ψ), 输出该位置的颜色(r, g, b)和该点的透明度/density(α)

- 需要输入角度是因为要拟合这个场景的光照

- ![img](ideas.assets/v2-2feabdae3730faa57d1521f9b11e9f5f_720w.jpg)

- <img src="ideas.assets/image-20201223204103234.png" alt="image-20201223204103234" style="zoom: 50%;" />

  物体外的点是0, 内的是1

- ![image-20201223212902868](ideas.assets/image-20201223212902868.png)

  - 在物体边缘采样更多

### Pipeline

1. 让摄像机光线穿过场景生成一组采样的三维点
2. 使用这些点及其相应的二维观察方向作为神经网络的输入，生成一组颜色和密度的输出
3. 使用传统的 volume rendering 技术将这些颜色和密度累积到二维图像中

![image-20201228101610821](ideas.assets/image-20201228101610821.png)

- 这个volume rendering的函数是可微的, 所以目标就是最小化 预测的颜色值 - ground truth 

### Positional encoding

- why
  - 要表示更高频的函数, 不然会oversmooth

- 作用: map each input 5D coordinate into a higher dimensional space. 

### Hierarchical sampling

> 分层采样

- why
  - 高分辨率的采样频率要高很多, 使用分层采样能减少采样次数

###  Structure

1. 输入: 3D coordinate $\bold{x} = (x, y, z, θ, φ)$ (位置, 方向)
2. 中间: 8 fully connected layers (ReLU, 256 channels per layer)
3. 输出: $\bold{\sigma}$(向量在当前camera ray的贡献值, camera ray上所有向量的贡献值加起来是1), a 256-dimensional feature vector 
4. 输入: the 256-dimensional feature vector, camera ray's view direction
5. 中间: fully connected layer (ReLU, 128 channels)
6. 输出: view-dependent RGB color (颜色)

### Math

期望的camera ray $\bold{r} = \bold{o} + t\bold{d}$ 的颜色 $C(\bold{r})$ 算法: 
$$
C(\bold{r}) = \int_{t_n}^{t_f}
T(t)\;
\sigma(\bold{r}(t))\;
\bold{c}(\bold{r}(t), \bold{d})\;dt,\\
\text{where}\;
T(t) = exp(-\int_{t_n}^t\sigma(\bold{r}(s))\;ds).
$$

- $t_n$: near bound
- $t_f$: far bound
- $T$: 累计透过率 the accumulated transmittance along the ray from $t_n$ to $t$ (the probability that the ray travels from $t_n$ to $t$ without hitting any other  particle)

实际的颜色 $\hat{C}(\bold{r})$ 算法:
$$
\hat{C}(\bold{r}) = \sum_{i=1}^{N}
T_i(1-exp(-\sigma_iδ_i))\bold{c}_i, \;
\\\text{where}\;
T_i = exp(-\sum_{j=1}^{i-1}\sigma_jδ_j),
\\\text{where}\; δ_i = t_{i+1}-t_i
$$

- $δ_i$: 两个相邻样本的距离

### Questions

- [ ] 不用卷积, 参数数量不会爆炸吗

分成了两个网络

- [ ] 这篇论文是怎么应用可微分渲染的?

optimize the scene representation by minimizing the error of rendering all camera rays from a collection of standard RGB images 

把一个static的场景表示为一个连续的5D函数

- [ ] 为什么半球形的采样没有深度估算误差造成的问题， 深度不也是网络预测出来的吗

深度也是网络预测出来的, 但是不一定和实际的深度一样, 只是看起来没问题, 

- [x] 输出的数据是什么样的， RGB吗? 有深度吗

RGB, 无深度

- [x] 球形的采样是不是要建立3D模型

好像是由一系列向量构成的一个场景的volumetric representation, 每个向量都有($x, y, z, \theta, \phi$), 位置和方向, 同一个camera ray上的向量排成一条线, 然后优化这个vector-valued function. 回想ray-tracing, 图像不就是通过发射一根根光线构成的吗

- [ ] 向量的方向都是从camera到物体的, 优化后也是, 那变换视角后, 这些向量还能用吗, 如果用, 怎么选用那个camera ray 上的向量

density(σ) 只和位置有关, color 和位置和相机的视角都有关

- [x] 如果是一个体模型, 每个体素有一个颜色, 那么当视角发生变化的时候, 颜色如何跟着发生变化 不是还和输入的视角有关吗 

是和view direction有关, 所以每个体素?不是一个颜色, 想想Lumigraph

- [x] 那相机都在一个平面有深度吗

有

- [x] 每个像素是怎么算出来的

用体渲染的技术, camera ray 上的vector的值加起来

渲染一个视角就是计算每个像素的$C(\bold{r})$

- [ ] 高频信息如何处理 用更多的 voxel 吗
- [ ] 高频场景如何减少存储空间
- [ ] voxel 和向量什么关系
- [ ] 如果是σ和位置和视角有光, color只和位置有关呢
- [ ] 是不是分成了两个网络来训练 如果是, 为什么



### Todo

- [ ] 看看https://github.com/bmild/nerf跟unity的结合
- [ ] 看看[issue](https://github.com/bmild/nerf/issues)里的问题

### Reference

- [图形学新高潮? NeRF 笔记 - 知乎 (zhihu.com)](https://zhuanlan.zhihu.com/p/187541908)
- [非卷积5D中文翻译及学习笔记](https://blog.csdn.net/ftimes/article/details/105890744)
- [Matthew Tancik: Neural Radiance Fields for View Synthesis - YouTube](https://www.youtube.com/watch?v=dPWLybp4LL0&ab_channel=AndreasGeiger) 
- [Neural Rendering (CVPR 2020) - Morning Session](https://www.youtube.com/watch?v=LCTYRqW-ne8&ab_channel=NeuralRendering)

- [翻译+笔记 NeRF](https://blog.csdn.net/ftimes/article/details/105890744)
- [翻译+笔记 NeRF 2](https://www.flyinghuster.com/[%E8%AE%BA%E6%96%87%E8%A7%A3%E8%AF%BB]NeRF-Representing%20Scene%20as%20Neural%20Radiance%20Fields%20for%20View%20Synthesis/)

## NeRF-W

> NeRF in the wild

- 可能有两个误差
  - 可能有遮挡, 所以要考虑一个参数, 这个参数只会影响到颜色, 不会影响到σ
  - 空间位置可能不同, 这会影响到σ, 颜色
- 都是用的网络, 没有图形学

### Questions



### Reference

[NeRF-W bilibili](https://www.bilibili.com/video/BV1Qi4y1u7Es?from=search&seid=501675493729586449)

- Target: given a set of photographs of an object or a scene, estimate the most likely 3D shape that explains those photographs, under the assumptions of known materials, viewpoints, and lighting conditions
- There exist many cues that can be used to extract geometry from photographs: <u>texture, defocus, shading, contours, and stereo correspondence</u>.

# MVS

> Multi-View Stereo
>
> 多视图三维重建

## Pipeline

multi-view stereo pipeline. 

<img src="ideas.assets/image-20210104103320693.png" alt="image-20210104103320693" style="zoom:50%;" />

1. imagery collection
2. camera parameters estimation
3. 3D geometry reconstruction
4. textured 3D geometry

## Imagery Collection

![image-20210104111437852](ideas.assets/image-20210104111437852.png)

- One can roughly classify MVS capture setups into three categories
  - Laboratory setting,
  - Outdoor small-scale scene capture,
  - Large-scale scene capture using fleets or crowd-sourcing, e.g. cars, planes, drones, and Internet.

## Camera Parameters Estimation

> Camera Parameters: 
>
> - camera pose information consisting of location and orientation
> - camera intrinsic properties such as focal length and pixel sensor size

### Camera Projection models

![image-20210104135306940](ideas.assets/image-20210104135306940.png)

- [Camera Intrinsic & Extrinsic矩阵](http://zhixinliu.com/2016/11/15/2016-11-15-camera-intrinsic/)
- [MVS Tutorial p18]() 

### SfM

> Structure from Motion
>
> compute the camera parameters

- commonly used to compute camera models of unordered sets of images, usually offline. 

- SfM重构的思想是利用相机运动轨迹来估算相机参数. 相机在不同视点摄取多幅图像，利用这些图像计算出相机的位置信息以及运动轨迹，从而在空间坐标系下生成三维点云，恢复出物体的空间结构．由于初步匹配过程形成的特征点较为粗糙，因此在估算相机参数之前，<u>常用几何约束删除匹配错误的特征点对</u>．SfM重构的方法主要有增量式和全局式两种

- SfM算法是一种基于各种收集到的无序图片进行三维重建的离线算法。在进行核心的算法structure-from-motion之前需要一些准备工作，挑选出合适的图片

  1. 从图片中提取焦距信息(之后初始化BA需要)
  2. 利用SIFT等特征提取算法去提取图像特征
  3. 用KD-tree模型去计算两张图片特征点之间的欧式距离进行特征点的匹配，从而找到特征点匹配个数达到要求的图像对
  4. 对于每一个图像匹配对，计算对极几何，估计F矩阵并通过ransac算法优化改善匹配对。这样子如果有特征点可以在这样的匹配对中链式地传递下去，一直被检测到，那么就可以形成轨迹。
  5. 进入structure-from-motion部分

  关键的第一步就是选择好的图像对去初始化整个BA过程。首先对初始化选择的两幅图片进行第一次BA，然后循环添加新的图片进行新的BA，最后直到没有可以继续添加的合适的图片，BA结束。得到相机估计参数和场景几何信息，即稀疏的3D点云。其中两幅图片之间的bundle adjust用的是稀疏光束平差法sba软件包，这是一种非线性最小二乘的优化目标函数算法。

- input: a set of images

- output: 

  - the camera parameters of every image
  - a set of 3D points visible in the images which are often encoded as **tracks** (A track is defined as the 3D coordinates of a reconstructed 3D point and the list of corresponding 2D coordinates in a subset of the input images. )

- Most of the current state-of-the-art SfM algorithms share the same basic processing pipeline

  ![image-20210104150922712](ideas.assets/image-20210104150922712.png)

  feature detection, feature matching, track generation, structure-from-motion and bundle adjustment

- One of the key developments for SfM was the use of RANSAC [61] to robustly estimate the epipolar geometry between two or three views given noisy matches.

- every image has to be matched to every other image, which is computationally very expensive. Efficient indexing combined with high quality **descriptors** allowed efficient pairwise matching of millions of images. Further work on simplifying the connectivity graph of the tracks (简化连通图的迹点) and parallelization (并行) lead to the current state-of-the-art SfM pipelines used in the industry. 

#### 增量式重构

- 增量式重构是从两张图像中重建出部分场景以及两相机的***R***（旋转矩阵）、***T***（平移矩阵），然后添加图像，利用PnP计算出第三幅图像的***R***、***T***， 通过三角化重建出更多的场景．由于在求位姿与三维点时会有大量噪声干扰，后续计算结果会发生漂移，因此引入BA（Bundle Adjustment）算法进行优化．在每次添加图像完成三角化后都需要进行优化．
- 步骤
  1. 初始化
  2. PnP解算
  3. 三角化
  4. BA算法优化．其中较为重要的步骤是利用PnP算法求解相机位姿．(PnP有很多种类，如P3P、EPnP、DLT、UPnP和MRE

[Bundle Adjustment](https://blog.csdn.net/OptSolution/article/details/64442962)

### VSLAM

> Visual Simultaneous Localization and Mapping

- specializes in computing the location of a camera from a video stream, usually real-time.

## Reference

- [三维重建算法研究综述](http://nxdxb.cnjournals.org/ch/reader/download_pdf.aspx?file_no=20200509&year_id=2020&quarter_id=5&falg=1)

## ?

- [ ] 

# Texturing

## pipeline

1. determine the visibility of faces in the input images

## MRF

> Markov Random Field
>
> 马尔可夫随机场，也叫马尔可夫网。无向图模型也叫马尔科夫随机场(Markov Random Fields)或马尔科夫网络

- 马尔可夫性质：它指的是一个随机变量序列按时间先后关系依次排开的时候，第N+1时刻的分布特性，与N时刻以前的随机变量的取值无关, 只与N时刻的随机变量的取值有关。
- 随机场：当给每一个位置中按照某种分布随机赋予相空间的一个值之后，其全体就叫做随机场。我们不妨拿种地来打个比方。其中有两个概念：位置（site），相空间（phase space）。“位置”好比是一亩亩农田；“相空间”好比是种的各种庄稼。我们可以给不同的地种上不同的庄稼，这就好比给随机场的每个“位置”，赋予相空间里不同的值。所以，俗气点说，随机场就是在哪块地里种什么庄稼的事情。
- 马尔可夫随机场：马尔科夫随机场是具有马尔科夫特性的随机拿种地打比方，如果任何一块地里种的庄稼的种类仅仅与它邻近的地里种的庄稼的种类有关，与其它地方的庄稼的种类无关，那么这些地里种的庄稼的集合，就是一个马尔可夫随机场。
- 在随机场的基础上添加马尔科夫性质，从而得到马尔科夫随机场。把马尔科夫随机场映射到**无向图**中，此无向图中的节点都与某个随机变量相关，连接着节点的边代表与这两个节点有关的随机变量之间的关系，所以，马尔科夫随机场其实表达出随机变量之间有些关系因素是必须要考虑的，而另外则有些是可以不用考虑的。<u>马尔科夫随机场的某个随机变量，仅仅只与其相邻的随机变量有关，与那些不相邻的随机变量无关。</u>
- [马尔可夫随机场_百度](https://baike.baidu.com/item/马尔可夫随机场/3287733#reference-[1]-2313875-wrap)
- [计算机视觉方向简介 | 多视角立体视觉MVS (careerengine.us)](https://posts.careerengine.us/p/5e1b48bf626378473bdf97f5)
- MVS中的MRF是以mesh面为

## Energy Formulation

> 能量函数, 能量越小越稳定, 和cost function的意义相似

why: :question: smoothing or stereo correspondence problem
$$
E(l) = \sum_{F_i\in Faces}E_{data}(F_i, l_i) + \sum_{(F_i, F_j)\in Edges}E_{smooth}(F_i, F_j, l_i, l_j)
$$

- $l$: label $l$ assigns a view $l_i$ to be used as texture for each mesh face $F_i$
- $l_i$: view
- $F_i$: mesh face
- $E_{data}(\cdot, \cdot)$: 数据项data term, prefers "good" views for texturing a face
- $E_{smooth}(\cdot, \cdot, \cdot, \cdot)$: 平滑项smoothness term, minimizes seam(edge between faces textured with different images) visibility. 
- $E(l)$ 越小越好: 通过 graph cuts 和 alpha expansion 来最小化

## Graph Cuts

- why: 它可在保持相关的尖锐不连续性（sharp discontinuities）的同时，加强分段平滑性

- ![img](ideas.assets/2012110618452932.jpg)

- 一张image可以看作是一个矩阵, 图中的每个像素就是矩阵中的一个位置，这个像素可以看做是图中的一个顶点。把相邻顶点之间用短线(有向或无向)连接起来就形成了边，也就构成一幅Graph了。

- 边的权值由平滑项和数据项组成，这2部分的比重用1个系数来平衡，

  - 平滑项B(A)主要体现顶点像素和其相邻区域像素之间值的变化强度，如果变化剧烈说明这两者很有可能出于边缘部分，则被分割开的可能性比较大，:question:而按照最小割的分割原理，这时2者的平滑项权值应该较小
  - 数据项R(A)则表示对应顶点属于前景或者背景的惩罚项

  ![img](ideas.assets/2012110618460647.png)

- [Graph Cuts初步理解 - 钟离踏雪 - 博客园](https://www.cnblogs.com/saliency/p/3659026.html)

- [Graph Cuts in Vision and Graphics概述 - 知乎 (zhihu.com)](https://zhuanlan.zhihu.com/p/210236545?utm_source=qq)

- Graph Cuts中的Cuts是指这样一个边的集合，很显然这些边集合包括了上面2种边，该集合中所有边的断开会导致残留”S”和”T”图的分开，所以就称为“割”。如果一个割，它的边的所有权值之和最小，那么这个就称为最小割，也就是图割的结果。:question:而福特-富克森定理表明，网路的最大流max flow与最小割min cut相等。所以由Boykov和Kolmogorov发明的max-flow/min-cut算法就可以用来获得s-t图的最小割。这个最小割把图的顶点划分为两个不相交的子集S和T，其中s ∈S，t∈ T和S∪T=V 。这两个子集就对应于图像的前景像素集和背景像素集，那就相当于完成了图像分割。

- 图像分割可以看成pixel labeling（像素标记）问题，目标（s-node）的label设为1，背景（t-node）的label设为0，(s, t最后要分离), 这个过程可以通过:question:最小化图割来最小化能量函数得到。那很明显，发生在目标和背景的边界处的cut就是我们想要的（相当于把图像中背景和目标连接的地方割开，那就相当于把其分割了）。同时，这时候能量也应该是最小的。假设整幅图像的标签label（每个像素的label）为L= {l1,l2, , , , lp}，其中li为0（背景）或者1（目标）。那假设图像的分割为L时，图像的能量可以表示为：

  ![image-20210112212344236](ideas.assets/image-20210112212344236.png)

  其中，R(L)为区域项（regional term），B(L)为边界项（boundary term），而a就是区域项和边界项之间的重要因子，决定它们对能量的影响大小。如果a为0，那么就只考虑边界因素，不考虑区域因素。E(L)表示的是权值，即损失函数，也叫能量函数，图割的目标就是优化能量函数使其值达到最小。

- [Graph Cuts 图分割学习 - 知乎](https://zhuanlan.zhihu.com/p/58185005)

- 

- [ ] 如何和MRF结合起来

  <img src="ideas.assets/image-20210112215248701.png" alt="image-20210112215248701" style="zoom: 67%;" />

  [Grouping and segmentation (iitd.ac.in)](https://web.iitd.ac.in/~sumeet/14.pdf)

  通常是相邻的像素点或者体素点, 但这篇论文用的相邻的mesh face

- [ ] 贴纹理需要又不是图像分割, 这里应该如何修改

## α-expansion

- why: minimize energy 能量最小化
- 是一个[非凸优化](https://www.zhihu.com/question/20343349)问题, 求全局最优是NP-hard的, 可用蒙特卡洛?
- *Fast Approximate Energy Minimization via Graph Cuts*
- [Alpha-expansion and Alpha-beta-swap Algorithm Flow-CSDN](https://blog.csdn.net/nothinglefttosay/article/details/48554555)

# ghost

## Mini Cut

## Gradient Magnitude

[math - What is the gradient orientation and gradient magnitude? - Stack Overflow](https://stackoverflow.com/questions/19815732/what-is-the-gradient-orientation-and-gradient-magnitude/19816362)

## Mean-Shift

- 简单说，就是有一个点 x,它的周围有很多个点 x_i 我们计算点 x 移动到每个点 x_i 所需要的偏移量之和，求平均，就得到平均偏移量 m, （<u>该偏移量的方向是周围点分布密集的方向</u>）该偏移量是包含大小和方向的。然后点 x 就往平均偏移量方向移动，再以此为新的起点不断迭代直到满足一定条件结束。

- mean-shift的算法流程是： 

  1. 选取中心点 x，以半径 h 做一个高维球（如果我们是在图像或者视频处理中，则是2维的窗口，不限定是球，可以是矩形），标记所有落入窗口内的点为  x_i 
  2. 计算 m，如果 m 的值小于阈值或者是迭代次数到达某个阈值，则停止算法，否则利用上面求圆心的公式更新圆点，继续步骤1

  

- [meanshift算法图解_csdn](https://blog.csdn.net/csdnforyou/article/details/81161840)

- [Meanshift，聚类算法 - Liqizhou - 博客园 (cnblogs.com)](https://www.cnblogs.com/liqizhou/archive/2012/05/12/2497220.html)