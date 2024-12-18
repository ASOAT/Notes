20241212
Status: #methods
Tags: 
aliases: 
# LSTM
![[LSTM-2.png]]
大致的内容都在这张图里面了，可以把LSTM类比成异星工场那种类型的转送带自动化游戏，使用了各种门来对数据进行处理。
用形象一点的话来形容LSTM的过程的话就是“重重筛选”，只保留想要的信息。

**遗忘门：**
$$f_t = \sigma(W_f \cdot [\boldsymbol{h}_{t-1},\boldsymbol{x}_t]+\boldsymbol{b}_f)$$
这是一个$[0,1)$的向量，接近0代表遗忘，和上一时刻的单元状态$C_{t-1}$点乘，决定了上一时刻的单元状态保留多少到这一时刻。

**输入门**：
分为两部分，结构和遗忘门类似，就懒得打公式了。
先说使用$\tanh$作为激活函数的，这一部分相当于把这一时刻的输入信息进行处理得到$c_t'$，并没有进行删减。然后再通过输入向量$i_t$决定哪些信息需要保留。

将遗忘门和输入门加起来就是这一时刻的单元状态$c_t$

**输出门:**
既然看到sigmoid激活函数了，就说明这个门的作用在于决定这一时刻的单元状态有哪些作为我的输出。







---
# References