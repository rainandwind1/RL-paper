# $RL^2$: Fast Reinforcement Learning Via Slow Reinforcement Learning(2016)

## Abstract

传统强化学习虽然能够学习很复杂的任务，但是其训练过程需要大量的试验（试错），反观现实中很多动物基于很少的试验就能够掌握一些新的任务，本篇文章致力于解决这个问题，算法利用RNN表示并学习，编码到RNN的权值中，RNN接收的信息与典型的RL算法基本相同，大小尺度的任务中效果都不错。

## Introduction

这里说到之所以学习的效率低下的原因之一是缺乏先验，使得代理必须重新从训练中重建关于世界的知识。

贝叶斯强化学习提供了一个将先验知识纳入学习过程的框架，但是贝叶斯的计算实在是复杂繁琐，因此，实际的强化学习算法往往结合贝叶斯和特定领域的思想，以降低样本的复杂性和计算负担。

相比于设计特殊环境下的强化学习算法，这里将智能体本身的学习过程视为一个目标，可以使用标准的强化学习算法进行优化。

将代理建立为一个RNN网络，将过去的经过正则化的状态、奖励、动作和结束标志等作为输入，保存回合过程中的隐层状态，此时代理就成为看了一个学习的算法，并且能够随时部署在我们手头的任务上。

## Method

对强化学习问题的简述。

![image-20200729112650119](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20200729112650119.png)

### Policy Representation

用RNN表示策略，以s,a,r,done_flag为输入，输入之前加入嵌入层，为防止梯度爆炸和消失等问题使用GRU网络，输出接着全连接层和softmax处理，输出动作的分布。

### Policy Optimization

为减少调参的工作量选择TRPO算法，同时使用GAE减少方差。

## Evaluation

两个问题：（1）对于特殊的MDP问题能否解决或适应（2）能否解决高维问题



## Discussion

本文提出了一种设计更好的强化学习算法的不同方法:与其自己充当设计人员，不如使用标准的强化学习技术端到端地学习算法；即“快速”RL算法是一种计算，其状态存储在RNN激活中，RNN的权值由通用的“慢”强化学习算法学习；



 



