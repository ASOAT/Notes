20241206
Status: #public-knowledge
Tags: 
aliases: Kullback-Leibler Divergence
# Kullback-Leibler散度
衡量两个概率分布之间的“差异”或“距离”。
直观上，$D_{KL}(P||Q)$表示的使一个分布$Q(x)$（实际使用的分布）相对于另一个分布$P(x)$（真实分布）的信息损失，是一种有方向性的差异（即$D_{KL}(P||Q) \neq D_{KL}(Q||P)$）。

KL散度表示为交叉熵$H(P,Q)$和熵$H(P)$之间的差值：
$$D_{KL}(P||Q) = - \sum_x P(x)\log Q(x) + \sum_x P(x)\log P(x) = \sum_x P(x) \log \frac{P(x)}{Q(x)}$$
它表示用$Q(x)$来描述$P(x)$需要的额外信息量

显然，KL 是不对称的，当我们想要测量两个同样重要的分布之间的相似性时，它可能会导致错误的结果。

---
# References
[[熵&交叉熵]]
