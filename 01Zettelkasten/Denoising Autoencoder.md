20241206
Status: #methods
Tags: 
aliases: DAE，去噪自动编码器
# Denoising Autoencoder
避免过拟合和提高鲁棒性

![[Denoising Autoencoder.png]]

在输入向量中添加噪声或以随机的方式掩盖一些数值，输入被部分破坏：
$$\begin{aligned}
\mathbf{\tilde{x}}^{(i)} & \sim\mathcal{M}_{\mathcal{D}}(\tilde{\mathbf{x}}^{(i)}|\mathbf{x}^{(i)}) \\
L_{\mathrm{DAE}}(\theta,\phi) & =\frac{1}{n}\sum_{i=1}^n(\mathbf{x}^{(i)}-f_\theta(g_\phi(\tilde{\mathbf{x}}^{(i)})))^2
\end{aligned}$$



---
# References
[[Autoencoder]]