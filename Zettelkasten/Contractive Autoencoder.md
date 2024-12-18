20241206
Status: #methods
Tags: 
aliases: 收缩自动编码器
# Contractive Autoencoder
与系数自动编码器类似，鼓励学习到的表示停留在收缩空间中，以获得更好的鲁棒性。

惩罚隐藏层对输入的梯度，从而约束潜在表示的变化范围。
$$\mathcal{R} = \|J_f(\mathbf{x})\|_F^2=\sum_{ij}\left(\frac{\partial h_j(\mathbf{x})}{\partial x_i}\right)^2$$
总的损失函数为：
$$\mathcal{L}=\mathcal{L}_{\text{reconstruction}}+\lambda\cdot\mathcal{R}$$



---
# References
[[Autoencoder]]