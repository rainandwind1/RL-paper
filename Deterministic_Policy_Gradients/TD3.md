# Addressing Function Approximation Error in Actor Critic Methods(2018)

## Abstract

​		典型的基于值函数的强化学习算法例如DQN中的函数逼近误差将导致过估计和次优策略的产生，这些问题同时在AC算法系列中存在，这里我们提出了一种新的机制去同时最小化这种问题在actor 和 critic中的影响。在DDQN的基础上选择较小的critic值来去做差值来限制过估计的问题，我们指出了target网络和过估计的偏差之间的关系，并且我们建议延迟策略的更新以此来降低每次更新的误差从而提升算法性能。我们在OpenAI gym上评估算法的性能，并且都取得了较好的性能。

## Introduction

​		就说这个过估计的问题在离散空间问题中研究的很多，但是在连续空间控制问题中基本没进展，这篇文章将会呈现这种时分方法中的误差累积（ac设定中），由于逼近器的误差造成的过估计是不可避免的，并且这种误差会随着时分学习的引入而增大（自举），

​		![image-20200521201336109](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20200521201336109.png)

​		DPG也存在这种问题，target网络对于方差约减来说是非常重要的，可以有效的减少累积误差，提出了延迟的策略更新知道值的估计收敛才更新策略，最后我们提出了一个创新性的正则策略，利用Sarsa式的更新来引导相似的动作估计从而在未来减少方差。

​		在DDPG的基础上形成了Twin Delayed Deep Determined Policy Gradient(TD3)算法

## Related Work

​		由于估计带来的误差：过估计偏差，高方差构建，已存在的几种应对方法：DDQN，直接减少方差值的方法（方差约减），矫正，以及通过异策略加蒙特卡洛回归最小化误差的尺度。

​		提出了通过平均值估计的方式来进行方差约减，平滑值函数可以用于训练随机策略，提升性能。

​		近期工作：重要性采样，分布式方法，逼近约束等等方法，减少折扣因子等等。

## Background

​		强化学习基本知识AC+DQN的

## Overestimation Bias

​		由于误差带来的过估计不可避免，从而影响到策略的更新，在ac中虽然策略是通过梯度更新的，但是仍然会存在过估计的影响。

### Overestimation Bias in Actor Critic

### Clipped Double Q-Learning for Actor Critic

![image-20200601211513627](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20200601211513627.png)

这种剪切会出现低估的问题，但是这种低估的问题比高估更容易处理，因为低估的动作不会随着策略的更新传递下去。

并且这样在ac的设定中只需要三个网络就行了，共享的actor网络以及两个critic网络。并且会将选择的中心倾向于低方差的动作估计，从而使得策略更新更加稳定。

## Adressing Variance

最小化误差的重要性

### Accumulating Error

### Target Networks and Delayed Policy Updates

![image-20200601222507886](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20200601222507886.png)

降低policy net的更新频率，等到value网络的error足够小时，在更新policy，并且在目标网络中使用跟随的方式更新网络参数。

策略更新"少而精"的策略核心

### Target Policy Smoothing Regularization

由于确定性策略的输出值的单一性可能导致网络的更新误差不断积累使得方差变大，这里使用一个平滑的正则措施，每次更新为一个确定性策略输出值的邻域，这里默认每个动作的周围小空间内的更新是类似的，或者说具有相同的价值。这个邻域通过增加噪声来实现，剪切的噪声。



![image-20200601224251377](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20200601224251377.png)



## Experiments

连续控制任务：

​		![image-20200602091946348](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20200602091946348.png)



基本全领先，实验参数等配置在这一段。

## Evaluation



## Conclusion

证明了过估计的问题不仅是基于值函数方法的通病，在ac方法中也会出现，验证了累积误差的影响以及累积误差与过估计之间的关系，证明了target net的重要作用，限制误差提高优化与逼近的精度，这种TD3的架构可以配置到任意的ac方法中。