20241211
Status: #public-knowledge
Tags: 
aliases: 
# Normalizing Flows
由于需要在深度学习模型中运行反向传播，因此我们希望后验概率$p(\textbf{z}|\textbf{x})$可以简单有效地计算出导数。Normalizing Flows模型通过一连串的可逆变换函数将一个简单的分布转变成一个复杂的分布，根据变量替换定理反复用新的变量来替代，最终得到目标变量的概率分布。

![[Normalizing Flows.png]]
$$\begin{gather}
\mathbf{z}_{i-1} \sim p_{i-1}(\mathbf{z}_{i-1}) \\

\mathbf{z}_i = f_i(\mathbf{z}_{i-1}), \, \text{因此} \, \mathbf{z}_{i-1} = f_i^{-1}(\mathbf{z}_i) \\

p_i(\mathbf{z}_i) = p_{i-1}(f_i^{-1}(\mathbf{z}_i)) \left| \det \frac{d f_i^{-1}}{d\mathbf{z}_i} \right|

\end{gather}$$
根据反函数和雅可比矩阵的性质，可以推出：
$$p_i(\mathbf{z}_i) = p_{i-1}(\mathbf{z}_{i-1})\left|\det \frac{d f_i}{d \mathbf{z}_{i-1}}\right|^{-1}$$$$\log p_i(\mathbf{z}_i) = \log p_{i-1}(\mathbf{z}_{i-1}) - \log \left|\det \frac{d f_i}{d \mathbf{z}_{i-1}}\right|$$
$\displaystyle -\log \left|\det \frac{d f_i}{d \mathbf{z}_{i-1}}\right|$项体现了变换函数$f$对密度的缩放影响。
当我们知道每一对连续变量之间的关系，就可以展开输出$\mathbf{x}$的方程，追溯到初始分布$\mathbf{z_0}$：
$$\begin{aligned}
\mathbf{x} = \mathbf{z}_K &= f_K \circ f_{K-1} \circ \cdots \circ f_1(\mathbf{z}_0) \\

\log p(\mathbf{x}) = \log \pi_K(\mathbf{z}_K) 
&= \log \pi_{K-1}(\mathbf{z}_{K-1}) - \log \left| \det \frac{d f_K}{d \mathbf{z}_{K-1}} \right| \\ 
&= \log \pi_{K-2}(\mathbf{z}_{K-2}) - \log \left| \det \frac{d f_{K-1}}{d \mathbf{z}_{K-2}} \right| - \log \left| \det \frac{d f_K}{d \mathbf{z}_{K-1}} \right| \\
&= \cdots \\
&= \log \pi_0(\mathbf{z}_0) - \sum_{i=1}^K \log \left| \det \frac{d f_i}{d \mathbf{z}_{i-1}} \right|

\end{aligned}$$

有了归一化流，就可以通过调整变换函数$f$的参数，使对数似然函数最大化，换言之，训练标准为训练数据集$\mathcal{D}$上的负对数似然：
$$\mathcal{L}(\mathcal{D}) = -\frac{1}{|\mathcal{D}|} \sum_{\mathbf{x} \in \mathcal{D}} \log p(\mathbf{x})
$$


---
# References
[[Change of Variable Theorem]]
[[Inverse Function Theorem]]
