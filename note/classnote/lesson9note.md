# 9w：异常检测和推荐系统  

这周继续无监督学习，似乎内容还是很多……

## 1. Anomaly Detection  

异常检测。

### 1.1 Density Estimation

#### 1.1.1 Problem Motivation  
8 分

异常检测。用于生产、欺诈等正样本极少、且正样本变化较大的情况。因正样本变化大，因此花大力气为正样本建立的模型可能到下一次就不适用了（又有新的问题产生了），所以用大量负样本建模型，即：刻好“正常”情况应该是个啥样，其他都是异常。  

其实就是统计学里的假设检验过程。假设都不是异常，那概率还很低的话，就推翻假设，所以异常。  

个人感觉：异常检测的表述过程，比假设检验过程容易懂很多。  

以上乱说，以下笔记：  

> 这种算法的一个有趣之处在于 它虽然主要用于 非监督学习问题 但从某些角度看 它又类似于一些监督学习问题   

> 就训练集建立了x的概率模型之后，对于新的飞机引擎，也就是x-test，如果概率p低于阈值ε，那么就将其标记为异常。如果x-test的概率p大于给定的阈值ε，我们就认为它是正常的。 

#### 1.1.2 Gaussian Distribution  
10 分

这一节纯粹是为高斯分布补课，与上下文无关。  

高斯分布，等于正态分布。由两个参数：平均值miu、方差sigma平方，来决定分布情况。  

以前学过，当平均值miu是0、标准差sigma是1时，称之为标准正态分布。  

平均值决定了曲线在x轴方向上的移动情况；  
sigma决定了曲线的**密度**情况。  

特别强调，是**密度**，而不是宽窄。为什么呢？因为整个曲线与X轴之间的面积是不变的，sigma小，就压缩得又高又瘦；sigma大，就拉伸得又矮又胖。（有没有瘦头陀和胖头陀的即时感？）  

为什么整个面积不变？其实就是总概率1。这一点以前一直没想明白，这次看着一堆x点，突然就明白了。  

> 就是这个图，一堆x点：  
> ![](http://7xotr7.com1.z0.glb.clouddn.com/16-5-12/84621680.jpg)

---  
##### 脑洞大开的理解  
整个X样本，x轴就是X样本中的各个具体的值，不管是出现在中间（接近平均值）还是边上，它都是大样本中的一分子。  

分布指代的问题就是：有多大的可能性取这个值而不是另一个值，所有可能性加在一起是什么？加在一起就是总概率，肯定是1（100%）。  

高度y，我可以理解为太密集了，于是x轴堆不下了，就被“挤”到另一个维度上了，形成了面积。  
数轴概念不能造成这样的情况，只有抽屉、盒子才能造成这样的情况。所有可以把x轴看成是一个又一个小盒子，里面装着各自指定范围内的x数值，装不下了就溢出到y轴，形成面积。最后这幅图看上去就是钟形曲线——高斯分布曲线。嗯，还是瘦头陀和胖头陀。   

---

以上乱说，以下笔记： 

> ![](http://7xotr7.com1.z0.glb.clouddn.com/16-5-12/54944849.jpg)  
> 这个钟形曲线是有公式的！！！

对μ和σ平方进行参数估计的标准公式：  

> μ公式：  
> ![](http://7xotr7.com1.z0.glb.clouddn.com/16-5-12/7951008.jpg)   
> σ平方公式：  
> ![](http://7xotr7.com1.z0.glb.clouddn.com/16-5-12/52665481.jpg)   
> 或者这个：  
> ![](http://7xotr7.com1.z0.glb.clouddn.com/16-5-12/84846007.jpg)  

用m还是m-1，只是个习惯问题。数学差异在应用时不太体现。  

> 在实际使用中 到底是选择使用 m分之1还是m减1分之1 其实区别很小 只要你有一个还算大的训练集 因此 如果你见过m减1分之1 这个版本的公式 它同样可以很好的估计出参数 只是在机器学习领域 大部分人更习惯使用 m分之1这个版本的公式。  
> 这两个版本的公式 在理论特性和数学特性上稍有不同 但是在实际使用中  他们的区别甚小 几乎可以忽略不计 

#### 1.1.3 Algorithm  
12 分

主要问题：应用高斯分布开发异常检测算法   

首先要从数据中建立一个p(x)概率模型：  

> 估计 p(x) 的分布问题 这种问题通常被称为密度估计问题

> ![](http://7xotr7.com1.z0.glb.clouddn.com/16-5-12/37693907.jpg)  

异常检测算法 ：

>![](http://7xotr7.com1.z0.glb.clouddn.com/16-5-12/17026354.jpg)  

举例：  
> ![](http://7xotr7.com1.z0.glb.clouddn.com/16-5-12/21364435.jpg)

### 1.2 Building an Anomaly Detection System

#### 1.2.1 Developing and Evaluating an Anomaly Detection System  
13 分

主要问题：如何开发一个关于异常检测的应用来解决一个实际问题，重点关注如何评价一个异常检测算法。  

> 为了做到这一点 为了能评价一个 异常检测系统 我们先假定已有了一些带标签的数据 所以 我们要考虑的 异常检测问题 是一个非监督问题 使用的是无标签数据 但如果你有一些 带标签的数据 能够指明哪些是异常样本 哪些是非异常样本 那么这就是我们要找的 能够评价异常检测算法的标准方法

> ![](http://7xotr7.com1.z0.glb.clouddn.com/16-5-12/55115110.jpg)

#### 1.2.2 Anomaly Detection vs. Supervised Learning  
8 分


#### 1.2.3 Choosing What Features to Use  
12 分

### 1.3 Multivariate Gaussian Distribution (Optional)

#### 1.3.1 Multivariate Gaussian Distribution  
14 分


#### 1.3.2 Anomaly Detection using the Multivariate Gaussian Distribution  
14 分 
 

## 2. Recommender Systems

### 2.1 Predicting Movie Ratings

#### 2.1.1 Problem Formulation  
8 分


#### 2.1.2 Content Based Recommendations  
15 分


### 2.2 Collaborative Filtering

#### 2.2.1 Collaborative Filtering  
10 分


#### 2.2.2 Collaborative Filtering Algorithm  
8 分


### 2.3 Low Rank Matrix Factorization

#### 2.3.1 Vectorization: Low Rank Matrix Factorization  
8 分


#### 2.3.2 Implementational Detail: Mean Normalization  
9 分

