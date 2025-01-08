20241206
Status: #methods
Tags: 
aliases: VAE；变分自动编码器
# Variational Autoencoder
找到输入数据$x$ 的潜在空间表示$z$，同时在潜在空间中学习一个先验分布$p(z)$，从而可以通过采样生成与输入数据分布一致的新数据。
![[Variational Autoencoder-1.png]]

![[Variational Autoencoder.png]]

编码器：输出一个正态分布中$q(z|x) \sim \mathcal{N}(\mu, \sigma^2)$
解码器：从潜在变量$z$重构输入数据，建模$p(x|z)$
假设潜在变量$z$的先验分布$p(z)$是一个标准正态分布：$p(z) \sim \mathcal{N}(0,\mathcal{I})$
## # 损失函数
**公式推导：**
$$\begin{aligned}\max L&=\sum_x\log p(x)\\\text{while} \space p(x)&=\int_zp(z)p(x|z)dz\end{aligned}$$
对于上述公式，将编码器$q(z|x)$加入，通过推导得到损失函数的定义
$$\begin{aligned}\log p(x)&=\int_zq(z|x)\log p(x)dz\\&=\int_zq(z|x)\log(\frac{p(z,x)}{p(z|x)})dz=\int_zq(z|x)\log(\frac{p(z,x)}{q(z|x)}\frac{q(z|x)}{p(z|x)})dz\\&=\underbrace{\int_zq(z|x)\log(\frac{p(z,x)}{q(z|x)})dz}_{lower\mathrm{~bound~L}_b}+\underbrace{\int_zq(z|x)\log(\frac{q(z|x)}{p(z|x)})dz}_{KL(q(z|x)||p(z|x)\geq0}\\&\geq\underbrace{\int_zq(z|x)\log(\frac{p(x|z)p(z)}{q(z|x)})dz}_{lower\mathrm{bound~L}_b}\end{aligned}$$
$$\begin{aligned}&\log p(x)=\{L_b+KL(q(z|x)||p(z|x))\}\leq0\\
&KL(q(z|x)||p(z|x)) \geq 0\\
&L_b=\int_zq(z|x)\log(\frac{p(x|z)p(z)}{q(z|x)})dz\leq0\end{aligned}$$
可以发现，我们只关注lower bound，这也是VAE常被成为ELBO的原因，继续分解$L_b$得到：
$$\begin{aligned}L_{b}&=\int q(z|x)\log(\frac{p(z,x)}{q(z|x)})dz=\int q(z|x)\log(\frac{p(x|z)p(z)}{q(z|x)})dz\\&=\underbrace{\int q(z|x)\log(\frac{p(z)}{q(z|x)})dz}_{-KL(q(z|x)||p(z))}+\int q(z|x)\log p(x|z)dz\end{aligned}$$


**重构误差**
重构输入数据的质量
$$L_{reconstruction} = - \mathbb{E}_{q(z|x)}[\log p(x|z)]$$
这一项表示在编码器编码后重新得到观测值$x$的概率，越大越好。

或者使用均方误差MSE（连续数据），二元交叉熵BCE（离散数据）
**KL散度**
衡量编码器输出的潜在分布$q(z|x)$与先验分布$p(z)$的差异：
$$\mathcal{L}_{\text{KL-divergence}}=D_{\mathrm{KL}}(q(z|x)\|p(z))$$
$$D_\mathrm{KL}(q(z|x)\|p(z))=\int q(z|x)\log\frac{q(z|x)}{p(z)}dz$$
在正态分布假设下，可以简化为：
$$D_{\mathrm{KL}}(q(z|x)\|p(z))=-\frac{1}{2}\sum_{i=1}^d\left(1+\log(\sigma_i^2)-\mu_i^2-\sigma_i^2\right)$$
## # 训练过程
**调整Encoder:**
因为第二项包含了Decoder有关的内容，因此在实际训练中通常调整$q(z|x)$使KL散度减小，同时这也意味着$q(z|x)$在接近$p(z)$

**调整Decoder：**
调整$p(x|z)$只对重构误差生效



损失函数中的期望项涉及了采样，因此不能反向传播梯度，引入重新参数化的技巧：
$$z = \mu + \epsilon \cdot \sigma, \epsilon \sim \mathcal{N}(0,I)$$
$\epsilon$为一个辅助的独立随机变量。


---
# References
[[Autoencoder]]
[[Kullback-Leibler 散度]]