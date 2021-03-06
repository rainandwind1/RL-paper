# Exploration By Random Network Distribution (2018)

## Abstract

为强化学习引入一种探索奖励，这种方法简单易实现并且增加的计算代价最小，这种奖励是通过一个固定随机初始化的网络预测输出与观测之间的误差实现的，同时引入了一种灵活组合的启发式外部奖励，随机网络分布奖励（RND）组合外部奖励的方式显著提高了雅达利游戏的探索能力，并且首次在某些游戏中的表现超越人类。

## Introduction

强化学习的传统设定在密集奖励的情况下很容易成功，但是在奖励稀疏的情况下通常找不到最优策略，现实中稀疏奖励的情况非常普遍。

RND 简单易实现，在高维空间中表现很好，可以和策略优化算法一起使用，计算效率高，其探索奖励基于观测状态与神经网络的输出间的误差，真能够促进，基于agent过去经验的网络的预测错误来量化新经验的新奇性。

举个例子，这里以代理当前的观测和动作为输入，预测下一个观测， 最大化这个误差的代理将能够具备发现那些噪声大的观测的能力，但实现起来比较困难。

对于这种不希望看到的随机性，我们提出了一种替代解决方案，即通过使用一个答案是其输入的确定性函数的预测问题来定义探索奖励。即预测一个固定随机初始化的神经网络基于当前观测（以当前观测为输入）的输出。

此外发现当忽视了外部奖励之后，代理还是能够通过最大化RND探索奖励达到较好的效果，利用PPO将外部奖励和RND奖励结合，

## Method

### Exploration Bonuses

奖励有两部分组成：$r_t=e_t+i_t$其中$e_t$是环境奖励，$i_t$为探索奖励，其值在那些新的状态下较大，常被访问的状态下较小，

基于计数的探索奖励：

![image-20200727111113836](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20200727111113836.png)

可算的是有限状态下的表格型情况，非表格的无限状态情况下使用近似伪计数的方法。

另一种计算$i_t$的方法是作为代理状态转换的预测误差，

### Random Network Distribution

 两个神经网络：一个固定随机初始化的目标网络用于设置预测问题，和一个利用代理收集的数据训练的预测网络。目标网络对一个观测实现嵌入，预测网络使用梯度下降法训练最小化预测误差：

![image-20200727113256214](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20200727113256214.png)

这种设定下访问次数越少的新状态其误差越大，访问次数越多的旧状态其预测误差越小。

#### 预测误差的误差源的分类

***1.训练数据的规模：例子少，训练误差高*** --- > RND利用了这个

2.随机性：由于目标函数是随机的(任意不确定性)，预测误差较大。

3.模型误分类（输出错误/误差）：由于缺少必要的信息，或模型类过于有限，无法适应目标函数的复杂性，预测误差较大。

4.学习动力：预测误差太高，因为优化过程找不到合适的预测模型类别

2和3 RND成功避开因为其确定性网络的和内类模型预测网络的性质。

### 与不确定度量化的关系

精馏误差可以被视为在预测常数零函数时的不确定性的量化

## 组合内部奖励和外部奖励

## 奖励与观测的正则化

有些环境的探索奖励受到奖励尺度大小的影响程度不一，因此为了保持奖励在一个一致的尺度上我们标准化了内在奖励除以内在回报标准差的运行估计。

观测的正则化很重要，因为对于一个固定参数的神经网络来说不同的数据集的尺度不同，因此网络的参数会受到数据尺度影响

预测网络和目标网络使用相同的正则方法，

## Experiments

episodic 和 no-episodic之间的实验效果区别

## Discussion

伪代码：

![image-20200728112302463](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20200728112302463.png)





 



