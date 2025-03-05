20241206
Status: #public-knowledge
Tags: [[Generative Model]]
aliases: GAN, 对抗生成网络
# Generative adversarial Network
GAN由两个模型组成：
- 判别器D估计给定样本来自真实数据集的概率。它作为一个分类器，并经过优化以区分假样本和真实样本。
- 生成器G在给定噪声变量z输入的情况下输出合成样本(z带来潜在的输出多样性）。它被训练来捕捉真实的数据分布，因此它的生成样本可以尽可能真实，或者换句话说，可以欺骗判别器以提供高概率。

训练过程中，判别器需要保证自己验钞能力是准确的（对真实数据$p_r$的估计是准确的），$D(x)$对真实样本$x$输出接近1.
同时还需要努力识别生成器G生成的”假钞“，$D(x)$对生成样本$G(z)$输出接近0.
生成器G则努力生产更逼真的”假钞“来欺骗判别器D，$D(G(z))$输出接近1.

得到以下损失函数：
$$\begin{aligned}
\min_G \max_D L(D,G) &= \mathbb{E}_{x \sim p_r(x)}[\log D(x)] + \mathbb{E}_{z \sim p_z(z)}[\log (1-D(G(z)))]\\
\end{aligned}$$
$$L(G,D) = \int_x \Big(p_r(x) \log(D(x)) + p_g(x)\log(1-D(x)\Big)dx$$
对积分中的内容求导：
$$\frac{dL(G,D)}{dD(x)} = p_r(x)\frac{1}{D(x)} - p_g(x)\frac{1}{1-D(x)} = \frac{p_r - (p_r + p_g)D(x)}{D(x)(1-D(x)}$$
令该项等于0，得到：
$$D^*(x) = \frac{p_r}{p_r + p_g}$$
当生成器被训练到最佳状态后，$p_r = p_g$，此时$D^*(x) = \frac{1}{2}$，判别器难以区分生成的样本和真实的样本。

$p_r$和$p_g$的JS散度可以计算为：
$$\begin{aligned}
D_{JS}(p_{r}\|p_{g})= & \frac{1}{2}D_{KL}(p_{r}||\frac{p_{r}+p_{g}}{2})+\frac{1}{2}D_{KL}(p_{g}||\frac{p_{r}+p_{g}}{2}) \\
= & \frac{1}{2}\left(\log2+\int_{x}p_{r}(x)\log\frac{p_{r}(x)}{p_{r}+p_{g}(x)}dx\right)+ \\
 & 
\begin{aligned}
\frac{1}{2}\left(\log2+\int_xp_g(x)\log\frac{p_g(x)}{p_r+p_g(x)}dx\right)
\end{aligned} \\
= & \frac{1}{2}\left(\log4+L(G,D^{*})\right)
\end{aligned}$$
因此可以看出GAN的损失函数量化了生成数据分布和真实样本分布之间的相似性：$$L(G,D^*) = 2D_{JS}(p_r || p_g) - 2\log2$$
## GAN存在的问题
1. 难以达到纳什均衡：D和G都在不断更新，会引起巨大的振荡
2. 如果判别器表现不佳则生成器没有准确的反馈，制造假钞的人随便糊弄都能骗过警察，导致手艺不精；如果判别器做的太好，则损失函数的梯度快速下降到接近于0，警察一眼就看出假钞，制造假钞的人没有生存空间。
3. 缺少可以告知我们训练进度的函数，没有一个好的评估指标。

---
# References
[[Jensen-Shannon 散度]]
