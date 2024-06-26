---
title: 2024-06-19-Convolutional Neural Network
date: 2024-06-19
date modified: 2024-06-22
categories: DeepLearning
---

## Motivation

> [!Important] 为什么采用 CNN
> - 计算开销
>
>> 传统的全连接层架构在处理维数非常高的参数数据时所带来的参数开销几乎无法接受，训练效率与成本无法接受
> - 特征捕获能力
>>
>> 全连接层架构将所有的输入都展平，丧失了样本数据原有的空间特征

我们希望有操作能够同时满足以下性质:

- 平移不变性： 图形的特征并不因平移而改变
- 局部性：神经网络前几层仅探索局部性质  
我们将 $[H]_{ij}$ 记为隐藏层的输出， 其对应的输入为 $[X]_{ij}$(图像在位置 (i,j) 所对应的像素)

$$
[H]_{ij} = [U]_{ij} + \sum_{k}\sum_{j}[W]_{i,j,k,l}[X]_{k,l} = [U]_{ij} + \sum_{a}\sum_{b}[V]_{i,j,a,b}[X]_{i+a,j+b}
$$

交换求和顺序，将权重的索引下标定义为与 (i,j) 相关  
我们再满足其局部性,通过限制 a,b 的下标浮动,同时为了支持输入与输出中的多个通道，我们添加第四个坐标

$$
[H]_{i,j,d} = u + \sum_{a=-\Delta}^{\Delta}\sum _{b=-\Delta}^{\Delta}\sum_{c}[V]_{a,b,c,d}[X]_{i+a,j+b,c}
$$

其中 H 中的索引 d 表示输出通道，而随后的输出继续进入下一个卷积层，然后