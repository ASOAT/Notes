20241206
Status: #methods
Tags: 
aligns: Jensen-Shannon Divergence, JSD
# Jensen-Shannon 散度
衡量两个概率分布之间相似性的一种度量，是KL散度的一种对称化和归一化的版本。

通过计算$P$和$Q$相对于一个中间分布$M(x)$的KL散度来定义：
$$M(x) = \frac{1}{2}P(x) + \frac{1}{2}Q(x)$$
$$Q_{JS}(P||Q) = \frac{1}{2}D_{KL}(P||M) + \frac{1}{2}D_{KL}(Q||M)$$
JS散度是对称的，且$0 \leq D_{JS}(P||Q) \leq \log2$

---
# References
[[Kullback-Leibler 散度]]