20250116
Status: #methods
Tags: [[Android 自定义View]] 
aliases: 
# Android 自定义View PathEffect
## CornerPathEffect
把所有拐角变成圆角，构造函数为：
```Java
CornerPathEffect(float radius)
```
## DiscretePathEffect
对线条进行随机的偏离，构造函数为：
```Java
DiscretePathEffect(float segmentLength, float deviation)
```
原理是将绘制改成使用定长的线段进行拼接，并且在拼接的时候对路径进行随机偏离。
其中，`segmentLength` 代表用于拼接的每一段线条的长度，`deviation` 是片力量，效果如下图所示
![[Android 自定义View PathEffect.png|300]]
## DashPathEffect
使用虚线进行绘制，构造函数为：
```Java
DashPathEffect(float[] intervals, float phase)
```
其中 `intervals` 是一个数组，数组中的元素数必须为偶数，以线条长度、空白长度的顺序排列。通过控制这个数组可以实现不同效果的虚线。
`Phase` 是虚线的偏移量，通过改变这个数能够实现虚线的滚动显示。
## PathDashPathEffect
使用一个 `Path` 来绘制虚线，构造函数为;
```Java
PathDashPathEffect(Path shape, float advance, float phase, PathDashPathEffect.Style style)
```
其中 `advance` 是两个相邻 `shape` **起点**之间的间隔；`style` 用于制定拐弯改变的时候 `shape` 的转换方式，有三个值，`TRANSLATE`, `ROTATE`, `MORPH`, 效果分别如下所示
![[Android 自定义View PathEffect-1.png]]
## SumPathEffect
分别按照两种 `PathEffect` 对目标进行绘制，构造函数为：
```Java
SumPathEffect(PathEffect pathEffect1, PathEffect pathEffect2)
```
*与 ComposePathEffect 不同，这一效果最终实现的实际是两条 Path*
## ComposePathEffect
对目标使用一个 PathEffect ，然后再使用另一个，构造方法为：
```Java
ComposePathEffect(PathEffect outerpe, PathEffect innerpe)
```
其中 `innerpe` 是先应用的，`outerpe` 是后应用的。









---
# References
