20241212
Status: #public-knowledge
Tags: [[Kernel Function]]
aliases: 
# Matern核
$$k(x, x') = \frac{2^{1-\nu}}{\Gamma(\nu)} 
\left( \sqrt{2\nu} \frac{\|x - x'\|}{\ell} \right)^\nu 
K_\nu \left( \sqrt{2\nu} \frac{\|x - x'\|}{\ell} \right)
$$
- $\ell$：长度尺度
- $\nu$：平滑性参数
- $K_\nu$：第$\nu$阶的修正贝塞尔函数
- 适用于不平滑函数，$\nu=0.5$是绝对指数核，$\nu \rightarrow \infty$收敛为高斯核





---
# References
