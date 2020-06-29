## parallel data processing

同时运行

## distributed processing

可以不同时运行

## Task Parallelism

A task is split into two sub-tasks, Sub-task A and Sub-task B, which are then run on two **different nodes** on the **same dataset**.

## Data Parallelism

A dataset is divided into two sub-datasets, Sub-dataset A and Sub-dataset B, which are then processed on two different nodes **using the same function**.

## OLTP

> on-line transaction processing

pos机

write-intensive

## OLAP

离线处理

processing in batch mode

## process workloads

### batch

## MapReduce

With MapReduce, the data processing algorithm is instead moved to the nodes that store the data. 借助MapReduce，数据处理算法改为移至存储数据的节点

不对数据进行处理

解决容量(volume) 种类(variety) 问题

### Map tasks

- map![1571888806924](big_data_fundamentals.assets\1571888806924.png)

  预处理

- combine (optional): ![1571888827314](big_data_fundamentals.assets\1571888827314.png)
  - summarizes a mapper’s output before it gets processed by the reducer
  - For example, a combiner function will work for finding the largest or the smallest number, but will not work for finding the average of all numbers since it only works with a subset of the data. 
  
- partition: ![1571888846780](D:\Note\BD\big_data_fundamentals.assets\1571888846780.png)

### Reduce tasks

- shuffle and sort
- reduce

![1571838120855](big_data_fundamentals.assets\1571838120855.png)

# 5V

## 容量

DFS

MapReduce

nosql: scale out 

## 速度

> 大数据产生的速度, 大数据处理的速度

MapReduce: 取得更快, 处理得更快

nosql: using schema-on-read 读写分开(课本196)

## 多样性

- 数据本身类型

NoSql: semi structure、

Hadoop, MapReduce

- 数据处理结果的呈现多样性

结构化, 半结构化, 非结构化数据?

## 质量

和数据本身的性质密切相关, 无法改变, 只能

## 价值

和数据本身的性质密切相关, 无法改变, 只能让价值更容易被呈现

# 数据存储

## ACID

适用于关系型数据库

atomicity

consistency

isolation

durability



## CAP

consistency

## BASE

适用于noSQL



## Column Family 

列簇

## Graph

同层结点没有关系

# NewSQL

NewSQL = ACID + NoSQL -> OLTP