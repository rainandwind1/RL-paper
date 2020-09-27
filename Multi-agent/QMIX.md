# QMIX : Monotonic Value Function Factorisation For Deep Multi-Agent Reinforcement Learning(2018)

深度强化学习的单调值函数因式分解

## Abstract

学习基于额外信息的联合动作值是一种有效的开发集中学习的方式。QMIX——一种集中的端到端的训练离散策略的算法，QMIX使用一个网络来估计联合动作值，这个网络将每个代理的值作为一个复杂的非线性组合，而这些组合仅约束于局部观察。在结构上强制执行每个智能体值中的联合动作值是单调的，这允许在非策略学习中联合行动值可跟踪地最大化，并保证集中和分散策略之间的一致性。在星际争霸二的微代理任务中进行测试。

## Introduction

部分观测性和通信条件的约束性使得学习离散化的策略成为必要，围绕如何最好地利用集中式训练的许多挑战仍然存在。

$Q_{tot}$条件于全局状态和联合动作，当有许多代理时，这样的功能是很难学习的，即使它可以学习，也没有提供明显的方法来提取分散策略，以允许每个代理仅根据单个观察选择单个操作。

单纯的学习离散的局部Q函数：不稳定收敛性得不到保证

单纯的学习全局Q函数：智能体数目较少时不切实际，并且同策略的方法使得其采样效率极低。

值分解网络（VDN）：VDN严重限制了集中动作-价值函数的复杂性，忽略了训练过程中任何额外的状态信息。

QMIX：VDN的完全因式分解对于提取去中心化的策略是不必要的;

![image-20200807110627404](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20200807110627404.png)

QMIX的思想：

![image-20200807110904489](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20200807110904489.png)

通过限制混合网络的权值为正来确保偏导大于零的约束。

## QMIX

DQN  DRQN  IQL VDN

在实践中，即使在混合游戏和竞争游戏中，IQL通常也是一个非常强大的基准（虽然其本身未解决由于智能体间的策略改变造成的环境的非平稳性使其本身的收敛性得不到保证的问题）

一致性约束要求：VDN完全满足（强满足）

![image-20200807143328045](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20200807143328045.png)

agent net    mix net 权值为正，非负

![image-20200807154811360](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20200807154811360.png)



## Experiments



## Conclusion





