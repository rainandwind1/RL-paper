# Rainbow: Combing Improvements in Deep Reinforcement Learning 2017

## Abstract

​	说到目前为止DQN上的提升的技巧和方向已经有不少了，但是这些方法中哪些是互补的还不知道，如何组合他们以发挥作用仍然没有研究透彻，这篇文章针对6个DQN的拓展研究了他们的组合。就是rainbow产生的来由，并根据实验显示了算法在数据效率和性能上的优异表现，并且做了烧蚀实验。

## Introduction

​	DQN : 经验回放+卷积神经网络  2015

​	DDQN： 解耦操作 评估自举的动作  2016

​	Prioritized Replay: 提高了经验回放的效率 2015

​	Dueling networks : 通过将状态和动作优势值函数分开表示泛化动作 2016

​	A3C：方差和偏差的平衡，将观测的奖励更快的传到每一个状态上 2016

​	Distributed QN：学习折扣回报的交叉熵分布而不是期望 2017

​	Noisy DQN: 使用随机网络层来负责探索。 2017

## Background

DQN : 经验回放+卷积神经网络  2015

​	DDQN： 解耦操作 评估自举的动作  2016

​	Prioritized Replay: 提高了经验回放的效率 2015

​	Dueling networks : 通过将状态和动作优势值函数分开表示泛化动作 2016

​	A3C：方差和偏差的平衡，将观测的奖励更快的传到每一个状态上 2016

​	Distributed QN：学习折扣回报的交叉熵分布而不是期望 2017

​	Noisy DQN: 使用随机网络层来负责探索。 2017

## The Integrated Agent

截断式的n-step Distribuition RL loss加 Dueling架构使用KL损失当做有限回放的标准，将线性网络改为noisy线性网络。



