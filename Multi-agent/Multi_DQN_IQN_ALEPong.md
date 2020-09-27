# Multi-agent Cooperation and Competition with Deep Reinforcement Learning(2015)

## Abstract

多智能体出现在政治经济和社会领域逐渐增多，DQN在Pong游戏中的应用，合作性的代理能够找到最优策略使球在游戏盘面上，通过修改游戏的奖励机制来探索智能体间的合作和竞争机制。

## Introduction

交流合作和竞争出现在代理之间，本研究的目的是研究由自主深度q -网络控制的多智能体之间的紧急合作与竞争策略，我们探索了两个个体在如此复杂的环境中如何在不同的奖励方案下表现和互动。

在不同的奖励设置下代理间产生了竞争和合作的行为，竞争的代理在得分方面做得更好，而合作的代理会找到一个最佳的策略来尽可能长时间地保持球在游戏中

## Method

IQL

奖励的配置与代理合作与竞争动作间的关系，研究奖励的设置对代理得分的影响。

几项指标：平均：弹墙次数/击板次数/服务重启时间

## Result

（1）竞争型代理的出现

<img src="C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20200805193631079.png" alt="image-20200805193631079" style="zoom:50%;" />

（2）合作型代理的出现

<img src="C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20200805193651264.png" alt="image-20200805193651264" style="zoom:50%;" />

## Discussion

（1）DQN 对于多智能体系统下复杂环境中是一种非常有效的去中心化学习方法。

（2）奖励机制直接影响了代理之间的合作竞争等行为模式。

（3）在训练过程中发现出现了过估计的问题，后面期待使用Double DQN。

## Future work

目前方法的一个潜在的未来应用是研究在没有任何先验的协议、规则，甚至是他们自己和他们的环境的高级概念的情况下，如何在相互作用的主体之间产生通信代码和共识。