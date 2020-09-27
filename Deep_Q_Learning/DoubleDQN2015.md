# Deep Reinforcement Learning with Double Q-learning  DP 2015 

## Abstract

​	流行的Q-learning算法在某些特定条件下过高的估计了动作值函数的数值，这种过拟合在实际中的影响以及其是否可以避免还是个未知数，然而在这篇论文里我们将一一回答，新提出的Double Q-learning不仅降低了过大的估计值，在很多游戏中表现也不错。

​	强化学习的目的：在序贯决策中通过优化累计奖励信号来学习出好的策略，Q-learning中由于每次更新值函数时取最大的操作可能造成最后值函数数值过大的弊端，当动作值不准确时，不管误差来源于哪里，这种过高的估计都会出现。Double-DQN 相对于DQN在估计动作值上更为精确，并且总的得分更高。

## Background

### Deep Q Networks

target network + experience replay

### Double Q-learning

两个值函数网络，一个用来决定（产生）策略（动作），另一个用于决定他的值。

### Overoptimism due to estimation errors

figure2 对照结果证明了overestimation和拟合函数的灵活性对实验误差的影响。在Q-learning中由于取最大值的操作，overoptimism很容易出现，并且随着bootstrap不断地累积增长。自举加上overoptimsim会使得错误信息得到放大（哪些状态优于另一些状态），使得所学得的策略误差增大。

## Double DQN

 Double Q-learning降低overestimation的方法是将目标最大值的操作分解成动作选择和动作评估，尽管没有完全解耦，在DQN中target网络的架构是一个在不引入第二个网络的前提下达到此效果的一种方式，由此结合DQN和Double Q-learning的思想我们提出了Double DQN算法，使用Double DQN的更新方法，结合DQN的target网络架构，我们可以在不引入第二个网络的前提下实现Double Q-learning的目标，降低overoptimisim，同时保证计算量的最小增加。

## Result on overoptimisim

## Quality of the learned policies

## Robustness to Human starts

为了防止学出的策略对于游戏固定起始点的相关性，从而使得策略的鲁棒性和泛化性能降低，这里采用人为设置的不同的游戏起始点来做训练试验，

## Discussion

这篇文章所做出的五个贡献：

1.第一，展示了Q-learning在大规模问题中容易overoptimisim(overestimation)的问题，即使是在确定性的问题中，归咎于算法本身的缺陷，算法学习的固有缺陷。

2.第二，通过分析雅达利游戏中值函数的估计情况，展示了这种overoptimisim在实践中比之前认为的更加普遍和严重。

3.第三，展示了Double Q-learning 能够成功的减少这种overoptimisim现象，使得学习出的策略更加稳定可信。

4.第四，结合Double Q-learning和DQN，提出了Double DQN算法，在不增加额外的网络参数的情况下利用DQN的框架和神经网络，实现Double Q-learning的效果。

5.最后展示了Double DQN 在雅达利游戏上的优异性能，能够或得更好的策略。