# Robust Adversarial Reinforcement Learning(2017)

## Abstract

​	近些年来仿真速度和计算资源的提升推动了强化学习的成功，但是最近的强化学习模型的泛化能力存疑：（1）在真实世界和仿真环境之间的差距和不同非常大，使得模型学出的策略在这两者之间不能正常的转换（2）即使模型学出的策略在真实世界中成功了，但现实中的数据\通常非常匮乏，使得测试过程无法正常进行。这篇文章提出了鲁棒性对抗强化学习：*训练一个代理在不稳定的对手面前运行，该对手向系统施加干扰力量。共同训练的对手得到加强并能够学会最优的不稳定策略。*将优策略学习归纳为零和最小最大目标函数，最终（1）提升了训练的稳定性（2）使模型对训练测试条件的不同的鲁棒性提高（3）即使在没有对手的情况下表现依然优异。

## Introduction

​		深度神经网络的高容量和端到端的特性是深度强化学习成功的重要原因，但是一个重要的瓶颈是策略的学习对数据的依赖性太大，训练高容量的模型需要大量的训练数据或者是轨迹数据。现实世界中物理任务的数据收集和策略学习显然是非常有挑战性的。两种策略学习的方法（现实物理世界）

### Real-world Policy Learning

expensive、dangerous、time-intensive数据的匮乏性，以及通常会集中与某个特定的场景导致模型过拟合，策略的泛化性能也很低，急需一个能够对不同场景下泛化性能都很好的策略学习方法。

### Learning in Simulation

仿真环境中数据匮乏的问题可以解决但是仿真环境的引擎与现实环境是有区别的，因此学出来的策略应用到现实中也是可能有泛化性很差的问题存在的。

许多政策学习算法本质上是随机的，这进一步加剧了测试泛化和模拟迁移问题*。*

*我们需要的是一种在不同初始化和不同（真实和仿真）环境下运行中更加稳定和鲁棒的方法，并且这种方法训练所需要的数据更少。*

通过将不确定性干扰通过一个能够给环境添加干扰的对抗性代理来表示，并且这种对抗性代理也被加强了，因为他学出了一个对抗初始目标的最优策略。RARL训练了一对代理，主代理和干扰代理，其中主代理学习完成最初的任务目标，同时对其对手产生的破坏保持鲁棒性。

做了一些延伸性的实验评估RARL，证明了RARL对模型的初始化的鲁棒性和误差与不确定性的鲁棒性。

## Overview of RARL

目标：学出一个对仿真和训练与测试中出现的不匹配和误差鲁棒的策略。学习出一个对不同干扰都鲁棒的策略，在无约束的情况下，可能的扰动空间可能大于可能动作的空间，这使得采样轨迹在关节空间中更加稀疏。

为了解决以上的问题提出了两种方法：

（1 ）针对模型干扰的对抗代理：不对所有可能的干扰进行采样，而是共同训练第二个代理(对抗代理)，其目标是通过施加破坏稳定的力量来阻止原代理(主代理)。对手只会因为主角的失败而得到回报。因此，对手学会采样困难的例子:干扰将使原代理失败;主人公学会了一种应对对手制造的任何干扰的稳健政策。
（2）包含领域知识的对抗代理：在主代理的基础上赋予对抗代理以特殊的领域知识来对抗训练主代理。

## Background

![image-20200701115544273](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20200701115544273.png)

## Robust Adversarial RL



![image-20200701121345429](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20200701121345429.png)

这个等式表示状态转换P是个变量，此时对这个求期望结果会对环境的干扰和不稳定性产生鲁棒性。

不是直接使用随机或者固定的对抗对手，而是基于一个学好的策略基础之上产生对抗动作。***在RARL中，对手代理会抽取哪些最糟糕的轨迹样本来对抗主代理，但同时主代理也会从中收益，使得主代理对这些最差的轨迹样本的鲁棒性提高。***对手代理使用力量参数化，力量参数化过大将导致对抗代理抽取的样本太过偏见，使得学习不能进行，***在极限情况下对手代理将使得主代理一直无法成功，因此传统的RL方法可以看做是对抗代理的力量值为0的情况***

### Proposed Method:RARL

第一阶段：固定对抗策略学习主代理策略   接着固定主策略学习对抗策略，重复这个过程到策略收敛。就是这两个代理轮流优化

![image-20200701135855093](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20200701135855093.png)

### Experimental Evaluation

(a)不同初始化场景下的训练
(b)不同条件下测试
(c)带有敌对干扰的测试环境

## Conclusion

（1）RARL 对不同初始化的训练条件鲁棒
（2）对训练测试环境间的改变鲁邦性更好
（3）对测试环境难以仿真的干扰更为鲁棒













