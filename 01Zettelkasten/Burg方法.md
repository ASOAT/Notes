20241202
Status: #public-knowledge
Tags: 
# Burg方法
Burg方法的核心在于使用反射系数迭代更新参数：
$$\phi_i^{(k)}=
\begin{cases}
\phi_i^{(k-1)}+\kappa_k\phi_{k-i+1}^{(k-1)}, & \mathrm{for}i=1,2,\ldots,k-1, \\
\kappa_k, & \mathrm{for}i=k. & 
\end{cases}$$
## 反射系数求解
定义**前向预测误差**，用以表示滞后$k$个值预测当前值的误差：
$$f_t^{(k)}=X_t-\sum_{i=1}^k\phi_i^{(k)}X_{t-i},$$
定义**后向预测误差**，用以表示当前值滞后$k$个值的误差：
$$b_t^{(k)}=X_{t-k}-\sum_{i=1}^k\phi_i^{(k)}X_{t-k+i},$$
定义**误差能量**，通过最小化误差能量的方式来得到反射系数：
$$E^{(k)}=\sum_{t=k+1}^T\left[(f_t^{(k)})^2+(b_t^{(k)})^2\right]$$
在第$k$阶中，更新前向和后向预测误差：
$$\begin{aligned}
f_{t}^{(k)}&=f_t^{(k-1)}+\kappa_kb_{t-1}^{(k-1)},\\b_{t}^{(k)}&=b_{t-1}^{(k-1)}+\kappa_kf_t^{(k-1)}.
\end{aligned}$$
此时，可以将能量误差展开为：
$$E^{(k)}=\sum_{t=k+1}^T\left[(f_t^{(k-1)}+\kappa_kb_{t-1}^{(k-1)})^2+(b_t^{(k-1)}+\kappa_kf_t^{(k-1)})^2\right].$$
整理合并后得到：
$$E^{(k)}=\sum_{t=k+1}^T\left[(f_t^{(k-1)})^2+(b_t^{(k-1)})^2+2\kappa_kf_t^{(k-1)}b_{t-1}^{(k-1)}+\kappa_k^2((f_t^{(k-1)})^2+(b_{t-1}^{(k-1)})^2)\right].$$
为使误差能量最小化，对$\kappa_k$求导，并令导数为零：
$$\frac{\partial E^{(k)}}{\partial\kappa_k}=2\sum_{t=k+1}^Tf_t^{(k-1)}b_{t-1}^{(k-1)}+2\kappa_k\sum_{t=k+1}^T\left[(f_t^{(k-1)})^2+(b_{t-1}^{(k-1)})^2\right]=0.$$
整理得到：
$$\kappa_k=-\frac{\sum_{t=k+1}^Tf_t^{(k-1)}b_{t-1}^{(k-1)}}{\sum_{t=k+1}^T\left[(f_t^{(k-1)})^2+(b_{t-1}^{(k-1)})^2\right]}.$$
## 误差能量更新：
$$E^{(k)}=E^{(k-1)}+2\kappa_k\sum_{t=k+1}^Tf_t^{(k-1)}b_{t-1}^{(k-1)}+\kappa_k^2\cdot E^{(k-1)}.$$
$$\sum_{t=k+1}^Tf_t^{(k-1)}b_{t-1}^{(k-1)}=-\kappa_k\cdot\sum_{t=k+1}^T\left[(f_t^{(k-1)})^2+(b_{t-1}^{(k-1)})^2\right]=-\kappa_k\cdot E^{(k-1)}.$$
整理得：
$$E^{(k)}=E^{(k-1)}\cdot(1-\kappa_k^2).$$
## 白噪声误差估计
白噪声误差定义为：
$$\hat{\sigma}^2=\frac{1}{T}\sum_{t=p+1}^T\hat{\epsilon}_t^2,$$

$$\hat{\epsilon}_{t}=X_{t}-\sum_{i=1}^{p}\hat{\phi}_{i}X_{t-i}$$
仔细观察便能发现与误差能量E同源。

---
# Code
Burg方法的简单伪代码：
```python
function BurgMethod(data, p):
    # 输入：
    # data: 时间序列数据，长度为 T
    # p: AR模型的阶数
    # 输出：
    # phi: 长度为 p 的AR模型参数
    # sigma2: 白噪声的估计方差

    T = length(data)  # 数据长度
    f = data[:]       # 初始化前向误差 f_t^{(0)}
    b = data[:]       # 初始化后向误差 b_t^{(0)}

    E = sum(f**2)     # 初始预测误差能量 E^{(0)}

    phi = [0] * p     # 初始化 AR 参数数组
    for k in range(1, p+1):  # 递归估计 1 到 p 阶的参数
        # 计算反射系数 kappa_k
        numerator = -2 * sum(f[t] * b[t-1] for t in range(k, T))
        denominator = sum(f[t]**2 + b[t-1]**2 for t in range(k, T))
        kappa_k = numerator / denominator

        # 更新 AR 参数
        new_phi = [0] * k
        for i in range(k-1):  # 更新前 k-1 阶的参数
            new_phi[i] = phi[i] + kappa_k * phi[k-i-2]
        new_phi[k-1] = kappa_k  # 添加第 k 阶的反射系数

        phi[:k] = new_phi  # 更新到当前参数

        # 更新前向和后向误差
        new_f = [0] * T
        new_b = [0] * T
        for t in range(k, T):
            new_f[t] = f[t] + kappa_k * b[t-1]
            new_b[t] = b[t-1] + kappa_k * f[t]
        f, b = new_f, new_b  # 更新误差值

        # 更新总误差能量
        E = E * (1 - kappa_k**2)

    # 估计白噪声方差
    sigma2 = E / T

    return phi, sigma2

```

---
# References
