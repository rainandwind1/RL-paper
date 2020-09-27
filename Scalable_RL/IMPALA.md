# IMPALA: Scalable Distributed Deep RL with Importance Weighted Actor-Learner Architectures(2018)

 ## Abstract

解决使用单一代理学习器和参数的一系列任务，关键的挑战之一是应对大规模增加的数据和训练时间，开发了一个新的分布式代理IMPALA(Importance Weighted Actor-Learner Architecture)，此架构在单机训练的资源利用效率表现优异并且在大批量机器训练下的数据资源效率上也保持的很好。通过将解耦行为和学习同时与一种名为V-trace的策略外校正方法相结合，实现了高吞吐量下的稳定的学习。并在多任务强化学习中以及雅达利游戏中证明了IMPALA的有效性，最终证明了IMPALA在稀疏数据下表现更好，同时揭示了多任务训练中任务之间的转移性。

## Introduction

近年来的深度强化学习的进展中大多是每个任务中分开的训练一个代理，于是乎想要开发出一个能够同时掌握一系列任务的代理，以及适用对于不同环境下的评估方法。

A3C 的训练速度和对样本的利用率还是不够理想，距离应用还有距离。IMPALA能够在不损失训练速度和数据效率的前提下将训练机器拓展到数千台。A3C将策略参数传递给中心参数服务器，IMPALA将代理的轨迹信息传递给一个中心学习者，并使用GPU小批量处理轨迹并行化所有时间的独立操作。这种解耦的架构能够达到一个非常高的通量。由于行为策略会滞后于学习的目标策略（多次更新），因此使得学习成为异策略的学习过程。因此使用V-trace的算法来矫正这种有害效果。

通过可伸缩架构和V-trace的结合，IMPALA实现了极高的数据吞吐量每秒25万帧，比单机A3C快30多倍。更重要的是，IMPALA比基于A3C的代理数据效率更高，对超参数值和网络架构更健壮，从而使得IMPALA可以使用更深层的神经网络。

<img src="C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20200720104839707.png" alt="image-20200720104839707" style="zoom:50%;" />

## Related work

## IMPALA

同步参数更新

### Efficiency Optimisations

在batch中加入时间维度，LSTM 网络，

## V-trace

在解耦的分布式参与者-学习者架构中，异策略学习非常重要，因为在参与者生成动作和学习者估计梯度之间存在时滞；

异策略学习的目标：用行为策略产生轨迹来学习目标策略

### V-trace target

![image-20200720165058713](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20200720165058713.png)

这样一来异策略和同策略都适用。

两个阶段重要性参数的作用不同：

![image-20200720181106832](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20200720181106832.png)

两个知注意点：

<img src="C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20200720182056233.png" alt="image-20200720182056233" style="zoom:50%;" />

？？



![image-20200720182633070](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20200720182633070.png)

V-trace Ac 算法：加入了熵正则，避免提前收敛

![image-20200720183240454](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20200720183240454.png)

## Experiments

计算效率和尺度上的可伸缩性是IMPALA的初衷，

对V-trace的效果进行了一个对比的实验：

1.No-correction :No off-policy correction
2.$\epsilon$-correction:在梯度计算时增加一个较小的常数$\epsilon$避免过低的梯度值出现
3.1-step importance sampling:没有c
4.V-trace

## Conclusion