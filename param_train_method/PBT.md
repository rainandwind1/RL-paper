# Population Based Training of Neural Networks(2017)

 ## Abstract

深度神经网络的训练对模型架构、损失函数和优化函数等的超参数的敏感性一直是一个令人困扰的事情。PBT一个简单的异步优化算法，他有效的利用了一个固定计算预算来优化模型群体以及他们的超参数并达到最大的性能表现。重要的是，PBT发现了一个超参数设置的时间表，而不是遵循一般的次优策略，试图找到一个单一的固定集用于整个训练过程。PBT表现出更快的收敛特性和更高的性能。PBT能够自动发现超参数调度和模型选择，从而获得稳定的训练和更好的最终性能。

## Introduction

模型结构、数据呈现、模型优化细节等过程被诸多的超参数控制，如何调节合适的参数，调节过程非常的耗费算力，耗时耗力。

像深度强化学习这样的场景中，还有另一个复杂的层次，其中学习问题本身可能是非平稳的(例如，依赖于agent当前能够探索的环境的哪个部分)。因此，这类学习问题的理想超参数可能本身就是高度非平稳的，并且应该以一种阻止提前设置日程的方式变化。

两种调参的方法：并行搜索和串行优化；根据计算效率和资源来权衡，并行搜索同时进行多个优化过程——网格搜索和随机搜索；串行优化：使用从早期训练中获得的信息来逐步执行超参数优化，以通知以后的训练——例如手动优化和贝叶斯优化。串行优化一般会提供最好的解决方案，但需要多次串行训练运行，这通常是不可行的漫长的优化过程。

PBT拓展并结合了并行搜索和串行优化的方法，效果显著，利用了多个并发运行的优化过程的种群之间的信息共享，并允许基于性能在种群成员之间在线传播/传输参数和超参数。

此外，与大多数其他自适应方案不同，PBT够执行在线自适应的超参数-这在高度非平稳的学习动态的问题中非常重要，如强化学习。

PBT去中心化、异步，需要的开销和设置也非常少，具有自适应的调参能力。

在强化学习、监督学习中表现非凡，其提升点如下：

(a)训练过程中的超参自动选择
(b)在线模型选择，在最大化利用前置模型的计算上
(c)在线适应超参数的能力，使非平稳训练体制和发现复杂的超参数时间表。

A3C 的训练速度和对样本的利用率还是不够理想，距离应用还有距离。IMPALA能够在不损失训练速度和数据效率的前提下将训练机器拓展到数千台。A3C将策略参数传递给中心参数服务器，IMPALA将代理的轨迹信息传递给一个中心学习者，并使用GPU小批量处理轨迹并行化所有时间的独立操作。这种解耦的架构能够达到一个非常高的通量。由于行为策略会滞后于学习的目标策略（多次更新），因此使得学习成为异策略的学习过程。因此使用V-trace的算法来矫正这种有害效果。

通过可伸缩架构和V-trace的结合，IMPALA实现了极高的数据吞吐量每秒25万帧，比单机A3C快30多倍。更重要的是，IMPALA比基于A3C的代理数据效率更高，对超参数值和网络架构更健壮，从而使得IMPALA可以使用更深层的神经网络。

<img src="C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20200720104839707.png" alt="image-20200720104839707" style="zoom:50%;" />

## Related work

PBT从遗传算发中继承了很多思想，

串行优化：耗费计算资源相对较少，但是其优化次数较多
并行搜索：每组参数并行训练，耗费计算资源
PBT:并行训练多组参数，周期性评估参数表现；如果其中出现表现不佳的组合，则使用更好的模型取而代之，可以将计算资源整合到有潜力的参数组合上，因此效率大大提升，得到的结果也有质量的保证。

PBT 本身也有超参但是其调节速度比目标超参慢

## Population Based Training

一般的优化算法的目标是通过梯度下降等算法优化参数$\theta$以最值化目标函数$\hat{Q}$，但是我们实际关心的指标$Q$很可能与最值化目标不一致，PBT就是针对实际关心的目标函数$Q$来联合优化参数$\theta$和超参数$h$，首先定义评估目标函数$Q$，使用当前模型$f$的状态，并且定义评估函数仅是可训练参数$\theta$的函数，于是优化目标如下：
$$
\theta^{*}=\mathop{argmax}\limits_{\theta\in P}eval(\theta)
$$

### eval

注意，**$eval$**函数不需要是可微的，也不需要与下面列出的优化步骤中用于计算迭代更新的函数相同(尽管它们应该是相关的)
$$
\theta\leftarrow step(\theta|h)
$$
![image-20200721214728785](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20200721214728785.png)

这个过程耗时耗力，并且解对超参数的选择顺序非常敏感，不争取的选择参数将导致失败或者解的质量很差，通常需要对超参的先验知识（调参经验）。

于是进一步我们可以先确定最优超参，接着优化参数$\theta$：

![image-20200721215412210](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20200721215412210.png)

于是乎对N个$h$就会有N个最优的$\theta$产生，于是乎就可在这个种群中寻找最优参数;

### exploit  & explore

![image-20200721223104020](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20200721223104020.png)

具体过程实例：

![image-20200721223517533](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20200721223517533.png)

探索提供了小的修正，开发提供了核心的发力点

![image-20200721224139023](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20200721224139023.png)



![image-20200721175945562](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20200721175945562.png)

## Experiments

几个图很重要，说明了PBT的一些特性和RL的特性（树状图）

### Deep Reinforcement Learning

### Machine Translation

### Generative Adversarial Networks



## Conclusions