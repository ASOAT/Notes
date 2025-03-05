20241206
Status: #public-knowledge
Tags: 
aliases: 
# Wasserstein GAN
在原始的GAN中，判别器输出的时数据为真实数据的概率，而在WGAN中，判别器（Critic）的输出变为一个分数，表示生成数据和真实数据之间的差异。

WGAN的损失函数为：
$$L = \mathbb{E}_{x \sim P_{data}}[D(x)] - \mathbb{E}_{z \sim P_z}[D(G(z))]$$

使用Wasserstein距离代替原始GAN的JS散度，使：
- 即使生成分布$P_G$和真实分布$P_{data}$没有重叠，损失函数仍然有梯度，避免了梯度消失问题。
- Wasserstein距离是连续且可微的，这让生成器能够更稳定地优化。

传统GAN的判别器被替换成Critic，用于估计Wasserstein距离，Critic的输出越大，表示样本越接近真实分布。
1-Lipschitz 条件限制了 Critic 的梯度，确保其变化速度受控。这种平滑性对于 GAN 的训练至关重要，如果 Critic 的梯度变化过大，会导致生成器优化过程中出现剧烈震荡，影响训练稳定性。
1-Lipschitz 条件还确保 Critic 始终有意义的梯度，使生成器能够获得平滑且稳定的更新信号。

为了保证Critic满足1-Lipschitz条件，WGAN提出两种实现方式：
1. 权重剪切：
	更新Critic参数后，将其权重限制在一个固定范围内
2. 梯度惩罚**WGAN-GP**（Gradient Penalty）
	损失函数中加入梯度惩罚项：
	$$L_D=\mathbb{E}_{x\sim P}[D(x)]-\mathbb{E}_{x\sim G(z)}[D(G(z))]+\lambda\mathbb{E}_{\hat{x}}[(\|\nabla_{\hat{x}}D(\hat{x})\|_2-1)^2]$$

---
# References
[[Generative adversarial Network]]
[[Wasserstein 距离]]
[[K-Lipschitz]]