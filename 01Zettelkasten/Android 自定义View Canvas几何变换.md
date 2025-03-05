20250116
Status: #public-knowledge
Tags: [[Android 自定义View]] 
aliases: 
# Android 自定义View Canvas几何变换

```Java
Canvas.translate(float dx, float dy)
Canvas.rotate(float degrees, float px, float py)
```

```Java
Canvas.scale(float sx, float sy, float px, float py)
```
其中 `sx,sy` 是横向和纵向的缩放系数，`px,py` 是缩放的轴心。

```Java
Canvas.skew(float sx, float sy)
```
其中 `sx,sy` 是 x 和 y 方向的错切系数，效果如图所示
![[Android 自定义View Canvas几何变换.png|200]]











---
# References
