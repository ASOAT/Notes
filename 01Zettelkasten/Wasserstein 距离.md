20241206
Status: #methods
Tags: [[最优运输问题]]
aliases: Earth Mover's Distance
# Wasserstein 距离
可以被直观地理解为将一堆土从一个概率分布重新分布到另一个概率分布所需的最小搬运成本。

Wasserstein的目标在于寻找一个最优的”搬运计划“$\gamma(x, y) \in \Pi (P,Q)$，其中$\Pi(P,Q)$是所有可能的联合分布集合，满足边际分布为P和Q。

$$W(P,Q) = \min_{\gamma \in \Pi(P,Q)} \sum_{i,j} \gamma_{i,j} \cdot |x_i,y_j|$$
具有对称性，且是真正的距离度量，满足三角不等式。

当两个分布不相交时$D_{KL}$为无穷大，$D_{JS}$会有突然跳跃。
即使两个分布位于没有重叠的低维流形中，Wasserstein距离仍然可以提供有意义且平滑的中间距离表示。
## # 对偶性处理
由于联合分布十分复杂，下文提出一种基于Kortorovich对偶性的处理方法，转换成$f(x)$的优化问题

对于联合分布$\gamma(x,y)$，存在边际约束：
$$\int_\mathcal{Y}\gamma(x,y)dy = P(x), \int_\mathcal{X}\gamma(x,y)dx = Q(y)$$为了处理边际约束，引入拉格朗日乘子：
$$\begin{aligned}
\mathcal{L}(\gamma,\phi,\psi)=\int_{\mathcal{X}\times\mathcal{Y}}d(x,y)\left.\gamma(x,y)\right.dx\left.dy+\int_{\mathcal{X}}\phi(x)\left(P(x)-\int_{\mathcal{Y}}\gamma(x,y)\right.dy\right)dx+
\\\int_{\mathcal{Y}}\psi(y)\left(Q(y)-\int_{\mathcal{X}}\gamma(x,y)dx\right)dy
\end{aligned}
$$
合并积分项，得到：
$$\mathcal{L}(\gamma,\phi,\psi)=\int_{x\times y}\left(d(x,y)-\phi(x)-\psi(y)\right)\gamma(x,y)dxdy+\int_x\phi(x)P(x)dx+\int_y\psi(y)Q(y)dy$$

对$\gamma(x,y)$求最小值，必须保证函数有下界，若$\gamma(x,y)$前的项小于零，下界为负无穷，因此必须满足：
$$d(x,y)\geq\phi(x)+\psi(y),\quad\forall x,y$$
对于外层优化，得到对偶形式：
$$W(P,Q)=\sup_{\phi,\psi}\int_{\mathcal{X}}\phi(x)P(x)dx+\int_{\mathcal{Y}}\psi(y)Q(y)dy$$
同时需满足约束：
$$\phi(x)+\psi(y) \leq d(x,y),\quad\forall x,y$$

引入单一变量$f(x)$:
$$f(x) = \phi(x), \psi(y) = -\sup_x\{f(x) - d(x,y)\}$$
#有问题

---
# References
[[联合分布集合]]
[[拉格朗日方法]]
