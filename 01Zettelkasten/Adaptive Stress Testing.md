20241218
Status: #public-knowledge
Tags: 
aliases: 
# Adaptive Stress Testing
目标：找到输入序列$\textbf{x}$使系统失败概率（或者发生event of interest）最大
使用MDP建模，定义状态、动作、奖励函数和转移概率
使用优化算法搜索最优路径，常用：
- 强化学习
- MCTS

对于系统中非马尔可夫的部分（例如被测的自动驾驶系统，一般认为是黑盒的），通过动作回放的方式，再现某一个状态，即用$a_{0:t-1}$表示状态$s_t$


![[Pasted image 20241218163605.png]]
![[AST Application in Autonomous Vehicles.png]]
![[AST Application in Autonomous Vehicles-1.png]]
















---
# References
