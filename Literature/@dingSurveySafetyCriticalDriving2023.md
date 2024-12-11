Authors: Wenhao Ding, Chejian Xu, Mansur Arief, Haohong Lin, Bo Li, Ding Zhao
Year: 2023
Status: #literature
Tags:  [[Scenario generation]];
# A Survey on Safety-Critical Driving Scenario Generation—A Methodological Perspective
从系统的鲁棒性出发
## Overview of safety-critical scenario
场景参数化：$x \in \mathcal{X} = \{\mathcal{S},\mathcal{I},\mathcal{B}\}$，Static，Init，Behavior
自动驾驶车辆拆解：$F_{per} \circ F_{pla} \circ F_{con}$
构建挑战场景：$$\hat{\theta} = \arg \max \mathbb{E}_{x \sim p_{\theta}(x)}[g(F,x)]$$g是测试场景的评价标准
难点在于：
1. $p_\theta(x)$的表示
2. 如何量化评价测试场景

场景的表示方法可以使用动态对象的轨迹或策略模型，策略模型更加灵活但是使用轨迹表示场景更可控

测试场景评价：
- TTC
- 基于距离的指标或基于减速度的指标（紧急事件）
- 安全事件后指标：碰撞率、平均驶出道路距离、违反法规的频率等

对于输入场景的建模十分重要：因为其影响了最后输出的不确定性。
## Data-driven Generation
获得$p_\theta$
**直接采样**
1. 数据回放：从场景库中选择关键场景
	1. [[非齐次泊松描述感兴趣区域中交通系统的风险强度过程模型]]
2. 聚类：从场景中提取基元以实现对相似场景进行聚类
	1. Traffic Primitive：分层狄利克雷过程隐马尔可夫模型
3. 随机噪声：Waymo扰动重要参数重建致命事故
**密度估计**：学习密度模型来近似分布
1. 贝叶斯网络-概率图模型
	1. 动态贝叶斯网络
	2. 因子图 - 多辆车之间的驾驶行为
	3. 重要性采样
	4. 高斯过程 - 模拟连续场景的分布
2. 深度学习
	1. LSTM
	2. CNN + GRU 生成真实的多代理交通场景
3. 深度生成模型 - **CMTS**
	1. GAN
	2. VAE
	3. AR
	4. Flow-based model
	5. Diffusion
4. 模仿学习
## Adversarial Generation
生成器+受害者模型（AV）
$$\hat{\theta} = \arg \max \mathbb{E}_{p_{\theta}(x)}[Q(x,\pi)]$$
对抗生成往往只能针对单一场景，因此需要增加分布的熵$\mathbb{H}(x)$来保证生成场景的多样性。

**静态生成**：往往用于识别和分割

**动态生成**：
1. 初始条件：初始位置或初始速度；直接给出整个轨迹；
	1. 归一化流量模型来学习多模态分布，用真实世界数据分布作为约束
	2. 直接优化现有轨迹，扰动周围车辆的行驶路径
2. 强化学习：
	1. 多代理DDPG控制周围两辆车攻击自我车辆，为交通背景参与者设置辅助目标以避免生成不真实的场景。
	2. 基于约束的优化方法/贝叶斯优化方法
3. 启发式方法
4. 自适应压力测试
5. 生成行人过马路
6. LSTM生成初始条件和每一步动作
## Knowledge-based generation
使用显式知识来指导生成过程，domain knowledge $c \in \mathcal{C}$
$$\hat{\theta} = \arg \max \mathbb{E}_{x \sim p_{\theta}(x|c)}[g(F,x)]$$
还可以使用c作为约束条件处理已有场景：
$$\tilde{x} = \arg \max g(F,x) \qquad s.t. C(x) \geq 0$$

## Challenges and potential solutions 
可移植性、可控性
生成场景和真实场景之间的差距：Kullback-Libler分歧和Wasserstein距离等

**效率**：
代理模型和梯度估计方法
符号表示法可以帮助生成模型推理出使场景具有安全关键性的要素
因果发现方法可以揭示安全关键情景背后的潜在因果关系，找到导致风险的机制

**多样性**：
1. 优化的角度：基于采样的方法，从多种模式中获得可行的方案
2. 对密度估计模型进行正则化处理，或建立多模式分布

**可移植性**：
攻击应发生在组级或语义级。
构建分层场景，高层为风险场景制定计划，底层通过控制执行计划。

**可控性**：
1. 在固定几个参数的情况下重复一个特定的场景
2. 用类似的设置生成不同的场景
条件生成模型
increase the generalizability under such a zero-shot setting

## Conclusion and Discussion
三种推荐的方式：
1. 数据驱动+对抗生成：在不同场景下对系统进行广泛评估。从生成模型中随机抽样，通过对抗生成搜索安全关键场景
2. 数据驱动+基于知识：在特定场景中测试驾驶系统
3. 对抗生成+基于知识

对抗生成的场景往往太过危险，需要讨论如何使用鲁棒性优化和分布式鲁棒性优化来使生成的场景能被有效利用




---
# Extension Papers
