20250116
Status: #methods
Tags: [[Android 自定义View]] 
aliases: 
# Android 自定义View 绘制附加效果
## setShadowLayer
效果为在绘制内容下面加一层阴影，构造函数为：
```Java
setShadowLayer(float radius, float dx, float dy, int shadowColor)
```
如果需要清除阴影层，需要使用 `clearShadowLayer()`
> 在开启硬件加速的情况下 setShadowLayer 只支持文字的绘制

## setMaskFilter
构造函数为：
```Java
setMaskFilter(MaskFilter maskfilter)
```
分为两种效果，分别是: `BlurMaskFilter`, `EmbossMaskFilter`
### BlurMaskFilter
添加模糊效果，构造函数为：
```Java
BlurMaskFilter(float radius, BlurMaskFilter.Blur style)
```
其中 `style` 有四种类型，分别为：`NORMAL`, `SOLID` , `INNER`, `OUTER`, 效果分别如下所示
![[Android 自定义View 绘制附加效果.png|400]]
### EmbossMaskFilter
添加浮雕效果，构造函数为：
```Java
EmbossMaskFilter(float[] direction, float ambient, float specular, float blurRadius)
```
其中 `direction` 是一个三元素的数组，指定光源的方向。`ambient` 是环境光的强度，数值范围是 0-1。`specular` 是炫光系数。`blurRadius` 是应用光线的范围









---
# References
