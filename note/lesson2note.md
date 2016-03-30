# 线性模型  

## 1. feature scaling  

feature scaling 没理解，查阅，发现这里[浅谈Feature Scaling_迎客松_新浪博客](http://blog.sina.com.cn/s/blog_7f2889330101awle.html)，正好是看的ng老师的课记录的笔记：   

> 简单来说，它主要用来把所有特征值范围映射至同样的范围里面如（0,1）、（-1,1）、（-0.5,0.5）等。  
 
> Feature scaling (数据规范化) 是数据挖掘或机器学习常用到的步骤，这个步骤有时对算法的效率和准确率都会产生巨大的影响。
 
> 对精度的影响：很明显，这个步骤的必要性要依赖于数据特征的特性，如果有>=2特征，并且不同特征间的值变化范围差异大，那就很有必要使用Feature scaling。比如说，在信用卡欺诈检测中，如果我们只使用用户的收入作为学习特征，那就没有必要做这个步骤。但是如果我们同时使用用户的收入和用户年龄两个特征的话，在建模之前采用这个步骤就很有可能能提高检测精度，这是因为用户收入这个特征的取值范围可能为[50000,60000]甚至更大，但用户年龄只可能是[20,100]左右，这时候，假如说我用K最近邻的方法去做检测的话，用户收入这个特征的相似度对检测结果的影响将会大大大于用户年龄的作用，然而事实上，这两个特征对欺诈检测可能有着同等的重要性。因此，假如我们在检测实施前，对着两个特征进行规范化，那我们的检测方法中就能真正地同等对待它们。 


![](http://7xotr7.com1.z0.glb.clouddn.com/16-3-30/4837295.jpg)  

这个例子，现在明白了，说的是让长长的椭圆变成接近正圆的样子，也就是让两个变量差不多同尺度，scaling这个词还是比较准确的。  

博客作者是这样说的：  

> 例子如上图，在该例子中，我们想用线性回归根据房屋的大小和房屋的卧室数量来预测房价，采用的优化方法为batch gradient descent。在建立模型的过程中，如果不对房屋的大小和房屋的卧室数量两个特征规范化，我们的优化问题将会在很skewed的区域中进行（如左图所示），这样会使得batch gradient descent的收敛很慢。而当我们对其进行规范化之后，问题就会转变为偏圆形的空间中优化，这时候，batch gradient descent的收敛速度将会得到大幅度提高。  

> 常用的Feature scaling方法有如下几种：   

> 	xi' = (xi - a) / b；
> 其中a可以为特征xi的均值，b则可以为xi的最大值、（最大值 - 最小值）、 标准差等。  

> 该步骤的原理和方法都是很简单的，但是如果数据挖掘或机器学习中少了这一步，有时候会对学习效率和准确度产生巨大影响，因此，在学习建模之前，要认真考虑是否进行Feature scaling。  

ng这个例子中的方法是用这个变量除以它的最大值max。  

在后面的例子中：  

![](http://7xotr7.com1.z0.glb.clouddn.com/16-3-30/7528656.jpg) 

是减去均值除以max。

[Feature scaling - Wikipedia, the free encyclopedia](https://en.wikipedia.org/wiki/Feature_scaling)  

[Gradient Descent in Practice I - Feature Scaling - 斯坦福大学 | Coursera](https://www.coursera.org/learn/machine-learning/lecture/xx3Da/gradient-descent-in-practice-i-feature-scaling)


## 2. learning rate  

梯度下降中两个要点：  

1. 判断梯度下降是否能正常工作？（正常下降）  
2. 如何确定learning rate 这个alpha值  

知道为什么alpha太大会上升了，因为alpha大了，跨度大，跨过了最低点，直接在最低点两端跨来跨去，越跨越远。  

![](http://7xotr7.com1.z0.glb.clouddn.com/16-3-30/90993593.jpg)  

另外，相比较自动收敛测试（即设置一个阈值epslon）来说，ng老师说他更喜欢J（theta）下降曲线。原因一是阈值较难确定到合适的，二是曲线可以呈现出alpha太大的毛病（上升），可以修正alpha。  

## 3. 多元回归  

用多元回归来模拟一元高次回归，特别一定需要feature scaling，因为值和值之间的差异实在太大了！！！  

![](http://7xotr7.com1.z0.glb.clouddn.com/16-3-30/8377182.jpg)  

这个公式会自动算出最优theta，即让J(theta)最小的theta值，而且不需要使用feature scaling。  

梯度下降法和正规方程方法比较：  

![](http://7xotr7.com1.z0.glb.clouddn.com/16-3-30/36426259.jpg)  

注意，当n上到10000时，可以考虑用梯度下降法了。  

## 4. 正规方程不可逆问题  

首先，存在不可逆，但很少见。   

其次，在octave中，pinv和inv都是用来求矩阵的逆的。pinv其实是伪逆。用pinv计算一个不可逆矩阵，它也能得到解，照样有一个theta被计算出来，神奇吧？
 
哪些原因会造成不可逆呢？一是特征冗余，二是特征太多：  

![](http://7xotr7.com1.z0.glb.clouddn.com/16-3-30/68047484.jpg)    

特征太多的情况要通过一些手段去掉一些特征。  

结论就是，这个问题无需多关注。
