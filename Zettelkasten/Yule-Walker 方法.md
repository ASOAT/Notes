20241202
Status: #methods
Tags: [[Autoregressive Mode]]
# Yule-Walker 方法
对于一般的自回归模型，有：
$$X_t=\phi_1X_{t-1}+\phi_2X_{t-2}+\cdots+\phi_pX_{t-p}+\epsilon_t$$
假设**时间序列是平稳的**（$\mu = 0$），模型的[[自相关函数]]满足：
$$r_k = \mathbb{E}[X_tX_{t-k}]$$
**Proof:**
在时序分析中，自相关函数通常通过样本数据估计：
$$r_k = \frac{\mathbb{E}[(X_t - \bar{X})(X_{t-k} - \bar{X})]}{\sqrt{Var(X_t)Var(X_{t-k})}}$$
因为$Var(X_t) = Var(X_{t-k})$，且都为常数，由于时间序列是**平稳的**，$\bar{X} = 0$，所以$r_k$可以简化为：
$$r_k = \mathbb{E}[X_tX_{t-k}]$$
## Yule-Walker 方程推导
有了上述的自相关函数以后，就可以进行Yule-Walker方程的推导了，首先观察自回归模型函数：$$X_t=\phi_1X_{t-1}+\phi_2X_{t-2}+\cdots+\phi_pX_{t-p}+\epsilon_t$$
对两边同乘$X_{t-k}$后求期望，得到：
$$\mathbb{E}[X_tX_{t-k}] = \phi_1\mathbb{E}[X_{t-1}X_{t-k}] + \phi_2 \mathbb{E}[X_{t-2}X_{t-k}] + \cdots + \phi_p \mathbb{E}[X_{t-p}X_{t-k}] + \mathbb{E}[\epsilon_tX_{t-k}]$$
其中由于$\mathbb{E}[\epsilon_t] = 0$，而其他期望项可以写作$r_i$，因此可以将其整理为：
$$r_k =\phi_1 r_{k-1} + \cdots + \phi_p r_{k-p}$$
对于滞后$k = 0, 1, \dots, p$，上式可以整理为矩阵形式：
$$
\begin{bmatrix}
r_1 \\
r_2 \\
\vdots \\
r_p
\end{bmatrix}=
\begin{bmatrix}
r_0 & r_1 & \cdots & r_{p-1} \\
r_1 & r_0 & \cdots & r_{p-2} \\
\vdots & \vdots & \ddots & \vdots \\
r_{p-1} & r_{p-2} & \cdots & r_0
\end{bmatrix}
\begin{bmatrix}
\phi_1 \\
\phi_2 \\
\vdots \\
\phi_p
\end{bmatrix}.$$
记$\textbf{R}$为$p \times p$的自相关矩阵，可以写作：
$$\textbf{r} = \textbf{R} \cdot \boldsymbol{\phi}$$
求解得到回归系数：
$$\boldsymbol{\phi} = \textbf{R}^{-1} \textbf{r}$$

---
# References
