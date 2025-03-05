20241211
Status: #public-knowledge
Tags: 
aliases: 分数函数；score-based model
# Score function
分数函数是对对数概率密度函数$\log p_\theta(x)$的梯度：$$s_\theta(x) = \nabla_x \log p_\theta(x)$$表示分布$p_\theta(x)$在点$x$上的梯度方向，告诉我们应该如何调整$x$以增加其概率密度。

$$s_\theta(\mathbf{x}) = \nabla_\mathbf{x} \log p_\theta(\mathbf{x}) = -\nabla_\mathbf{x} f_\theta(\mathbf{x}) - \underbrace{\nabla_\mathbf{x} \log Z_\theta}_{=0} = -\nabla_\mathbf{x} f_\theta(\mathbf{x}).
$$
基于分数的模型与归一化常数无关！





---
# References
