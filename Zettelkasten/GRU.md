20241213
Status: #methods
Tags: 
aliases: Gated Recurrent Unit
# GRU
![[GRU.png]]
整体的认知和RNN，LSTM一样，都是从理解“传送带”图开始的，整个过程需要有跳过和保留的机制，因此引入Sigmoid激活函数。
先来介绍更新门和重置门。

重置门允许决定保留“可能还想记住”的过去状态，因为经过它的信息最后会和这一时刻输入的信息一起被处理然后输出到下一时刻。
更新门则控制下一时刻的状态中有多少是直接来自于上一时刻的状态，注意这里说的是直接，也就意味着剩下的是经过处理的信息。

两者的计算方式如下：
$$\begin{aligned}
\mathbf{R}_{t}=\sigma(\mathbf{X}_t\mathbf{W}_{xr}+\mathbf{H}_{t-1}\mathbf{W}_{hr}+\mathbf{b}_r),\\\mathbf{Z}_{t}=\sigma(\mathbf{X}_t\mathbf{W}_{xz}+\mathbf{H}_{t-1}\mathbf{W}_{hz}+\mathbf{b}_z),
\end{aligned}$$
使用Sigmoid函数将输入值转换到区间$(0,1)$，因为使用点乘，所以可以理解为门的值接近0就代表不想要这个信息了。

介绍完重置门和更新门以后，再来看GRU对信息的处理方式。
从重置门中出来的数据（直接来自于上一时刻，与输入并没有重叠的部分），和输入合并后，进行常规隐状态更新（Relax，我也不知道这是什么，但是至少不影响我目前的理解，只当它是信息处理就好了）
$$\tilde{\mathbf{H}}_t=\tanh(\mathbf{X}_t\mathbf{W}_{xh}+(\mathbf{R}_t\odot\mathbf{H}_{t-1})\mathbf{W}_{hh}+\mathbf{b}_h),$$
最后，把所有的信息汇总，得到门控循环单元的最终更新公式：
$$\mathbf{H}_t=\mathbf{Z}_t\odot\mathbf{H}_{t-1}+(1-\mathbf{Z}_t)\odot\tilde{\mathbf{H}}_t.$$










---
# References
