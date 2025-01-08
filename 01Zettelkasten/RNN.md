20241212
Status: #methods
Tags: 
aliases: 
# RNN
![[RNN-2.png]]
通过如图方式实现循环神经网络，每一时刻将上一时刻的输出和这一时刻的输入结合，输入到神经网络中。
$$h_t = \tanh[\boldsymbol{A} \cdot \begin{bmatrix}
h_{t-1}\\
x_t
\end{bmatrix}]$$
但是由于迭代的性质存在，导致每一次会有参数矩阵$\boldsymbol{A}$的累乘，尽管有$\tanh$的限制，还是十分容易出现梯度爆炸或者梯度消失的问题。












---
# References
[[tanh激活函数]]
