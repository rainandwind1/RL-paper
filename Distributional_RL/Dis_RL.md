# A Distributional Perspective on Reinforcement Learning 2017

## Abstract

讨论了值函数分布的重要性，随机回报的分布，通常学习分布的方法被用于风险行为评估上，在策略评估和控制上学习期望回报或者值函数的方法暴露出不稳定性，我们之后从分布式的角度设计了一个新的应用在贝尔曼等式上学习逼近值分布的算法，使用ALE环境平台进行评估，实验结果证明了学习值分布的优越性。

## Introduction

随机回报$Z$，期望代表$Q$，并使用等式代表其中的一个分布式的期望性质：

$Z(x,a)\overset{D}{=}R(x,a)+\gamma Z(X',A')$

传统的值分布的用处：(1)对参数不稳定性进行建模（2）设计风险敏感算法（3）理论分析

## Instability in control settintg

在策略评估情况下贝尔曼最优方程的分布式版本的不稳定性。

根本原因：收缩算子在期望值上是收缩的，但是在分布式的矩阵中不是收缩的，为建立分平稳分布的策略效果的算法提供了保证。

更好的逼近作用：站在算法的角度，学习逼近分布比学习逼近期望有更多的好处，贝尔曼算子保持了值分布的多态性，我们相信这会提高学习的稳定性，对整个分布的逼近也会缓和学习非平稳策略的影响。

这种学习分布的方法能够使得强化学习的效果显著提升。

用DQN代理学习值分布，从监督学习的角度来看，学习值分布是显而易见的，为什么要限制在均值上呢？从猜测中学习猜测。

## Setting

齐次马尔科夫决策过程，其中R为奖励函数，在这里我们将它视为一个随机变量，平稳分布的策略。

## Bellman's Equations

把值函数视为一个向量，期望回报

<img src="C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20200419170637253.png" alt="image-20200419170637253" style="zoom:100%;" />

## The Distributional Bellman Operators

将$Z^{\pi}$看做是一个状态动作对到回报的映射，称之为值分布。

## Distributional Equations

利用可能性空间是非常方便的

## Policy Evaluation

![image-20200420101044872](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20200420101044872.png)

![image-20200420101420087](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20200420101420087.png)

这里表面上贝尔曼算子与普通的没什么区别，实际上有三个随机源定义了这个贝尔曼算子的复合分布。

（1）奖励R的随机性
（2）状态转换$P^{\pi}$的随机性
（3）next state变量$Z(X',A')$

等式(5)是一个收缩映射，唯一的不动点就是$Z^{\pi}$ 

## Contraction in $\overset{-}{d_p}$

![image-20200420111836780](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20200420111836780.png)

在变分距离、KL散度上都不是收缩算子熬。

## Control

​	最优策略可以有很多个但是他们对应的最优Q值只有一个，而这里最优策略对应的最优值分布可能有多个，贪婪更新可能固有着分布式优化算子的在矩阵情况下的不收缩性。

​	定义最优值分布![image-20200421220509557](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20200421220509557.png)

​	以及贪婪策略值分布：![image-20200421221117605](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20200421221117605.png)

​	相应的贝尔曼最优算子也是提出了一个分布式贝尔曼最优算子

​	非平稳分布的最优照顾分布为$Z^{**}$，控制设定中的收敛性：

![image-20200421223500092](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20200421223500092.png)

## Approximate Distribution Learning

​	基于分布式贝尔曼最优算子得到一个新的算法，考虑选择使用一个近似的分布例如高斯分布。这里我们使用了丰富的近似分布。

### Parametric DIstribution

![image-20200422204121200](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20200422204121200.png)

### Projected Bellman Update

![image-20200426101517806](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20200426101517806.png)

## Advantages

![image-20200426103038633](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20200426103038633.png)

## Discussion

学习值分布的优点显著。

为什么学习分布很重要？：

（1）Reduced chattering(震荡减少)： 由于贝尔曼优化算子带来的不稳定性与函数逼近器结合后使策略不能收敛，这种现象称为震荡，基于梯度的CA算法能够有效的缓和这中震荡通过平均不同的分布来使得震荡混合在近似解中，类似保守的策略迭代。

（2）State aliasing（量化状态）：在确定性的环境中量化状态也能有效的产生随机性。在部分可观测领域中将表示学习与策略学习耦合的重要性。

（3）A richer set of predictions(丰富的预测)：从多种预测中学习是人工智能的循环出现的主题， 分佈的方法提供了一种辅助预测，即回报将带有一定的可能性。

（4）Framework for inductive bias(归纳性偏差架构)：

（5）Well-behaved optimization：利用KL散度当做loss使其容易最小化，连续密度下的KL散度效果并不好，因为其对结果值并不敏感。







