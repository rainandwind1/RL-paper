# Mastering Complex Control in MOBA Games with Deep Reinforcement Learning(2020)

## 摘要

​	多人在线对抗游戏中的1v1比赛，比1v1的传统游戏更为复杂，想要搜索到较好的策略也更为困难，这篇文章从系统和算法的角度提供了一个深度强化学习的解决框架，系统特性：低耦合，高度可伸缩性，算法包括控制依赖解耦、动作遮罩、目标注意机制和dualclip PPO等创新的手段和方法，基于他们提出的ac框架可以有效的训练，在1v1中能够击败职业玩家。

## 介绍

​	我们设计了一个包含多模态输入编码、控制中相互关联解耦、探索剪枝机制和攻击注意力的神经网络结构，以考虑MOBA 1v1游戏中不断变化的游戏情况。

贡献如下：

1. ​		在算法方面，我们开发了一个actor critic神经网络来建模MOBA动作控制。该网络采用多标签近端策略算法(PPO)目标优化，具有控制依赖解耦、目标选择注意机制、有效探索动作面具、学习技能组合LSTM、PPO改进版本dual clip PPO以确保训练收敛性。
2. meile

## System Design

复杂的代理控制会引入高方差，但是大型批处理对于加速训练又是非常必要的，因此设计了一个可伸缩的松耦合系统架构来构建数据并行的效用。

系统组成有以下四部分：1）Reinforcement Learning (RL) Learner  2） Artificial Intelligence (AI) Server 3）Dispatch Module  4）Memory Pool

![image-20200607120825597](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20200607120825597.png)



AI server: 负责环境与ai的交互, 通过self-play与镜像策略生成回合数据，使用玻尔兹曼探索产生对手策略，softmax输出。动作执行后回收奖励等信息，AI服务器与推理模型在同一个CPU为了节省IO输出，快速推理版本为feather CNN（生成episode快速），这个快速版本可以自动的将算法模型转化成用于推理的格式。
Dispatch: 收集样本，压缩，解压，
Memory : 存储样本数据，提供batch，它支持不同长度的样本，以及基于生成时间的数据采样
RL learner: 分布式训练环境，为了加速策略更新使用batch size，多学习器混合并行从memory 池中取数据，用ring allreduce 算法平均梯度，并行训练，但不同与IMPALA，在IMPALA中，参数分布在各个学习者之间，参与者并行地从所有学习者处检索参数。

## Algorithm Design

为了高效的训练这个网络，几种创新的策略被用在了上面，第一个是目标注意力机制：帮助选择组合单位的目标，第二个是LSTMs：帮助学习组合技能以及时给予对方以伤害和持续打击，第三个是控制依赖解耦以形成多标签近端策略优化(PPO)目标。第四个是基于游戏知识的剪枝方法，action mask，最后是双端剪切的PPO算法，保证算法在大批次的收敛性，



## Conclusion and Future Work

​		在本文中，作者提出了一种深度强化学习(DRL)方法来处理MOBA 1v1游戏中代理的复杂动作控制，从系统和算法两个角度。我们提出了一个可扩展的、非策略的DRL系统架构，用于大规模情节探索。我们提出了一个演员批评家多标记神经网络，包括建模MOBA战斗的几种策略，以及一个确保收敛的PPO算法的双剪切版本。我们的框架产生的AI可以击败MOBA 1v1游戏中的顶级专业电子竞技玩家，该游戏在热门MOBA游戏《王者荣耀》中进行了测试。下一步，我们将开放框架和算法，并将《王者荣耀》游戏核心开放给社区，以促进对复杂游戏的进一步研究;我们还将通过虚拟云为公众提供部分计算资源









​	

​	





