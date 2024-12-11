20241206
Status: #methods
Tags: 
aligns: VAE；变分自动编码器
# Variational Autoencoder
找到输入数据$x$ 的潜在空间表示$z$，同时在潜在空间中学习一个先验分布$p(z)$，从而可以通过采样生成与输入数据分布一致的新数据。

![[Variational Autoencoder.png]]

编码器：输出一个正态分布中$q(z|x) \sim \mathcal{N}(\mu, \sigma^2)$
解码器：从潜在变量$z$重构输入数据，建模$p(x|z)$
假设潜在变量$z$的先验分布$p(z)$是一个标准正态分布：$p(z) \sim \mathcal{N}(0,\mathcal{I})$
## # 损失函数
**重构误差**
重构输入数据的质量
$$L_{reconstruction} = - \mathbb{E}_{q(z|x)}[\log p(x|z)]$$
或者使用均方误差MSE（连续数据），二元交叉熵BCE（离散数据）

**KL散度**
衡量编码器输出的潜在分布$q(z|x)$与先验分布$p(z)$的差异：
$$\mathcal{L}_{\text{KL-divergence}}=D_{\mathrm{KL}}(q(z|x)\|p(z))$$
$$D_\mathrm{KL}(q(z|x)\|p(z))=\int q(z|x)\log\frac{q(z|x)}{p(z)}dz$$
在正态分布假设下，可以简化为：
$$D_{\mathrm{KL}}(q(z|x)\|p(z))=-\frac{1}{2}\sum_{i=1}^d\left(1+\log(\sigma_i^2)-\mu_i^2-\sigma_i^2\right)$$
## # 训练过程
损失函数中的期望项涉及了采样，因此不能反向传播梯度，引入重新参数化的技巧：
$$z = \mu + \epsilon \cdot \sigma, \epsilon \sim \mathcal{N}(0,I)$$
$\epsilon$为一个辅助的独立随机变量。


---
# References
[[Autoencoder]]
[[Kullback-Leibler 散度]]