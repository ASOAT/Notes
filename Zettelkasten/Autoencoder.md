20241206
Status: #methods
Tags: 
aligns: 
# Autoencoder
以无监督的方式学习一个恒等函数，以重建原始输入，并在这个过程中压缩数据，从而发现一个更有效和压缩的表示。

![[Autoencoder.png]]

该模型包含一个以$\phi$为参数的编码器函数$g(\cdot)$和一个以$\theta$为参数的解码器函数$f(\cdot)$，瓶颈层输入$\textbf{x}$的低维编码$\textbf{z}=g_\phi(\textbf{x})$，重建的输入式$\textbf{x}' = f_\theta(g_\phi(\textbf{x}))$.

参数$(\theta,\phi)$一起学习，输出一个与原始输入相同的重建数据样，$\textbf{x} \approx f_\theta(g_\phi(\textbf{x}))$。

量化两个向量之间的差异可以使用交叉熵（激活函数为sigmoid）或者简单的MSE损失。
$$L_{\mathrm{AE}}(\theta,\phi)=\frac{1}{n}\sum_{i=1}^{n}(\mathbf{x}^{(i)}-f_{\theta}(g_{\phi}(\mathbf{x}^{(i)})))^{2}$$

---
# References
