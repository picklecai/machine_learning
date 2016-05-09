# 8w  无监督学习和降维

看了目录，这周内容不是一般地多……

## 1. Unsupervised Learning

### 1.1 Clustering

#### 1.1.1 Unsupervised Learning: Introduction  
3 分

看ng老师雀跃的表情和“保证精彩”……  

举例：  
无监督学习和监督学习的区别？  
没有y  

聚类这种无监督学习是怎样的效果？  
自动“聚”成不同类

![](http://7xotr7.com1.z0.glb.clouddn.com/16-5-9/94342434.jpg)

#### 1.1.2 K-Means Algorithm  
13 分

主要问题：什么是**K-means算法**以及它是怎么运作的  

> 首先随机选择两（就是K，将要聚的类别数）个点，作为聚类中心 (cluster centroids)   
> K均值是一个迭代方法 它要做两件事情：第一个是簇分配，第二个是移动聚类中心。  
> 
> - 簇分配：遍历所有的样本，依据每一个点是更接近哪个中心将它分配到两个不同的聚类中心中；   
> - 移动聚类中心：将两个聚类中心，移动到和它一样颜色的那堆点的**均值**处。  
> 
> 循环以上簇分配和移动聚类中心的过程，直到点的簇不变，聚类中心不再移动为止。 

以上说K均值如何工作。  
 
以下说K均值的输入：  

> K均值算法接受两个输入：第一个是参数K，表示你想从数据中聚类出的簇的个数；另外一个输入是只有x没有标签y的训练集。  
> 
> 这里注意：在非监督学习的K均值算法里，我们约定 x(i) 是一个n维向量。这就是训练样本是 n 维而不是 n+1 维的原因。  

**训练集没有常数项。**  

异常情况（其实是实际中更普遍的情况）：  

>  原本看起来并没有三个分开的簇。但是从某种程度上讲，K均值仍然能将数据分成几个类。 

![](http://7xotr7.com1.z0.glb.clouddn.com/16-5-9/79248835.jpg)

#### 1.1.3 Optimization Objective  
7 分

主要问题：K均值的优化目标函数（或者需要最小化的代价函数是什么？   

> 解决这个问题有两个好处：一是保证K均值正确运行，二是找到更好的簇，避免局部最优解。  

符号表示：  

> ![](http://7xotr7.com1.z0.glb.clouddn.com/16-5-9/49256823.jpg)    
> c表示序号，miu表示聚类中心。所以miu(c(i))表示的是xi所在的簇的聚类中心。  
> 
> K均值中，我们用大写K来表示簇的总数，用小写k来表示聚类中心的序号。因此，小写k的范围，就应该是1到大写K之间。 

最优化函数：  

> ![](http://7xotr7.com1.z0.glb.clouddn.com/16-5-9/56985366.jpg)   
> 
> 那么 K均值算法 要做的事情就是 它将找到参数 c(i) 和 μi 也就是说 找到能够最小化 代价函数 J 的 c 和 μ 这个代价函数 在K均值算法中 有时候也叫做 失真代价函数(distortion cost function)

点离聚类中心的距离的平方和。  

![](http://7xotr7.com1.z0.glb.clouddn.com/16-5-9/54093315.jpg)  

因为最近，所以代价最低。

#### 1.1.4 Random Initialization  
8 分


#### 1.1.5 Choosing the Number of Clusters  
8 分


## 2. Dimensionality Reduction

### 2.1 Motivation

#### 2.1.1 Motivation I: Data Compression  
10 分


#### 2.1.2 Motivation II: Visualization  
5 分


### 2.2 Principal Component Analysis

#### 2.2.1 Principal Component Analysis Problem Formulation  
9 分


#### 2.2.2 Principal Component Analysis Algorithm  
15 分

### 2.3 Applying PCA

#### 2.3.1 Reconstruction from Compressed Representation  
4 分


#### 2.3.2 Choosing the Number of Principal Components  
11 分


#### 2.3.3 Advice for Applying PCA  
13 分

