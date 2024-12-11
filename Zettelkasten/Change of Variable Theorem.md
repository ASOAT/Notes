20241211
Status: #methods
Tags: 
aligns: 变量替换定理
# Change of Variable Theorem
推断变量替换后的概率密度函数$p(x)$。

给定一个随机变量及其已知的概率密度函数$z \sim \pi(z)$，使用单射函数$x = f(z)$来构造一个新的随机变量，该函数是可逆的，所以$z = f^{-1}(x)$。
根据概率分布的定义有：
$$\int p(x)dx = \int \pi(z)dz = 1$$
$$p(x) = \pi(z) \left|\frac{dz}{dx}\right|=\pi(f^{-1}(x)) \left| \frac{d f^{-1}}{dx} \right| = \pi(f^{-1}(x)) \left| (f^{-1})'(x) \right|
$$
多变量版本有类似的表达方式：
$$\begin{gathered}
\mathbf{z} \sim \pi(\mathbf{z}), \, \mathbf{x} = f(\mathbf{z}), \, \mathbf{z} = f^{-1}(\mathbf{x})
\\
p(\mathbf{x}) = \pi(\mathbf{z}) \left| \det \frac{d\mathbf{z}}{d\mathbf{x}} \right| = \pi(f^{-1}(\mathbf{x})) \left| \det \frac{df^{-1}}{d\mathbf{x}} \right|
\end{gathered}
$$
其中$\displaystyle \det \frac{d \textbf{f}^{-1}}{d \textbf{x}}$是函数$f$的雅可比矩阵行列式。




---
# References
