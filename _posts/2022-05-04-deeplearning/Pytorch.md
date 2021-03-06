---
layout: post
title: deeplearning
mathjax: true
categories: code
tags: deeplearning
keywords: deeplearning
description: Record deeplearning knowledge points
mermaid: true
highlight: true
status: Archived
type: mdpdf
repopath: 2022-05-04-deeplearning-cn
---

#### 计算图

不论是动态图还是静态图，它们都属于**计算图**。计算图是用来**描述运算的有向无环图**，它有两个主要元素:结点(Node)和边(Edge)。**结点表示数据**，如向量、矩阵、张量，而**边表示运算**，如加减乘除卷积等。

采用计算图来描述运算的好处不仅是让运算流的表达更加简洁清晰，还有一个更重要的原因是**方便求导计算梯度**。



#### 动态图

动态图意味着**计算图的构建和计算同时发生**(define by run)。这种机制由于能够实时得到中间结果的值，使得**调试更加容易**，同时我们将大脑中的想法转化为代码方案也变得更加容易，**对于编程实现来说更友好**。Pytorch使用的就是动态图机制，因此它更易上手，风格更加pythonic，大受科研人员的喜爱。



#### 静态图

静态图则意味着**计算图的构建和实际计算是分开**(define and run)的。在静态图中，会事先了解和定义好整个运算流，这样之后再次运行的时候就不再需要重新构建计算图了(可理解为编译)，因此速度会比动态图更快，从**性能上来说更加高效**，但这也意味着你所期望的程序与编译器实际执行之间存在着更多的代沟，代码中的错误将难以发现，无法像动态图一样随时拿到中间计算结果。Tensorflow默认使用的是静态图机制，这也是其名称的由来，先定义好整个计算流(flow)，然后再对数据(tensor)进行计算。



**torch.nn.Parameter**是继承自torch.Tensor的子类，其主要作用是作为nn.Module中的可训练参数使用。

这个函数理解为类型转换函数，将一个不可训练的类型 Tensor 转换成可以训练的类型 parameter 并将这个 parameter 绑定到这个module 里面(net.parameter() 中就有这个绑定的 parameter，所以在参数优化的时候可以进行优化)，所以经过类型转换这个变量就变成了模型的一部分，成为了模型中根据训练可以改动的参数。使用这个函数的目的也是想让某些变量在学习的过程中不断的修改其值以达到最优化。



 **super(Model, self).init()：**其代表对继承的那个父类的属性进行初始化

**nn.Linear（）**是用于设置网络中的全连接层的，需要注意的是全连接层的输入与输出都是二维张量，一般形状为[batch_size, size]，不同于卷积层要求输入输出是四维张量。

#### pytorch.range() 和 pytorch.arange() 的区别

1. `torch.range(start=1, end=6)` 的结果是会包含`end`的，
   而`torch.arange(start=1, end=6)`的结果并不包含`end`。
2. 两者创建的`tensor`的类型也不一样

`torchvision.transforms`主要是用于常见的一些图形变换。

`torchvision.transforms.Compose()`类。这个类的主要作用是串联多个图片变换的操作。

1. transform.ToTensor(),
2. transform.Normalize((0.5,0.5,0.5),(0.5,0.5,0.5))

ToTensor()能够把灰度范围从0-255变换到0-1之间，而后面的transform.Normalize()则把0-1变换到(-1,1).

![Image](https://github.com/cscdxu/cscdxu.github.io/blob/master/_posts/2022-05-04-deeplearning/image-20210708195347209.png)

np.linspace主要用来创建等差数列
