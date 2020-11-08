介绍

CG和CV的区别

![image-20200927092304202](GAMES101.assets/image-20200927092304202.png)

# 基础知识

## dot prodct

> [link](https://zh.wikipedia.org/wiki/%E7%82%B9%E7%A7%AF)



## cross product

> 叉乘

<img src="GAMES101.assets/image-20200927091429112.png" alt="image-20200927091429112" style="zoom:50%;" />

- Cross product is orthogonal to two initial vectors：叉乘会得到一个新的向量，这个向量同时垂直于a和**b**
- Direction determined by right-hand rule：新向量的方向由右手定则来确定（右手的四个手指弯曲使其在水平面同时垂直于**a**、**b**向量，如图中红线所示，拇指指向的方向为新向量的方向）
- Useful in constructing coordinate（坐标） systems

![image-20201011194835883](GAMES101.assets/image-20201011194835883.png)

### 计算

![image-20200927091747964](GAMES101.assets/image-20200927091747964.png)

- 右手坐标系，$\overrightarrow{x}× \overrightarrow{y} = \overrightarrow{z}$；

- 左手坐标系，$\overrightarrow{x}× \overrightarrow{y} = -\overrightarrow{z}$，OpenGL用的是左手坐标系

- 向量自己跟自己叉乘得到的是一个0**向量**，不是0

- <img src="GAMES101.assets/image-20200927092858454.png" alt="image-20200927092858454" style="zoom: 50%;" />

  推导过程详见 [link](https://zh.wikipedia.org/wiki/%E5%8F%89%E7%A7%AF)

- <img src="GAMES101.assets/image-20200927092914322.png" alt="image-20200927092914322" style="zoom:50%;" />

  ### 作用

- Determine left / right

  <img src="GAMES101.assets/image-20200927093142389.png" alt="image-20200927093142389" style="zoom:33%;" />

- Determine inside / outside

  <img src="GAMES101.assets/image-20200927093218783.png" alt="image-20200927093218783" style="zoom:33%;" />

# Transformation

- 2D: rotation, scale(缩放), shear
- 3D

## Linear Transforms

所有的线性变换都可以写成下面这样

<img src="GAMES101.assets/image-20200906103200916.png" alt="image-20200906103200916" style="zoom:50%;" />

### shear

<img src="GAMES101.assets/image-20200927102548635.png" alt="image-20200927102548635" style="zoom:50%;" />

垂直方向不变，水平方向偏移ay

但是平移（translation）不能用上面那种形式表示（一个矩阵乘以一个向量），得用下面这种

<img src="GAMES101.assets/image-20200906104509228.png" alt="image-20200906104509228" style="zoom:50%;" />

叫做Affine map = linear map + translation

为了能够统一地表示所有这些操作（旋转，缩放，平移），需要引入齐次坐标(Homogenous Coordinates)

### rotate

逆时针，绕原点

<img src="GAMES101.assets/image-20200927102710121.png" alt="image-20200927102710121" style="zoom:50%;" />

<img src="GAMES101.assets/image-20200906102845197.png" alt="image-20200906102845197" style="zoom:50%;" />

可以找两个特殊点，来推

看看逆时针和顺时针旋转，会发现这两个矩阵刚好互逆($R^T$是$R$的转置)

$R_\alpha= \begin{pmatrix}cos\alpha&-sin\alpha \\ sin\alpha&cos\alpha\end{pmatrix}$

$R_{-\alpha} = \begin{pmatrix}cos\alpha&sin\alpha \\ -sin\alpha&cos\alpha\end{pmatrix} = R^T_\alpha$ 

BTW: 如果一个矩阵的逆等于它的转置，这个矩阵就叫做正交矩阵。

### Homogenous Coordinates

> 齐次坐标

<img src="GAMES101.assets/image-20200927102931286.png" alt="image-20200927102931286" style="zoom:50%;" />

如果是点，最后一个维度的最后加的是1，前面都为0

如果是向量，最后一个维度都为0，因为向量有**平移不变性**（向量只跟长度、方向有关，与起点无关）所有要加0保护，不让平移操作改变它

增加一个维度还有一个好处，就是运算

- vector + vector = vector

- point - point = vector

- point + vector = point （一个点延一个方向移动到另一个点）

- point + point = 变成这两个点之间的中点, 因为

  $\begin{pmatrix}x \\y \\w\end{pmatrix}$是一个2维的点$\begin{pmatrix}x/w\\y/w\\1\end{pmatrix},w\not= 0$

#### scale

$$
S(s_x, s_y) = \begin{pmatrix}s_x&0&0 \\ 0&s_y&0\\0&0&1\end{pmatrix}
$$



#### rotation

$$
R(\alpha) = \begin{pmatrix}cos\alpha&-sin\alpha&0 \\ sin\alpha&cos\alpha&0\\0&0&1\end{pmatrix}
$$



#### translation

$$
T(t_x, t_y) = \begin{pmatrix}1&0&t_x \\ 0&1&t_y\\0&0&1\end{pmatrix}
$$





## Inverse Transform

$M^{-1}$is the inverse of transform $M$ in both a matrix and geometric sense

![image-20200927103005021](GAMES101.assets/image-20200927103005021-1604739240246.png)

## Composing Transforms

<img src="GAMES101.assets/image-20200906123712073.png" alt="image-20200906123712073" style="zoom: 67%;" />



## Decomposing Comples Transforms





## 3D Transforms

![image-20200906124430617](GAMES101.assets/image-20200906124430617.png)

**很重要，如果w不为0，x、y、z都要除以w得到的才是要的点**

![image-20200906124518686](GAMES101.assets/image-20200906124518686.png)

左上角的3*3矩阵还是表示线性变换, $t_x, t_y, t_z$ 还是表示平移。

### scale

> 缩放

<img src="GAMES101.assets/image-20200927084627876.png" alt="image-20200927084627876" style="zoom: 80%;" />

### translation

> 平移

<img src="GAMES101.assets/image-20200927084650757.png" alt="image-20200927084650757" style="zoom: 80%;" />

### rotate 

<img src="GAMES101.assets/image-20200927110737509.png" alt="image-20200927110737509" style="zoom:50%;" />

- $R_x$是绕x旋转，x轴的坐标不变，所以（0，0）位置是1
- 任何旋转都可以分解为绕x, y, z 旋转
- xyzxyz, 三个轴循环对称，x×y得z，y×z得x，z×x得y，是x×z得-y     ？？？

#### Rotation Formula

> Rodrigues’ rotation formula
>
> 罗格里德斯旋转公式？？？

![image-20200927110824432](GAMES101.assets/image-20200927110824432-1604739314094.png)

- **n**是旋转轴：默认是过原点，方向是**n**的方向。如果要沿任意轴旋转，需要先移动到原点再移动回去。
- N那个矩阵其实是向量**n**（可以到上面看叉乘的公式）

## View Transformation

> 观测变换

步骤（用拍照来做比喻）MVP变换

1. **model** transformaiton（模型变换，把要拍照的人都找来）
2. **view/camera** transformaiton（视图变换，找一个好的角度）
3. **projection** transformation（投影，Cheese!）
4. 视口（在下面光栅化部分）

### M

- 调整好模型, 比如先旋转好

### V

> 视图变换
>
> 也叫ModelView Transformation，MVP中的MV

- 假定相机永远在原点，朝向-z方向。如果一开始相机不满足条件，只需移动相机，移动的同时保持相机和物体相对静止即可。

  <img src="GAMES101.assets/image-20200927142718581.png" alt="image-20200927142718581" style="zoom:50%;" />

- 定义相机

  - position 位置：$\overrightarrow{e}$

  - look-at / gaze direction 仰角（垂直）：$\hat{g}$
  - up direction 倾斜角（水平）：$\hat{t}$

- $M_{view}$表示相机要进行变换的矩阵：也就是

  - Translates e to origin 平移到原点

  - Rotates g to -Z 

  - Rotates t to Y

  - Rotates (g × t) To X

    <img src="GAMES101.assets/image-20200927150545736.png" alt="image-20200927150545736" style="zoom: 50%;" />

- $M_{view} = R_{view} T_{view}$，$M_{view}$需要通过平移和旋转得到

  - $T_{view}$ 是平移矩阵，平移到原点，
    $$
    T_{view} = \begin{bmatrix} 1&0&0&-x_e  \\  0&1&0 &-y_e \\ 0&0&1&-z_e \\ 0&0&0&1 \end{bmatrix}
    $$
  
- $R_{view}$是旋转矩阵，作用是：Rotate g to -Z, t to Y, (g × t) to X。但是不好算，只能Consider its inverse rotation: X to (g × t), Y to t, Z to -g
    $$
    R_{view}^{-1} = \begin{bmatrix} x_{\hat{g}×\hat{t}}&x_t&x_{-g}&0  \\  y_{\hat{g}×\hat{t}}&y_t&y_{-g}&0 \\ z_{\hat{g}×\hat{t}}&z_t&z_{-g}&0 \\ 0&0&0&1 \end{bmatrix}
    $$
    
  
  （可以拿向量$\begin{bmatrix} 1\\0\\0\\0 \end{bmatrix}$，$\begin{bmatrix}0\\1\\0\\0 \end{bmatrix}$，$\begin{bmatrix} 0\\0\\1\\0 \end{bmatrix}$分别去做$R_{view}^{-1}$旋转，就可以得到相机原来的位置）
  
  因为旋转矩阵是正交矩阵，旋转矩阵的逆是其转置，所以
  $$
    R_{view} = \begin{bmatrix} x_{\hat{g}×\hat{t}}&y_{\hat{g}×\hat{t}}&z_{\hat{g}×\hat{t}}&0  \\  x_t&y_t&z_t&0 \\ x_{-g}&y_{-g}&z_{-g}&0 \\ 0&0&0&1 \end{bmatrix}
  $$
  

### P

> 投影变换

![image-20200928045708014](GAMES101.assets/image-20200928045708014-1604739362541.png)

#### Orthographic Projection

> 正交投影

- A simple way of understanding 简单的做法

  - Camera located at origin, looking at -Z, up at Y (looks familiar?) 相机位于原点

    ![image-20200928045910940](GAMES101.assets/image-20200928045910940.png)

  - Drop Z coordinate，这就是朝向-Z的好处，只要拿掉Z坐标就得到了投影

  - Translate and scale the resulting rectangle to [-1, 1]$^2$ 为了方便其他计算，也算是约定俗成的，之后可能再做一次缩放

    

- In general 通常的做法

  - We want to map a cuboid [l, r] × [b, t] × [f, n] to the “canonical (正则、规范、标准)” cube [-1, 1]$^3$

  <img src="GAMES101.assets/image-20200928050318704.png" alt="image-20200928050318704" style="zoom: 80%;" />

  ​	l, r, b, t, f, n 表示 left, right, bottom, top, far, near, 由于是右手系，far的z值反而会比near的z值小

  - 对比<u>简单的做法</u>，<u>通常的做法</u>需要先将cuboid的中心center与原点origin重合，然后缩放到一个 “canonical” cube

##### 计算

1. translate (center to origin)
2. scale (length/width/height to 2) 

Transfomation Matrix:
$$
M_{ortho}=
\begin{bmatrix} 
\frac{2}{r-l}&0&0&0\\
0&\frac{2}{t-b}&0&0\\
0&0&\frac{2}{n-f}&0\\
0&0&0&1\\
\end{bmatrix}
\begin{bmatrix} 
1&0&0&-\frac{r+l}{2}\\
0&1&0&-\frac{t+b}{2}\\
0&0&1&-\frac{n+f}{2}\\
0&0&0&1\\
\end{bmatrix}
$$

- 右边是平移矩阵：负的是因为要回到原点
- 左边是缩放矩阵：最后$r-l$这段长度会变成$(r-l) * \frac{2}{r-l}$这么长，也就是2，为-1到1的距离

#### Perspective Projection

> 透视投影(近大远小)

<img src="GAMES101.assets/image-20200928053352470.png" alt="image-20200928053352470" style="zoom:80%;" />

- 要用到的一些性质（齐次坐标）
  - (x, y, z, 1), (kx, ky, kz, k != 0), (xz, yz, z 2 , z != 0) all represent the same point (x, y, z) in 3D
    e.g. (1, 0, 0, 1) and (2, 0, 0, 2) both represent (1, 0, 0)
  - simple, but useful

<img src="GAMES101.assets/image-20200928053750144.png" alt="image-20200928053750144" style="zoom:80%;" />

- 投影步骤
  1. “squish” the frustum into a cuboid (n -> n, f -> f) ($M_{persp->ortho}$ ) 先将远平面挤到和近平面一样大
  2. Do orthographic projection (M ortho , already known!) 再正交投影

- 一些规定
  - 近平面啥都不变
  - 远平面的z不变，中心也不变

##### 计算

1. 首先将远平面缩成近平面的大小，所以先找远近平面的关系 

   <img src="GAMES101.assets/image-20200928054110480.png" alt="image-20200928054110480" style="zoom: 67%;" />

   这里面有两个相似三角形，比值是$\frac{n}{z}$

   $y'=\frac{n}{z}y$，$x'=\frac{n}{z}x$

   所以我们知道了缩放后远平面x，y的变化，远平面上的点的变化：
   $$
   \begin{pmatrix}
      x \\
      y \\
      z \\
      1
   \end{pmatrix} \implies
   \begin{pmatrix}
      nx/z \\
      ny/z \\
      unknow \\
      1
   \end{pmatrix} ==
   \begin{pmatrix}
      nx \\
      ny \\
      still\space unknow \\
      z
   \end{pmatrix}
   $$

   - $z$在这里还不知道是怎么变化。
   - 点的坐标都乘上一个数（比如$z$），点还是那个点。

2. 尝试推一下$M^{(4×4)}_{persp->ortho}$
   $\because M^{(4×4)}_{persp->ortho}   \begin{pmatrix}      x \\      y \\      z \\      1   \end{pmatrix} =   \begin{pmatrix}      nx \\      ny \\      unknow \\      z   \end{pmatrix}$
   
   $\therefore M_{persp->ortho} =    \begin{pmatrix}      n&0&0&0 \\      0&n&0&0 \\   	?&?&?&?\\      0&0&1&0   \end{pmatrix}$
   
   - 由于不知道z最后变成什么，也就无法逆推原来是什么乘z
   
3. 寻找更多的线索来确定$M_{persp->ortho} $第三行，比如

   1. **所有近平面的点位置都不变**，所以近平面的点做$M_{persp->ortho} $变化（缩放到和近平面一样大）得到的还是近平面。

      设近平面的点为$\begin{pmatrix}x \\   y \\   n\\   1\end{pmatrix}$，且 $M^{(4×4)}_{persp->ortho}   \begin{pmatrix}      x \\      y \\      z \\      1   \end{pmatrix} =   \begin{pmatrix}      nx \\      ny \\      unknow \\      z   \end{pmatrix}$

      

      由于近平面的点变化后不变，且格式是$\begin{pmatrix}      nx \\      ny \\      unknow \\ n \end{pmatrix}$ ，所以$unknow$应该是$n^2$，也就是说$M_{persp->ortho}\begin{pmatrix}      x \\      y \\      n\\      1   \end{pmatrix} = \begin{pmatrix}      nx \\      ny \\      n^2 \\      n   \end{pmatrix}$，逆推得$\begin{pmatrix}0&0&A&B\end{pmatrix} \begin{pmatrix}      x \\      y \\      n\\      1   \end{pmatrix} = n^2$，$M_{persp->ortho}$的第三行是$\begin{pmatrix}0&0&A&B\end{pmatrix}$，即$An+B=n^2$。

      由于有两个未知数A，B，我们需要更多线索

   2. **所有远平面的点z值都不变**，那我们不妨拿中心点$\begin{pmatrix} 0\\0\\f\\1 \end{pmatrix}== \begin{pmatrix} 0\\0\\f^2\\f \end{pmatrix}$来看看，$M_{persp->ortho}\begin{pmatrix} 0\\0\\f\\1 \end{pmatrix}=\begin{pmatrix} 0\\0\\f^2\\f \end{pmatrix}$，所以$\begin{pmatrix}0&0&A&B\end{pmatrix}\begin{pmatrix} 0\\0\\f\\1 \end{pmatrix} = f^2$，即$Af+B=f^2$

4. 整理一下已获得的线索

   $An+B=n^2\\Af+B=f^2$，得$A=n+f\\B=-nf$ 

5. Finally, every entry in $M_{persp->ortho}$ is known! $ M_{persp->ortho} =    \begin{pmatrix}      n&0&0&0 \\      0&n&0&0 \\   	0&0&n+f&-nf\\      0&0&1&0   \end{pmatrix}$

6. Do orthographic projection ($M_{ortho}$ ) to finish: $M_{persp} = M_{ortho} M_{persp->ortho}$ 

##### 问题

**如果一个平面位于远平面和近平面之间，做透视投影后，z的值会变吗？**

我的答案是会变得靠近远平面：

![IMG20200929215728](GAMES101.assets/IMG20200929215728-1601388138771.jpg)

##### 其他概念

![image-20201107103752753](GAMES101.assets/image-20201107103752753.png)

- field-of-view(fovY) 垂直可视角度。角度越小的话透视投影的结果会更像正交投影（大小差得比较小）；角度越大差得越大。

- aspect ratio 宽高比

  ![image-20201107104603224](GAMES101.assets/image-20201107104603224.png)

- $aspect = \frac{r}{t}$

- $tan\frac{fovY}{2} = \frac{t}{|n|}$

# Rasterization

> 光栅化
>
> MVP之后图像在[-1,1]$^3$的立方体中，光栅化就是把图像画到屏幕上
>
> raster == screen in German (屏幕也叫光栅成像设备)

实时图形学(>30fps)常用到光栅化

## Viewport Transform

> 视口变换

- irrelevant to z

- Transform in xy plane: [-1, 1]$^2$ to [0, width] x [0, height]

- Viewport transform matrix:

  $M_{viewport} = \begin{pmatrix}      \frac{width}{2}&0&0&\frac{width}{2} \\ 0&\frac{height}{2}&0&\frac{height}{2} \\ 0&0&1&0 \\      0&0&0&1   \end{pmatrix}$

  z方向不动，x，y缩放到屏幕大小，然后平移到原点处

## Triangle

> （fundamental shape primitive）

- 性质
  - most basic polygon，任何其他多边形都可以拆成三角形
  - Guaranteed to be planar：三角形内部一定是一个平面，折一个三角形的话就变成两个三角形了。
  - Well-defined interior：多边形有凹凸，三角形没有，可以通过向量的叉积来判断点在三角形内还是外
  - Well-defined method for interpolating values插值 at vertices over triangle (barycentric interpolation)：三角形内部的插值

### 是否在三角形内

![image-20201107134139649](GAMES101.assets/image-20201107134139649.png)

沿一个方向，比如顺时针，计算$\vec{P_1P_2}×\vec{P_2Q}$，$\vec{P_2P_0}×\vec{P_2Q}$，$\vec{P_0P_1}×\vec{P_0Q}$ 如果得出的三个结果都为正或者都为负，说明点在三角形内。

点刚好在边上可以不做严格处理。

### Bounding Box

> 包围盒

- 包围盒的水平范围是从x最小到x最大，垂直范围是从y最小到y最大，不在这个范围内的像素可以不光栅化。

## Sampling

> 采样
>
> Evaluating a function at a point is sampling.

We can discretize a function by sampling.

### 1D

```cpp
for (int x = 0; x < xmax; ++x)
	output[x] = f(x);
```

### 2D

$inside(t, x, y) = \begin{cases} 1 &\text{Point } (x,y) \text{ in triangle }t \\ c & otherwise\end{cases}$

```cpp
for (int x = 0; x < xmax; ++x)
	for (int y = 0; y < ymax; ++y)
		image[x][y] = inside(tri, x + 0.5, y + 0.5);  // 由像素点的中心点来决定这个像素在不在三角形内
```

## Artifact

> sampling artifact (error/mistakes/inaccuracies/瑕疵)

- Sampling Artifacts in Computer Graphics:
  - Jaggies, aliasing(staircase pattern 锯齿) —— sampling in space
  - Moiré Patterns(摩尔纹) —— undersampling images 隔行采样的结果
  - Wagon whheel effect(高速旋转的车轮看起来是倒转的，因为人眼的采样速度跟不上) —— sampling in time
  - . . . 
- Behind the Aliasing Artifacts: Signals are **changing too fast** (high frequency), but **sampled too slowly** 本质都是采样速度慢

## Antialiasing

> 反走样

![image-20201107140945848](GAMES101.assets/image-20201107140945848.png)

- Note antialiased edges in rasterized triangle
  where pixel values take intermediate values
- 顺序不能颠倒，必须先模糊再采样

### Frequency Domain 

- 傅里叶变换能把图片从时域（空间中不同的位置）变到频域

  <img src="GAMES101.assets/image-20201107150401029.png" alt="image-20201107150401029" style="zoom:50%;" />

  - 频率图中间是低频信号，四周是高频信号。自然界中的图片信息也是大部分都集中在低频区。

### Conovolution

> 卷积

- Filtering = Convolution ( = Averaging)？比如低通滤波过滤掉了高频信息，相当于平均了

#### Filter Kernel

![image-20201107153637570](GAMES101.assets/image-20201107153637570.png)

![image-20201107153653532](GAMES101.assets/image-20201107153653532.png)

卷积核如果变大，图片会变模糊（可以这么理解，考虑最极端情况，如果卷积核和图片一样大，那么得出的结果是所有的像素都是一样的颜色）



### Convolution Theorem

**Convolution in the spatial domain is <u>equal to multiplication in the frequency domain</u>, and vice versa** 时域的卷积等于频域的乘积，时域的乘积等于频域的卷积



例如以下两个操作得到的结果是一样的：

Option1:

1. Filter by convolution in the spatial domain 时域上的卷积

Option2:

1. Transform to frequency domain (Fourier transform) 先用傅里叶变换把图片从时域变到频域

2. Multiply by Fourier transform of convolution kernel 把卷积核也变到频域上，把两者相乘
3. Transform back to spatial domain (inverse Fourier) 用逆傅里叶变换从频域变到时域

![image-20201107153221614](GAMES101.assets/image-20201107153221614.png)

### 采样,走样,反走样

![image-20201107154255934](GAMES101.assets/image-20201107154255934.png)

- (c)为冲激函数，只在特定的位置有值
- (e)是(a)(c)相乘的结果
- (f)是(b)(d)做卷积的结果: 采样就是在重复原始信号的频谱, 当这些信号的频谱发生重叠时, 图像就走样了:

![image-20201107154742894](GAMES101.assets/image-20201107154742894.png)

- 采样不够快, 信号的频谱间隔会变小(时域和频域很多关系是相反的…)

(铺垫这么多终于到反走样了)

How Can We Reduce Aliasing Error?

Option 1: Increase sampling rate

- Essentially increasing the distance between replicas in the Fourier domain 用分辨率高的显示器, 分辨率高所以像素点小, 像素点小说明采样率高, 采样率高频谱重叠的就少
- Higher resolution displays, sensors, framebuffers…
- But: costly & may need very high resolution

Option 2: **Antialiasing**

- Making Fourier contents “narrower” before repeating
- i.e. Filtering out high frequencies before sampling

### 反走样

**Antialiasing = Limiting, then repeating**

![image-20201107155643538](GAMES101.assets/image-20201107155643538.png)

(先砍掉高频信号, 再采样)

1. Convolve f(x,y) by a 1-pixel box-blur

   (Recall: convolving = filtering = averaging)

   使用卷积来模糊, 下面是像素大小的卷积核

   ![image-20201107160707386](GAMES101.assets/image-20201107160707386.png)

2. Sample at every pixel’s center

   In rasterizing one triangle, the average value inside a pixel area of f(x,y) = inside(triangle,x,y) is equal to the area of the pixel covered by the triangle.

   ![image-20201107161323098](GAMES101.assets/image-20201107161323098.png)

   像素颜色的深度和被三角形覆盖的面积大小成正比, 就是把黑色平均到整个像素



#### MSAA

> Multisample anti-aliasing

- 不是通过提升分辨率来反走样, 增加采样点只是为了近似一个合理的三角形覆盖率, 最后像素的数量没变
- 计算量会增加

步骤还是先模糊再采样

1. 模糊

   Approximate the effect of the 1-pixel box filter by sampling multiple locations within a pixel and averaging their values 通过对一个像素内的多个位置进行采样并求其值的平均值，来近似1像素滤波器的效果:

   <img src="GAMES101.assets/image-20201107161714356.png" alt="image-20201107161714356" style="zoom:50%;" />

   1. Take NxN samples in each pixel.

      ![image-20201107162830323](GAMES101.assets/image-20201107162830323.png)

   2. Average the NxN samples “inside” each pixel.

      ![image-20201107162956071](GAMES101.assets/image-20201107162956071.png)

      ![image-20201107162944669](GAMES101.assets/image-20201107162944669.png)

      ![image-20201107162929344](GAMES101.assets/image-20201107162929344.png)

      This is the corresponding signal emitted by the display 显示器发出的相应信号

      ![image-20201107163009772](GAMES101.assets/image-20201107163009772.png)

2. 采样: 采样就很简单了, 现在每个像素只有一个颜色了

#### FXAA

> Fast Approximate AA

- 找到边界->换成没有锯齿的边界

#### TAA

> Temporal/tɛmˈp(ə)r(ə)l/ AA (重音不同, 和‘临时的’做区分)

- 复用上一帧的信息

#### DLSS

> Deep Learning Super Sampling

- Super resolution / super sampling
  - From low resolution to high resolution
  - Essentially still “not enough samples” problem

## Z-buffering

- Store current min.z-value **for each sample** (pixel) 每个像素点都记录一个最浅的深度, 

- Needs an additional buffer for depth values

  - frame buffer stores color values
  - depth buffer (z-buffer) stores depth

- IMPORTANT: For simplicity we suppose

  **z is always positive**
  (smaller z -> closer, larger z -> further)

### 实现

- Initialize depth buffer to $\infty$

- During rasterization:

  ```cpp
  for (each triangle T)
  	for (each sample (x,y,z) in T)
  		if (z < zbuffer[x,y]) // closest sample so far
  			framebuffer[x,y] = rgb; // update color
  			zbuffer[x,y] = z; // update depth
  		else
  			; // do nothing, this sample is occluded
  ```

![image-20201107193519149](GAMES101.assets/image-20201107193519149.png)

- 复杂度: O(n)

# Shading

![image-20201107194645615](GAMES101.assets/image-20201107194645615.png)

- 从上到下分别是 高光, 漫反射, 环境光照

![image-20201107194841473](GAMES101.assets/image-20201107194841473.png)

## Diffuse Reflection

### Blinn-Phong

Diffusely(Lambertian) Reflected Light:
$$
L_d=k_d(I/r^2)max(0,\vec{n}\cdot \vec{l})
$$

- $\vec{n}$: 平面的法向量, 单位向量

- $\vec{l}$: 光的入射方向, 单位向量

- $L_d$: diffusely reflected light

- $k_d$: diffuse coefficient(color) 反射系数, 如果是1说明全部反射; 如果是0说明全部吸收了

- $(I/r^2)$: **到达的能量** energy arrived at the shading point

  (球体表面积计算公式为S=4πr²) 能量跟距离成反比

  <img src="GAMES101.assets/image-20201107195329213.png" alt="image-20201107195329213" style="zoom: 33%;" />

- $\vec{n}\cdot \vec{l}$: **接收的能量** 与光线的直射的角度的关系, 如果结果是1, 说明是直射; 如果结果是0, 说明光线和平面平行, 没有光线照射; 如果结果是负的, 说明点光源在平面表面的另一边, 没有意义不考虑

<img src="GAMES101.assets/image-20201107195216631.png" alt="image-20201107195216631" style="zoom: 67%;" />

- 漫反射和观测角度 $\vec{v}$ 没有关系, 公式中也没有出现 $\vec{v}$

## Specular Hightlights

- Intensity depends on view direction
- Bright near mirror reflection direction

<img src="GAMES101.assets/image-20201108163741494.png" alt="image-20201108163741494" style="zoom: 67%;" />

- $\vec{R}$为可以看到高光的角度

### Blinn-Phong

<img src="GAMES101.assets/image-20201108165728527.png" alt="image-20201108165728527" style="zoom:67%;" />

半程向量
$$
\begin{aligned}
\vec{h} &= bisector(\vec{v},\vec{l})\\
	    &= \frac{\vec{v}+\vec{l}}{||\vec{v}+\vec{l}||}
\end{aligned}
$$
Specularly Reflected Light
$$
\begin{aligned}
	L_s &=k_s(I/r^2)max(0,cos\alpha)^p\\
		&=k_s(I/r^2)max(0,\vec{n}\cdot \vec{h})^p\\
\end{aligned}
$$

- $\vec{n}$: normal vector, 平面的法向量, 单位向量

- $\vec{h}$: half vector, $\vec{v}$和$\vec{l}$的中间向量, 单位向量

  $\vec{v}$ close to mirror direction ⇔ **half vector near normal**, Measure “near” by dot product of unit vectors, 通过半程向量和法向量是否接近来判断观看角度和高光角度是否接近

- $k_s$: 镜面反射系数

- 颜色, 通常高光是白的

- $\vec{n}\cdot \vec{h}$: 得两个向量夹角的$cos$值, 越接近1说明观看角度越接近高光角度

- $^p$: Increasing p narrows the reflection lobe 控制高光大小

  ![image-20201108172035193](GAMES101.assets/image-20201108172035193.png)

  $cos$ 的容忍范围太大, 即使差了45°, 数值上也差不了多少, 导致高光范围太大, 即使角度偏很多还是能看到高光, 实际情况应该是和只要偏离一点就看不到高光. 所以需要让它的变化更陡峭一些

  通常会取到100, 200

  ![image-20201108173238708](GAMES101.assets/image-20201108173238708.png)

- 没有考虑$\vec{n}\cdot \vec{l}$(接收的能量)……

## Ambient Lighting

- Shading that does not depend on anything
  - Add constant color to account for disregarded
    illumination and fill in black shadows

  - This is approximate / fake!

    

$$
L_a = k_aI_a
$$

- 公式中没有出现$\vec{l}$, 与直接光照方向无关; 也没有出现$\vec{v}$, 与观测方向也无关. 所以是一个常数
- $k_a$: 环境光系数
- $I_a$: 环境光的强度

## Blinn-Phong Reflection Model

![image-20201108174249515](GAMES101.assets/image-20201108174249515.png)
$$
\begin{aligned}
	L &= L_a + L_d + L_s\\
	  &= k_aI_a + 
	  	 k_d(I/r^2)max(0,\vec{n}\cdot \vec{l}) +  
	  	 k_s(I/r^2)max(0,\vec{n}\cdot \vec{h})^p
\end{aligned}
$$


# Curves & Meshes

> 几何

# Ray Tracing

> 光线追踪

# Animation

> Simulation 模拟





作业一、二：史雨宸，syc0412@mail.ustc.edu.cn
作业四、五：邓俊辰，1050106988[@qq](http://games-cn.org/forums/users/qq/).com
作业三、六、七：刘光哲，lgz17@mails.tsinghua.edu.cn
作业八：禹鹏、郭文鲜，y2505418927@gmail.com，wxguojlu@hotmail.com