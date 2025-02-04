20250108
Status: #idea
Tags: 
aliases: 
# 20250108 Psychophysical用于动效评估初步想法

## 幅度
利用类似于 Weber 公式的思想
$$
c = \Delta \phi / \phi
$$
$\phi$ 表示当前输入的加速度，$\Delta \phi$ 表示屏幕上动效内容的变化。
$c$ 的变化能够说明动效对于加速度的映射合理性：按照 Weber 定律，对于更大的 $\phi$，需要更大的 $\Delta \phi$ 来确保差异能被感知到，同时对于微弱的刺激，c 也应该更大*这一点可以不考虑*。同时 $c$ 也能够为不同动效提供对比的渠道，$c$ 越大则说明动效的敏感程度越高。

## 方向
同时根据 $\Delta \phi$ 来说明动效方向设计的合理程度，$\Delta \phi$ 主要通过前后图像像素的变化程度计算得到，从这能够得出：
- 对于不同方向的加速度输入，图像的变化是否构成显著差异，否则说明图像对于方向的提示较为模糊，存在两种情况：
	- 在设计上就存在两个方向容易混淆的问题。
	- 对于处于周边视觉范围的提示，例如固定的箭头，在方向变化时像素的变化程度有限，因此认为对于方向的提示是模糊的，这一点可以通过叠加周边视觉的显著性概率分布进行表示。












---
# References
[[Weber公式]]
[[Fechner 定律]]