20241211
Status: #methods
Tags: 
aliases: 
# Gaussian Process
高斯过程可以理解为一个无限维的高斯分布，能够描述一个函数$f(x)$在每个输入点$x$的所有可能值的分布。
高斯过程的数学定义为：
$$f(x) \sim \mathcal{GP}(m(x), k(x, x'))
$$
- $m(x) = \mathbb{E}[f(x)]$是均值函数，表示函数在$x$处的期望值。
- $k(x',x)=Cov(f(x),f(x'))$是核函数，表示$f(x)$和$f(x')$的相关性。

高斯过程定义：
$$[f(x_1), f(x_2), \ldots, f(x_n)] \sim \mathcal{N}(\mathbf{m}, \mathbf{K})
$$
其中：
- 均值$\textbf{m} = [m(x_1),m(x_2),\dots,m(x_n)]^T$
- 协方差矩阵$\mathbf{K}$的元素$K_{ij}=k(x_i,x_j)$





---
# References
[[高斯分布]]
