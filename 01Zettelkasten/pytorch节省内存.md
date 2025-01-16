20250107
Status: #methods
Tags: 
aliases: 
# pytorch节省内存

运行 `Y=Y+X ` 后，Y 会指向另一个内存地址。我们希望原地执行参数更新，不然在机器学习的过程中，其他引用可能会指向旧的内存位置。
只需要使用代码 `Y[:] = <expression>` 就可以了 












---
# References
