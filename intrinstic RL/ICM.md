# Curiosity-driven Exploration by Self-supervised Prediction(2017)

Intrinsic Curiosity Module (ICM)

## Abstract

​	在真实场景中外在奖励通常是稀疏的甚至是缺省的，这个时候好奇心将是代理在未来阶段的一个重要的技能，这里将好奇心定义为agent在通过自监督逆动力学模型学习的视觉特征空间中预测自身行为的能力中的误差，（1）外在奖励稀疏的情况下，好奇心的代理能够在与环境交互的更少的情况下达到学习目标；（2）在没有外部奖励的探索下，好奇心能够推动代理更有效的探索；（3）对于不可见区域的探索能力速度也是显著提高。

## Introduction

​	好奇心是一种可能在未来获得奖励回报的学习技巧。大多数的内在奖励公式可以被分为两类，（1）鼓励代理探索新的状态（2）鼓励代理执行能够减少预测动作序列误差的动作

​	好奇心的两个基础用途：1.帮助探索环境  2.帮助学习在未来可能用到的技巧

​	所提出的方法使agent能够在没有明确目标的情况下**学习可推广的技能**。

## Curiosity-Driven Exploration

​	代理由两个子系统组成：一个奖励生成器，输出好奇心驱使的内部奖励信号，另一个是策略输出最大化奖励信号的动作序列。除了内部奖励信号，代理也会收到些许外部奖励信号（来自环境的），整个奖励信号的组成如下：

​	![image-20200610220756335](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20200610220756335.png)

### Prediction error as curiosity reward

​	直接使用原生的像素来描述误差并使用该误差作为好奇心的驱动力是片面的并且容易造成很大的误差和问题，那么该怎么选取特征来做预测从而使得该误差能够较好的作为测量好奇心大小的量具呢，这里有三种情况：（1）代理能够控制的事物（2）代理不能控制的事物但是这个事物能够影响代理（3）代理不能控制并且这个事物不会影响代理。那么一个好的量具应该具备1，2的功能同时不会受到3的影响。

### Self-supervised prediction for exploration

![image-20200611102610342](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20200611102610342.png)

正向逆向动力学模型   正向：预测St+1,	逆向：预测at

## Experimental Setup



![image-20200611170719201](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20200611170719201.png)

![image-20200611170733057](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20200611170733057.png)

![image-20200611170742610](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20200611170742610.png)

![image-20200611170751671](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20200611170751671.png)

