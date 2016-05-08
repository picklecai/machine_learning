# 7w：Support Vectors Machines （支持向量机）  

## Part Ⅰ：Large Margin Classification

### 1. Optimization Objective  
15 分  

![](http://7xotr7.com1.z0.glb.clouddn.com/16-5-6/44955823.jpg)  

![](http://7xotr7.com1.z0.glb.clouddn.com/16-5-6/8268149.jpg)


### 2. Large Margin Intuition  
11 分

![](http://7xotr7.com1.z0.glb.clouddn.com/16-5-6/73591307.jpg)  

![](http://7xotr7.com1.z0.glb.clouddn.com/16-5-6/81078310.jpg)  

![](http://7xotr7.com1.z0.glb.clouddn.com/16-5-6/61425773.jpg)  

underfitting时，需要C变大，即lambda变小，少惩罚，才能更接近拟合状态。

### 3. Mathematics Behind Large Margin Classification  
20 分

![](http://7xotr7.com1.z0.glb.clouddn.com/16-5-6/85244952.jpg)  

![](http://7xotr7.com1.z0.glb.clouddn.com/16-5-6/22472253.jpg)  

这里为什么theta和分类线垂直，不太懂。  

![](http://7xotr7.com1.z0.glb.clouddn.com/16-5-6/91427597.jpg)  

这道题，做几次都错。  

最好的分类线就是x1 = 0，所以theta就是x2 = 0 

这样，比如（2，1）这个点，x在theta上的投影是2，即：p= 2 。 这个点的y是正值，1。  

所以：

	p*||theta||  = 1  
theta的范就是1/p = 1/2

## Part Ⅱ：Kernels

### 4. Kernels I  
16 分  

![](http://7xotr7.com1.z0.glb.clouddn.com/16-5-6/44978884.jpg)

这是高斯核函数。个人理解，就好像以这个点为核，看其他点离它远近。近即同类，远即不同类。多下几个这样的核，圈子就做好了。

![](http://7xotr7.com1.z0.glb.clouddn.com/16-5-6/75058817.jpg)  

![](http://7xotr7.com1.z0.glb.clouddn.com/16-5-6/17808461.jpg)  

当sigma变化时，等高线的变化。

![](http://7xotr7.com1.z0.glb.clouddn.com/16-5-6/91277077.jpg)  
theta值已知时，计算预测值。

### 5. Kernels II  
16 分  

如何选择标记点：

> 因此 在实际应用时 怎么选取标记点 是机器学习中必须解决的问题 这是我们的数据集 有一些正样本和一些负样本 我们的想法是 我们将选取样本点 我们拥有的 每一个样本点 我们只需要直接使用它们 我们直接 将训练样本 作为标记点 

![](http://7xotr7.com1.z0.glb.clouddn.com/16-5-6/57032117.jpg)

核函数为什么不能用于其他算法：  

> 顺便说一下 你可能会想为什么我们不将 核函数这个想法 应用到其他算法 比如逻辑回归上 事实证明 如果愿意的话 确实可以将核函数 这个想法用于定义特征向量 将标记点之类的技术用于逻辑回归算法 但是用于支持向量机 的计算技巧 不能较好的推广到其他算法诸如逻辑回归上 所以 将核函数用于 逻辑回归时 会变得非常的慢 相比之下 这些计算技巧 比如具体化技术 对这些细节的修改 以及支持向量软件的实现细节 使得支持向量机 可以和核函数相得益彰 而逻辑回归和核函数 则运行得十分缓慢 更何况它们还不能 使用那些高级优化技巧 因为这些技巧 是人们专门为 使用核函数的支持向量机开发的


## Part Ⅲ：SVMs in Practice

### 6. Using An SVM  
21 分  

关于sigma的大小选择：  

> 如果 σ 的平方很大 那么你就有可能 得到一个较大的误差 较低方差的分类器 但是如果 σ 的平方很小 那么你就会有较大的方差 较低误差的分类器 

- sigma大，bias大，方差小；  
- sigma小，bias小，方差大；  

终于在这里找到这个知识点了……  

题目在这里：  

![](http://7xotr7.com1.z0.glb.clouddn.com/16-5-6/69524847.jpg) 

应该选C变大，sigma变小。  

![](http://7xotr7.com1.z0.glb.clouddn.com/16-5-6/44297293.jpg)  

上面是什么时候选用什么核函数。  

默塞尔定理：  
![](http://7xotr7.com1.z0.glb.clouddn.com/16-5-6/27220552.jpg)  

一对多时svm的数量：  

![](http://7xotr7.com1.z0.glb.clouddn.com/16-5-6/12406528.jpg)

比较全面的选择什么核函数：  

![](http://7xotr7.com1.z0.glb.clouddn.com/16-5-6/42081302.jpg)   

使用神经网络的问题：  
![](http://7xotr7.com1.z0.glb.clouddn.com/16-5-6/73502821.jpg)

这道题做了几次都是错的：  

![](http://7xotr7.com1.z0.glb.clouddn.com/16-5-6/45127551.jpg)    

主要错误点在最后一项。我把它理解成局部最低点问题了。

