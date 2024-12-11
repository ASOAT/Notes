20241203
Status: #methods
Tags: 
# Importance Sampling
对于一般分布求期望值：
$$\mathbb{E}[f(x)] = \int f(x) p(x) dx$$
当$p(x)$采样困难（稀疏事件或复杂分布等）时，选择一个重要性分布$q(x)$使期望变为：
$$\mathbb{E}[f(x)] = \int f(x) \frac{p(x)}{q(x)}dx$$
其中，$\omega = \frac{p(x)}{q(x)}$被称为重要性权重，估计期望为：
$$\mathbb{E}[f(X)] = \sum_{i=1}^N f(x_i)\omega_i,\qquad x_i \sim q(x)$$
$q(x)$满足：
$$q(x)\in[0,1],\sum_{x\in\mathbb{X}}q(x)=1,p(x)>0\Rightarrow q(x)>0.$$

---
# References
