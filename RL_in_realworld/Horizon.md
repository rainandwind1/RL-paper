# Horizon: Facebook’s Open Source Applied Reinforcement Learning Platform

## Abstract

​		Horizon Facebook开源强化学习应用平台，端到端的解决大数据集下的工业场景应用强化学习问题，反馈回路慢，实验需谨慎，以生产用例为中心的，平台包含的工作流有：数据预处理，特征转换，分布式训练，反事实的策略评估，优化服务以及基于模型的数据理解（处理）工具。并使用实验证明了利用Horizon训练出来的RL模型由于脸书上的监督模型。

## Introduction

​	深度强化学习将彻底改变自动系统的构建方式，然而当前强化学习的大部分工作都是针对于学术研究的，聚焦于模拟环境中的评估。

![image-20200510123517602](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20200510123517602.png)

![image-20200510122813357](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20200510122813357.png)

### Data preprocessing

​	带有自动转换数据成为测试算法的输入数据格式

### Feature Normalization

​	提取每个特征的元数据的类型和正则化的方法，这些数据将自动的使用在训练和服务过程中的预处理特征中。

### Data Understanding Tool

​	在现实环境中并没有那么容易满足MDP问题，并且没有规定好的状态转换对可循，这里提供了一个参考和解释以及自动的识别和检索公式。

### Deep RL model implementations

​	Horizon提供了以下算法的实现：离散动作：DQN、DDQN、Dueling D/DQN；连续动作：DDPG、SAC

### Multi-Node and Milti-GPU training

​	Horizon支持CPU GPU 多GPU以及多节点的训练方式

### Counterfactual Policy evaluation

### Optimization Serving

​	Caffe2 优化模型的参数和可移植性，以便应用到千百台机器上。

### Test Algorithms

## Data Preprocessing


