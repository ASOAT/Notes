Authors: Haowei Sun, Shuo Feng, Xintao Yan, Henry X. Liu
Year: 2021
Status: #literature
Tags: [[自动驾驶测试]]
# Corner Case Generation and Analysis for Safety Assessment of Autonomous Vehicles
光看论文感觉又是挺想当然的一篇论文，当然实际上的工作肯定不止论文这么简单，但是论文里面只有一点公式。。也无法说明到底是什么样的Corner case，只是单纯提高Failure的概率。

车辆状态，其中$p$表示位置（*是什么位置？s-t坐标系？x-y？还是只有waypoint然后采样的纵向位置？*）:
$$x = \{p, v, \alpha\}$$
$m_t$表示$t$时刻被测车辆周围被观测到的车辆的数量（*那么怎么定义为被观测到呢？是只有靠近车辆一定距离算是被观测到了？还是考虑到了被遮挡的情况？*）
整个场景在$t$时刻被表示为：
$$X = \{s_0,s_1,\cdot,s_n\}$$
用$A$表示感兴趣的事件，$\theta$表示场景的参数，整个过程被描述为一个马尔可夫决策过程，目标则是最大化$P(A|\theta)$：
$$P(A|\theta) = \sum_{X \in D}P(A|X)P(X|\theta)$$
其中：
$$P(X|\theta) = p(s_0|\theta) \prod ^{m-1}_{k=0}P(s_{k+1}|u_k,s_k,\theta)P(u_k|s_k,\theta)$$
然后使用DRL的方法求解呗

然后用聚类等方法，使用自然驾驶数据集的边界得到较为自然的碰撞场景。









---
# Extension Papers
