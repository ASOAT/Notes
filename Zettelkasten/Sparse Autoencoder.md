20241206
Status: #methods
Tags: 
aligns: 
# Sparse Autoencoder
添加稀疏性正则化项，限制潜在空间中激活的神经元数量，从而学习到更有意义的特征

假设在隐藏层$l$中有$s_l$个神经元，该层中$j$的神经元的激活函数被标记为$a_j^l(\cdot),j=1,\cdots,s_l$。这个神经元$\hat{\rho}_j$的激活部分预计是一个小数$\rho$，称为稀疏系数；常见的配置是$\rho = 0.05$
$$\hat{\rho}_j^{(l)}=\frac{1}{n}\sum_{i=1}^{n}[a_j^{(l)}(\mathbf{x}^{(i)})]\approx\rho$$
损失函数形式：
$$\mathcal{L}=\mathcal{L}_{\text{reconstruction}}+\lambda\cdot\mathcal{L}_{\mathrm{sparsity}}$$
其中$\lambda$为稀疏正则化项的权重
$\mathcal{L}_{sparsity}$表示稀疏性约束项，常见有：
1. KL散度：$$\mathcal{L}_{\mathrm{sparsity}}=\sum_{j=1}^h\mathrm{KL}(\rho||\hat{\rho}_j)$$
2. L1正则化：$$\mathcal{L}_{\mathrm{sparsity}}=\|z\|_1=\sum_{i=1}^n|z_i|$$



---
# References
[[Autoencoder]]