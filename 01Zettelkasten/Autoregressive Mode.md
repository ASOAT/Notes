20241202
Status: #methods
Tags: 
# Autoregressive Mode
自回归模型常用于时序分析，一般形式为：
$$X_t=\phi_1X_{t-1}+\phi_2X_{t-2}+\cdots+\phi_pX_{t-p}+\epsilon_t,$$
可以写作：
$$\mathbf{X}=\mathbf{\Phi}\boldsymbol{\phi}+\mathbf{E}$$

有三项参数值得关注：
- p：参数数量，对于模型的拟合精度和过拟合等有影响，需要寻优。
- $\phi_i$：回归系数，自适应模型的直接优化对象。
- $\epsilon_t$：残差，表示无法被预测的随机性，一般被用作评估模型；若$\epsilon_t$为白噪声则说明模型拟合表现优秀。

对于p，一般从AIC（赤池信息准则）/BIC（贝叶斯信息准则）的角度出发：
$$AIC = -2l + 2p$$
其中$l$为模型的最大化似然函数：
- 构造似然函数：$$L(\phi_1,\phi_2,\ldots,\phi_p,\sigma^2|X)=\prod_{t=p+1}^Tf(X_t|X_{t-1},\ldots,X_{t-p}),$$
$$f(X_t|X_{t-1},\ldots,X_{t-p})=\frac{1}{\sqrt{2\pi\sigma^2}}\exp\left(-\frac{(X_t-\sum_{i=1}^p\phi_iX_{t-i})^2}{2\sigma^2}\right).$$
- 对数似然函数：
$$\ell(\phi_1,\phi_2,\ldots,\phi_p,\sigma^2)=-\frac{(T-p)}{2}\ln(2\pi)-\frac{(T-p)}{2}\ln(\sigma^2)-\frac{1}{2\sigma^2}\sum_{t=p+1}^T(X_t-\sum_{i=1}^p\phi_iX_{t-i})^2.$$
- 最大化似然函数：
对数似然函数对$\phi_i$和$\sigma^2$进行求导，使其导数等于0，得到$\phi_i$和$\sigma^2$的估计值。
	- 对于回归系数，最小化平方残差$\sum_{t=p+1}^T(X_t-\sum_{i=1}^p\phi_iX_{t-i})^2$，等价于最小二乘估计。
	- 对于噪声方差：
$$\hat{\sigma}^2=\frac{1}{T-p}\sum_{t=p+1}^T(X_t-\sum_{i=1}^p\hat{\phi}_iX_{t-i})^2.$$
$$BIC = -2l + p\ln(T)$$
其中$T$为样本数量。
观察AIC和BIC不难发现，更大的$l$能更好得降低AIC，即AIC更倾向于拟合更好的模型；更小的$p$能更好地降低BIC，即BIC更倾向于简洁的模型。
当然也可以使用交叉验证的方法。

对于$\phi_i$，优化的方法包括：
- [[Yule-Walker 方法]]
- [[最小二乘估计]]
- [[Burg方法]]



---
# Code
完整的自适应模型伪代码如下：
（包含p的寻找以及参数$\phi$ 的优化）
```python
function AR_Model(data, max_p):
    """
    自回归模型完整过程：
    - 寻找最优阶数 p
    - 优化 AR 模型参数
    - 输出模型拟合结果

    输入：
    - data: 时间序列数据，长度为 T
    - max_p: AR模型的最大阶数候选值

    输出：
    - p: 选择的最优阶数
    - phi: AR(p) 模型的参数向量
    - sigma2: 白噪声方差
    """

    # Step 1: 初始化
    T = length(data)  # 数据长度

    # Step 2: 遍历候选阶数，寻找最优阶数 p
    for p_candidate in range(1, max_p + 1):
		# 计算最大似然估计
        
        # 计算 AIC 和 BIC
        aic = 2 * p_candidate - 2 * log_likelihood
        bic = log(T) * p_candidate - 2 * log_likelihood

    # 选择最优阶数：根据 AIC 或 BIC 最小值
    p_optimal = argmin(aic_values)  # 或 argmin(bic_values)

    # Step 3: 根据最优阶数重新估计 AR 模型参数
    phi_optimal, sigma2_optimal = BurgMethod(data, p_optimal)

    # Step 4: 输出结果
    return p_optimal, phi_optimal, sigma2_optimal
```

---
# References
