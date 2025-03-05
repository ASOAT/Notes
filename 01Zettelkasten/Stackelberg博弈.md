20250216
Status: #public-knowledge
Tags: [[博弈论]]
aliases: 
# Stackelberg博弈
描述领导者与追随者之间的互动，特点为一个玩家（Leader）先选择自己的策略，另一个玩家（Follower）根据领导者的选择来反映并选择自己的策略。

假设领导者选择策略 $s_L$ 后，跟随者会选择使其收益最大化的策略 $s_{F}^*(s_{L})$。

假设领导者的收益函数为 $u_L(s_{L},s_{F})$, 可以写为：$$
\max_{s_{L}} u_{L} (s_{L}, s_{F}^*(s_{L}))
$$
其中跟随者的最优回应策略为：
$$
s_{F}^*(s_{L}) = \arg \max_{s_{F}} u_{F}(s_{L}, s_{F})
$$










---
# References
[Title Unavailable \| Site Unreachable](https://zhuanlan.zhihu.com/p/662019174)

求解：[[迭代最优回应法]]
