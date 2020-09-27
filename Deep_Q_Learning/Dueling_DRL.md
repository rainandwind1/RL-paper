# Dueling Network Architectures for Deep Reinforcement Learning 2016

## Abstract

​	近些年来深度强化学习中使用的网络有卷积神经网络，LSTM、自动编码机等，这篇文章在无模型的强化学习设定中提出了一个新的神经网络架构，竞争网络架构代表着两个分开的逼近器，一个是状态值函数，另一个是独立状态动作优势值函数，这种设定的主要优势在于在当前的强化学习算法的基础上不做大的改变就能提高学习的泛化性能。并且实验的结果显示了这种架构在多个相似值的动作情况下能够优化策略评估，并且在雅达利2600游戏上取得了当前最好的效果。

## Introduction

​	最近在强化学习领域的工作大多是研究新的算法或是将不同的神经网络或是逼近器融入算法中，我们的工作则是补充和替代性的，聚焦提出一种适合无模型强化学习的神经网络架构，这种架构很容易应用到当前已有的算法中，也就是说这篇文章提出的是一种新的适用型的网络，所应用的算法还是已有的算法。

​	提出的架构名称为竞争网络架构，显示的将状态值的表示和（状态独立）动作优势值分开，竞争架构由两个数据流组成，分别是值和优势函数，共享一个卷积网络特征学习模块，两个数据流通过一个特殊的聚合层组合产生最终的状态值函数Q。

​	竞争网络无监督的自动产生分开的状态值和优势值的估计值。

​	直观的来看，竞争架构能够学习出哪一个状态是有价值的哪一个状态是没有价值的，而不用对每个状态的每个动作都花费精力学习一遍，这种设置在动作不影响状态的情况下非常有用，竞争网络架构能够快速去除冗余信息的影响，

### Related Work

​	贝尔曼残差更新被分解成两个部分，一个是状态值函数，另一个是相应的优势值函数，优势值函数的更新比Q学习的更新收敛要快。

![image-20200429175042734](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20200429175042734.png)

## Background

![image-20200429190444473](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20200429190444473.png)

​	advantage函数将状态值从Q函数中减去，从而得到每个动作重要性的相对度量。1.DQN 2.DDQN 3.Prioritized Replay

## The Dueling Network Architecture

​	对于自举的算法来说，每一个状态的状态值估计都是很重要的，在DQN中卷积神经网络之后紧跟的是全连接层，竞争网络架构中紧跟的是两个数据流，分别输出的是状态值函数和优势值函数的数值，最后再由两个数据流组合而成为Q值输出，至于如何组合输出这两个模块需要精心的设计。

​	![image-20200429223643305](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20200429223643305.png)

![image-20200429223816782](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20200429223816782.png)

![image-20200429223844709](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20200429223844709.png)

等式7下我们无法判别，因为给定Q, V和A不是唯一的，当等式7直接使用时，这种非唯一性就能表现出来，于是找改进的方法，

![image-20200429224915204](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20200429224915204.png)

![image-20200429225412363](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20200429225412363.png)



## Experiments

Policy Evaluation

在动作空间很大的设定中，竞争式网络架构比普通的单流架构收敛的更快。

## General Atari Game-Playing



## Discussion

​		竞争式架构的优势部分在于他学习状态值函数的能力，竞争式架构中每更新一次Q值，V值也随之更新，但是在一般的单流输出的网络中，只有当值函数的一个动作更新时，相应的动作值函数才会更新，而这个状态的其他动作值则保持不变，因此这种竞争式的架构给状态值分配了更多的资源，从而能够更好的学习状态值函数，这种优势在实验中也显示了出来，当动作空间很大时，竞争式架构的优势更加明显。

​	相对于Q的大小不同来说，Q值之间的差值更为明显，值可以达到15，差值则为0.04，这种数值尺度上的差异可能会带来噪声。



## Conclusions



