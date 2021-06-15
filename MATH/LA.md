- 几何层面上的理解能让你知道要用什么工具, 以及为什么会有用, 以及结果为什么会这样; 数值层面上的理解能让你顺利使用这些工具
- 线性代数围绕两种基本运算: 向量加法（vector addition）和标量数乘（scalar multiplication） 

# 向量&矩阵

## 线性组合

> linear combination

<img src="LA.assets/image-20200902214451681.png" alt="image-20200902214451681" style="zoom:50%;" />

- 为什么叫线性呢？如果你固定其中一个标量，让另一个标量自由变化，这两个向量合起来指向的终点会描出一条直线；如果让两个标量同时自由变化，就能够得到所有可能的向量。
- 为什么要定义基向量呢？随便找两个向量不就能表达任何向量了吗？因为如果这两个向量刚好共线或者是零向量就不妙了。

<img src="LA.assets/image-20200902220704556.png" alt="image-20200902220704556" style="zoom:50%;" />

- 给定向量线性组合的向量集合称为给定向量张成的空间(span)
- 张成空间（span）：如果共线，span就是一条线
- span其实就是仅通过vector addition和scalar multiplication这两种基础运算能获得的所有向量集合

## 线性相关

> linearly dependent

如果有3个**随机的**向量，这么这3个向量的组合能包含3维空间内的所有向量。

如果一个向量可以表示为其他向量的线性组合，因为这个向量已经落在向量张成空间中，那么它们**线性相关**

<img src="LA.assets/image-20200902221918056.png" alt="image-20200902221918056" style="zoom:50%;" />

如果所有向量都给张成空间添加了新的维度，那么这些向量**线性无关**。

<img src="LA.assets/image-20200902221843556.png" alt="image-20200902221843556" style="zoom:50%;" />

## 线性变换

> linear transformation

线性变换需要具有以下两条性质：

1. all lines must remain lines, without getting curved. 保持坐标网格线平行且等距分布 (parallel and evenly spaced)
2. the origin must remain fixed in place. 原点保持不动

比如旋转坐标，剪切（Shear，就是将网格倾斜），拉伸或挤压坐标轴等

<img src="%E7%BA%BF%E4%BB%A3%E7%9A%84%E6%9C%AC%E8%B4%A8.assets/image-20200902223900857.png" alt="image-20200902223900857" style="zoom:50%;" /><img src="LA.assets/image-20200902223926593-1620800372173.png" alt="image-20200902223926593" style="zoom:50%;" />

- 需要满足那两个性质的原因是: 向量v是基向量i, j的特定线性组合, 变换后v也是i, j同样的线性组合. 已知变换前v和i, j的关系, 根据变换后的i, j就可以推断变换后的v

- 例子: i从(1,0)变到(1, -2); j从(0, 1)变到(3, 0). 二维线性变换仅由4个数字完全确定

  ![image-20210512144734140](LA.assets/image-20210512144734140.png)

<img src="LA.assets/image-20200902225439504-1620800372173.png" alt="image-20200902225439504" style="zoom: 50%;" />

- 把图中绿色部分看作是第一个基向量变化后的样子, 红色部分看作是第二个基向量变化后的样子. 
- 没有变换的情况, 也就是 $\begin{bmatrix} x \\ y \end{bmatrix}$ 表示在普通直角坐标系中（基向量是$\begin{bmatrix} 1 \\ 0 \end{bmatrix}$，$\begin{bmatrix} 0 \\ 1 \end{bmatrix}$）$x\cdot \begin{bmatrix} 1 \\ 0 \end{bmatrix} + y \cdot \begin{bmatrix} 0 \\ 1 \end{bmatrix}$ 后的向量

- 更多例子

  <img src="LA.assets/image-20200902230303816-1620800372173.png" alt="image-20200902230303816" style="zoom:50%;" />

  - $\begin{bmatrix} 1 \\ 0 \end{bmatrix}$是新坐标的一个基向量，$\begin{bmatrix} 1 \\ 1 \end{bmatrix}$ 是另一个基向量，$\begin{bmatrix} x \\ y \end{bmatrix}$ 要从原来的普通直角坐标转成这个新的坐标，就只要乘以$\begin{bmatrix} 1&1 \\ 0&1 \end{bmatrix}$就可以了。

  - $\begin{bmatrix} 1&0 \\ 0&1 \end{bmatrix}\begin{bmatrix} x \\ y \end{bmatrix} = \begin{bmatrix} x \\ y\end{bmatrix}$ 知道为什么结果是这样了吧？因为$\begin{bmatrix} 1&0 \\ 0&1 \end{bmatrix}$是普通的直角坐标系。
  - 矩阵（如$\begin{bmatrix} 1&1 \\ 0&1 \end{bmatrix}$ ）可以看作是对空间的一种特定变换（transformation of space），而由于新坐标的网格线具有平行且等距分布，原点不动的性质，要想得到向量$\begin{bmatrix} x \\ y \end{bmatrix}$变换后的结果，只要让$x，y$乘以变换后的新的基向量（如$\begin{bmatrix} 1&1 \\ 0&1 \end{bmatrix}$ ）

图中绿橙两个基向量是线性无关的，如果是线性相关，那就成一条直线了，如下面所示

<img src="LA.assets/image-20200902232742021-1620800372173.png" alt="image-20200902232742021" style="zoom:50%;" />

矩阵向量乘法就是计算**线性变换作用于给定向量**的一种途径。可以把矩阵解读为对空间的一种特定变换

### 复合变换

> 旋转和剪切（Shear）两种线性变换同时使用，就是“复合变换”

$\begin{bmatrix} x \\ y \end{bmatrix}$乘以一个旋转后的新坐标，再乘以一个剪切后的新坐标，效果等同于直接乘以一个已经旋转剪切过的新坐标。

<img src="LA.assets/image-20200903012422240-1620800372173.png" alt="image-20200903012422240" style="zoom:50%;" />

- 可以看出，两个矩阵相乘相当于对原坐标做了两次线性变换。建议每次计算矩阵乘法的时候可以想想这个。

- BTW：$\begin{bmatrix} 0&-1 \\ 1&0 \end{bmatrix}$ 是旋转矩阵，原来的两个基坐标是(1, 0) (0, 1) ，变成了(0, 1) (-1, 0)，画下图就知道旋转了90°

#### 性质

有了几何层面的理解, 有时候一些证明不需要矩阵的运算就能得证, 比如: 

1. **矩阵相乘的时候，顺序会影响结果**, 证明如下

   <img src="LA.assets/image-20200903081947903-1620800372173.png" alt="image-20200903081947903" style="zoom:50%;" /> <img src="%E7%BA%BF%E4%BB%A3%E7%9A%84%E6%9C%AC%E8%B4%A8.assets/image-20200903082001628.png" alt="image-20200903082001628" style="zoom:50%;" />

   将这两个动作叠加，顺序不同，结果不同

   <img src="LA.assets/image-20200903014250066-1620800372173.png" alt="image-20200903014250066" style="zoom: 33%;" /><img src="LA.assets/image-20200903014313792-1620800372174.png" alt="image-20200903014313792" style="zoom: 33%;" />

2. **(AB)C=A(BC)​ 证明矩阵乘法符合结合律**

   等式左边可以看作先执行$C$变换，再执行$AB$两个迭加变换；等式右边可以看作先执行C变换，再B变换，最后A变换。整个的顺序没有变，所以就应该相等。

### 三维空间

<img src="LA.assets/image-20200903085203576-1620800372174.png" alt="image-20200903085203576" style="zoom:50%;" />

这种3个基向量互相垂直的坐标可以用$\begin{bmatrix} 1&0&0 \\ 0&1&0\\0&0&1\end{bmatrix}$表示，3个基向量的坐标分别是(1,0,0)、(0,1,0)、(0,0,1)

一个例子

<img src="LA.assets/image-20200903085958863-1620800372174.png" alt="image-20200903085958863" style="zoom:50%;" />

绕y轴旋转90° (红色的保持不变)

<img src="LA.assets/image-20200903090115067-1620800372174.png" alt="image-20200903090115067" style="zoom:50%;" />

向量和矩阵的乘法和二维空间的同理

<img src="LA.assets/image-20200903093013153-1620800372174.png" alt="image-20200903093013153" style="zoom:50%;" />

矩阵和矩阵的乘法也和二维空间的类似

<img src="LA.assets/image-20200903093206590-1620800372174.png" alt="image-20200903093206590" style="zoom:50%;" />

相当于两次坐标变换的复合

## 逆矩阵

- 相当于逆变换
- 行列式为0时, 说明变换后空间被降维, 被压缩到更低的维度上, 就没有逆变换, 因为有的信息已经丢失, 无法将一条线“解压缩”成一个平面

## 列空间

> column space
>
> 矩阵的列向量张成的空间

- 零向量一定能会被包含在列空间中 (因为线性变换必须保持原点位置不变)

## 秩

> rank
>
> 代表变换后列空间的维数

- 2*2的矩阵, 秩最大是2; 3\*3的矩阵, 秩为2意味着空间被压缩了

### 满秩

> full rank
>
> 矩阵的秩和矩阵的列向量的个数相等

- 对于满秩变换来说, 唯一能在变换后落在原点的就是零向量自身; 对于非满秩变换来说 (把空间压缩到一个更低的维度上) , 可能会有一系列向量在变换后变成零向量

  <img src="LA.assets/image-20210603165044680.png" alt="image-20210603165044680" style="zoom:50%;" /><img src="LA.assets/image-20210603165134182.png" alt="image-20210603165134182" style="zoom:50%;" /><img src="LA.assets/image-20210603165156395.png" alt="image-20210603165156395" style="zoom:50%;" />

## 零空间

> null space / kernel 核
>
> 变换后落在原点(零向量)的向量的集合称为矩阵的“零空间”或“核”

- 零空间一定包含零向量, 因为不管是满秩变换还是很非满秩变换, 零向量始终在原点
  - 一个二维线性变换将空间压缩到一条直线上, 那么沿某个不同方向直线上的所有向量就被squished到原点(如上图)
  - 一个三维线性变换将空间压缩到一个平面上, 会有一整条线上的向量在变换后落在原点
  - 一个三维线性变换将空间压缩到一条线上, 会有一整个平面上的向量在变换后落在原点 [link](https://www.bilibili.com/video/BV1ys411472E?p=8)

- 解 $A \overrightarrow{x}=\overrightarrow{v}$ 的时候, 如果 $\overrightarrow{v}$ 是零向量, 零空间给出的就是这个向量方程所有可能的解

# 行列式

> <img src="LA.assets/image-20210510222524336.png" alt="image-20210510222524336" style="zoom: 67%;" />

- n阶行列式是n!项的代数和
- n阶行列式的每项都是位于不同行, 不同列n个元素的乘积
- $a_{1p_1}a_{2p_2}...a_{np_n}$的符号为$(-1)^t$. $t$是$p_1p_2...p_n$的[逆序数](https://baike.baidu.com/item/%E9%80%86%E5%BA%8F%E6%95%B0#:~:text=%E4%B8%80%E4%B8%AA%E6%8E%92%E5%88%97%E4%B8%AD%E9%80%86%E5%BA%8F%E7%9A%84,%E8%BF%99%E4%B8%AA%E6%8E%92%E5%88%97%E7%9A%84%E9%80%86%E5%BA%8F%E6%95%B0%E3%80%82)
  - eg. $a_{13}a_{21}a_{32}$中$t(312)=2$, 偶排列, 是正号
- n阶行列式可简记为$D_n$或$det(a_{ij})$

## 几何层面解释

### 二维空间

**行列式的绝对值能表示变换对空间拉伸或挤压了多少**

<img src="LA.assets/image-20200903110659837.png" alt="image-20200903110659837" style="zoom:50%;" />

一个1*1的矩形在坐标发生变换后($\begin{bmatrix} 3&0 \\ 0&2 \end{bmatrix}$, 表示x轴拉伸3倍，y轴拉伸2倍)，就变成了下面这样。

<img src="LA.assets/image-20200903110042030.png" alt="image-20200903110042030" style="zoom:50%;" />

这个矩形的面积被拉伸了6倍，行列式算出来就是6

<img src="LA.assets/image-20200907125022963.png" alt="image-20200907125022963" style="zoom:50%;" /><img src="%E7%BA%BF%E4%BB%A3%E7%9A%84%E6%9C%AC%E8%B4%A8.assets/image-20200907134005800.png" alt="image-20200907134005800" style="zoom:50%;" />

如果两个基坐标线性相关，那么这个平面就被压扁了, 行列式算出来就是0

<img src="%E7%BA%BF%E4%BB%A3%E7%9A%84%E6%9C%AC%E8%B4%A8.assets/image-20200907134205278.png" alt="image-20200907134205278" style="zoom:50%;" /><img src="LA.assets/image-20200907134239742.png" alt="image-20200907134239742" style="zoom:50%;" />

如果算出来是负的，那就要把坐标翻转，橙色向量跑到了绿色向量的右边

<img src="LA.assets/image-20200907134553903.png" alt="image-20200907134553903" style="zoom:50%;" />

#### 计算

<img src="LA.assets/image-20200907140840731.png" alt="image-20200907140840731" style="zoom:50%;" />

推导过程

<img src="LA.assets/image-20200907140923928.png" alt="image-20200907140923928" style="zoom: 67%;" />



### 三维空间

<img src="LA.assets/image-20200907134949593.png" alt="image-20200907134949593" style="zoom:50%;" />

被压扁的情况

<img src="LA.assets/image-20200907135159468.png" alt="image-20200907135159468" style="zoom:50%;" />

行列式是正的时候, 基向量构成右手定则的坐标系, 负的时候是左手定则

#### 计算

<img src="LA.assets/image-20200907141053816.png" alt="image-20200907141053816" style="zoom:50%;" />

### 性质

- $det(M_1M_2) = det(M_1)det(M_2)$: 根据行列式的含义顺理成章就得证

## 定理

- 定理1 一个排列中的任意两个元素对换,排列改变奇偶性
  - 推论: 奇排列变成标准排列的次数为奇数，偶排列变成标准排列的次数为偶数

<img src="LA.assets/image-20210512200710980.png" alt="image-20210512200710980" style="zoom: 67%;" />

## 性质

<img src="LA.assets/image-20210512131713616.png" alt="image-20210512131713616" style="zoom: 50%;" />

- 说明: 行列式中行与列具有同等的地位,因此行列式的性质凡是对行成立的对列也同样成立

- 推论: 如果行列式有两行（列）完全相同，则此行列式为零

  <img src="LA.assets/image-20210512200950929.png" alt="image-20210512200950929" style="zoom:67%;" />

<img src="LA.assets/image-20210512131734828.png" alt="image-20210512131734828" style="zoom: 50%;" />

<img src="LA.assets/image-20210512131812204.png" alt="image-20210512131812204" style="zoom: 50%;" />

<img src="LA.assets/image-20210512201044675.png" alt="image-20210512201044675" style="zoom: 50%;" />

<img src="LA.assets/image-20210512201411911.png" alt="image-20210512201411911" style="zoom: 50%;" />

<img src="LA.assets/image-20210512201635412.png" alt="image-20210512201635412" style="zoom:50%;" />

## 计算

<img src="LA.assets/image-20210512201725218.png" alt="image-20210512201725218" style="zoom:67%;" />

![image-20210512202017086](LA.assets/image-20210512202017086.png)

## 余子式

> ![image-20210512202318717](LA.assets/image-20210512202318717.png)

