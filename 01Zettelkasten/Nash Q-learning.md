20250218
Status: #public-knowledge
Tags: [[博弈论]] ；[[多智能体强化学习]]
aliases: 
# Nash Q-learning
拓展 Q-learning，应用于多智能体，目标是每个智能体在学习过程中不仅要考虑自己的奖励，还要预测其他智能体的策略对自己策略的影响。

Q 值的更新基于纳什均衡，更新公式为：
$$
Q_i(s, a_1, a_2, …, a_n) \leftarrow (1 - \alpha) Q_i(s, a_1, a_2, …, a_n) + \alpha [r_i + \gamma V_i(s’)]
$$
其中价值函数由当前 Q 值和策略组合确定：
$$
V_i(s) = \text{Nash equilibrium}(Q_i(s, a_1, a_2, \dots, a_n))
$$










---
# References
[[Q-learning]]