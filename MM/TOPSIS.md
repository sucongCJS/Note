# 优劣解距离法

1. 将原始数据矩阵统一指标类型(一般正向化处理), 得到正向化的矩阵, 
2. 对正向化的矩阵进行标准化处理以消除各指标量纲的影响
3. 找到有限方案中的最有方案和最劣方案
4. 分别计算各评价对象与最优方案和最劣方案间的距离, 获得各评价对象与最优方案的相对接近程度, 以此作为评价优劣的依据

# 核心思想

$$
\frac{z与最小值的距离}{z与最大值的距离 + z与最小值的距离}
$$

当z等于最小值的时候, 得分为0, 为最小

当z等于最大值的时候, 得分为1, 为最大



# 步骤

极大型指标: 越大越好

极小型指标: 越小越好

## 指标正向化

### 

把所有的指标转化为极大型

极小型->极大型: 最大的去减每个     

### 中间型指标->极大型指标

某个中间值最好(如pH = 7最好)

### 区间型指标->极大型指标

某个区间最好

## 指标标准化