20241211
Status: #methods
Tags: 
aliases: 
# Gaussian Process Regression
给定一个训练集$\mathcal{D}=\{(x_i,y_i)\}^n_{i=1}$，其中：
- $x_i$是输入点
- $y_i$是带噪声的观测值，满足$y_i=f(x_i)+\epsilon$，噪声$\epsilon \sim \mathcal{N}(0,\sigma_n^2)$

训练点的观测值$\mathbf{y}=[y_1,\dots,y_n]^\top$与预测点的函数值$f_*$的联合分布式多元高斯分布：
$$\begin{bmatrix}
\mathbf{y} \\
f_*
\end{bmatrix}
\sim \mathcal{N} \left(
\begin{bmatrix}
\mathbf{m} \\
m(x_*)
\end{bmatrix},
\begin{bmatrix}
\mathbf{K} + \sigma_n^2 \mathbf{I} & \mathbf{k}_* \\
\mathbf{k}_*^\top & k(x_*, x_*)
\end{bmatrix}
\right),
$$
其中：
- $\mathbf{K}$是训练点之间的协方差矩阵，使用核函数
- $\mathbf{k}_*$是预测点与训练点之间的协方差向量；
- $k(x_*,x_*)$是预测点的自身协方差

根据高斯分布的条件分布性质，预测点$x_*$的函数值$f_*$的分布为：
$$p(f_*|x_*,\mathcal{D})=\mathcal{N}(\mu_*,\sigma_*^2)$$
其中：
$$\mu_* = \mathbf{k}_*^\top(\mathbf{K}+\sigma_n^2\mathbf{I})^{-1}\mathbf{y}$$
是预测点的回归值，主要由训练点的观测值和相关性决定
$$\sigma_*^2 = k(x_*,x_*)-\mathbf{k}_*^\top(\mathbf{K}+\sigma_n^2\mathbf{I})^{-1}\mathbf{k}_*$$
是预测的不确定性，随着预测点原理训练点而增大。

使用预测点后验分布的期望来作为函数值的预测值。

## 训练
通过最大对数化边际似然$\log p(\mathbf{y})$来优化核函数的超参数

首先回顾多元高斯分布的概率密度函数：
$$p(\mathbf{y}) = \frac{1}{(2\pi)^{n/2} |\Sigma|^{1/2}} 
\exp\left( -\frac{1}{2} (\mathbf{y} - \boldsymbol{\mu})^\top \Sigma^{-1} (\mathbf{y} - \boldsymbol{\mu}) \right)
$$
在高斯过程回归中：
- 均值向量$\mathbf{\mu}=0$，目的在于：
	- 简化模型，将重点放在核函数的选择和优化上
	- 如果数据的真实均值偏离零，核函数通过调整其形式核参数可以捕捉到这种偏移，以RBF核为例，可以通过幅度$\sigma_f^2$。
- 协方差矩阵$\sum = \mathbf{K} + \sigma_n^2 \mathbf{I}$

得到观测数据的概率密度函数：
$$p(\mathbf{y}) = \frac{1}{(2\pi)^{n/2} |\mathbf{K} + \sigma_n^2 \mathbf{I}|^{1/2}} 
\exp\left( -\frac{1}{2} \mathbf{y}^\top (\mathbf{K} + \sigma_n^2 \mathbf{I})^{-1} \mathbf{y} \right)$$
取对数后，公式变为：
$$\log p(\mathbf{y}) = 
-\frac{1}{2} \mathbf{y}^\top (\mathbf{K} + \sigma_n^2 \mathbf{I})^{-1} \mathbf{y}
- \frac{1}{2} \log |\mathbf{K} + \sigma_n^2 \mathbf{I}|
- \frac{n}{2} \log(2\pi).
$$
将其分为三项：
1. 数据拟合项：$$-\frac{1}{2} \mathbf{y}^\top (\mathbf{K} + \sigma_n^2 \mathbf{I})^{-1} \mathbf{y}$$表示观测数据$\mathbf{y}$与高斯过程模型的拟合程度。
2. 复杂度惩罚项：$$- \frac{1}{2} \log |\mathbf{K} + \sigma_n^2 \mathbf{I}|$$表示协方差矩阵的复杂性（这个是行列式）
3. 常数项：与模型参数无关，忽略
### 梯度推导
为优化核函数参数$\mathbf{\theta}$，需要计算边际似然对$\boldsymbol{\theta}$的梯度：
对于第一项：
$$\frac{\partial}{\partial \boldsymbol{\theta}} 
\left( \mathbf{y}^\top (\mathbf{K} + \sigma_n^2 \mathbf{I})^{-1} \mathbf{y} \right) 
= - \mathbf{y}^\top (\mathbf{K} + \sigma_n^2 \mathbf{I})^{-1} 
\frac{\partial \mathbf{K}}{\partial \boldsymbol{\theta}} 
(\mathbf{K} + \sigma_n^2 \mathbf{I})^{-1} \mathbf{y}.
$$
对于第二项，利用行列式性质：
$$\frac{\partial}{\partial \boldsymbol{\theta}} 
\left( -\frac{1}{2} \log |\mathbf{K} + \sigma_n^2 \mathbf{I}| \right) 
= -\frac{1}{2} \operatorname{tr} \left( (\mathbf{K} + \sigma_n^2 \mathbf{I})^{-1} 
\frac{\partial \mathbf{K}}{\partial \boldsymbol{\theta}} \right).
$$
得到总体梯度：
$$\frac{\partial \log p(\mathbf{y} \mid \mathbf{X}, \boldsymbol{\theta}, \sigma_n^2)}{\partial \boldsymbol{\theta}}
= \frac{1}{2} \mathbf{y}^\top (\mathbf{K} + \sigma_n^2 \mathbf{I})^{-1} 
\frac{\partial \mathbf{K}}{\partial \boldsymbol{\theta}} 
(\mathbf{K} + \sigma_n^2 \mathbf{I})^{-1} \mathbf{y}
- \frac{1}{2} \operatorname{tr} \left( (\mathbf{K} + \sigma_n^2 \mathbf{I})^{-1} 
\frac{\partial \mathbf{K}}{\partial \boldsymbol{\theta}} \right).
$$


---
# References
[[Gaussian Process]]
[[Kernel Function]]
