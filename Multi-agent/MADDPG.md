# Multi-Agent Actor-Critic for Mixed Cooperative-Competitive Environments(2017)

## Abstract

首先分析传统强化学习算法在多智能体中使用的困难性，提出一中ac方法可以考虑其他代理的动作策略，成功的学习出复杂的多智能体协调策略，并且引入了新的训练机制提高了代理策略的鲁棒性，在合作性和对抗性的环境中进行了实验。

## Introduction

传统的强化学习如QL和PG通常在多智能体的环境下效果不好，其根本原因是每个代理的策略随着训练过程不断变化，从每一个单独的代理的角度来看，环境都是非平稳的，这对学习算法的稳定性发出了挑战并且不能使用经验回放，PG算法在多智能体协调的需求下方差太高；

提出了一种通用的多智能体算法，（1）策略的学习依靠部分观测信息（局部信息）在执行动作时（2）不需要特殊结构的代理信息交互机制和可微的环境动态模型，（3）竞争和合作和混合动作下都适用

提出了集中训练分散执行的框架，允许策略使用多余的信息来简化训练，这种信息在测试阶段不会使用，因此这种结构使得QL算法不能应用在其上，于是应用ac的架构，这里actor使用局部信息，critic使用全局代理的信息，这时在执行动作时运用的就是局部的信息，在竞争和和合作设定下都可以使用。在训练阶段critic可以使用全局信息训练，由于在测试执行阶段与训练阶段一样，仅仅是为了得出动作，而actor的训练和输出都依靠的是局部信息，这在测试和训练阶段的设置是一样的，而QL这类的算法在测试和训练时由于用的是同一个网络这样就不能直接使用全局信息。

们还引入了一种方法来提高多智能体策略的稳定性，方法是使用*一套策略*来训练智能体，因此需要与各种协作者和竞争对手策略进行健壮的交互？？

## Methods

徐志伟博士如是说道：因为每个单独的智能体在不断更新自己的策略，智能体以自己为中心来看，其余智能体和环境组成了总体的环境，因此环境相当于不停的在变化（非平稳性），于是IQL就会不稳定。

这种非平稳性也会使得PG算法的方差很大，并且降低方差的方法设置也收到限制。

DPG：

DDPG：目标网络+replay buffer+ac

中心训练，分散执行。

## <img src="C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20200806143934014.png" alt="image-20200806143934014" style="zoom: 67%;" />

基于以下三个约束：

（1）学习出的策略在执行时仅可以使用局部信息

（2）没有环境是一个动态可微的模型假设

（3）没有假设一个可区分的通信通道

只要在测试阶段不使用多余的信息，在训练阶段策略可以使用，因为Q函数在训练和测试时通常不能包含不同的信息，因此QL不适用，设计了一个ac架构，actor局部信息，critic利用全局信息学习， CTDE+DDPG=MADDGP

***应对多智能体环境下由于单个智能体的策略改变造成的的非平稳分布问题***：

![image-20200806152906624](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20200806152906624.png)

## Experiments

## Discussion

只考虑部分代理Q函数的Q模块

![image-20200806194948907](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20200806194948907.png)
