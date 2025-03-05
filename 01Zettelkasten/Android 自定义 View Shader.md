20250115
Status: #public-knowledge
Tags: [[Android 自定义View]]
aliases: 
# Android 自定义 View Shader
## LinearGradient
两点之间产生渐变，构造函数为：
```Java
LinearGradient(float x0, float y0, float x1, float y1, int color0, int color1, Shader.TileMode tile)
```
其中 `TileMode` 可以分为 `CLAMP`, `MIRROR` 以及 `REPEAT`, 效果分别如字面意思所示。`CLAMP` 效果为到达端点以后保持端点颜色
## RadialGradient
中心向周围渐变，构造函数为：
```Java
RadialGradient(float centerX, float centerY, float radius, int centerColor, int edgeColor, TileMode tileMode)
```
## SweepGradient
扫描渐变，构造函数为：
```Java
SweepGradient(float cx, float cy, int color0, int color1)
```
## BitmapShader
使用 Bitmap 作为图形或文字的填充，构造函数为：
```Java
BitmapShader(Bitmap bitmap, Shader.TileMode tileX, Shader.TileMode tileY)
```
## ComposeShader
将两个 Shader 进行混合使用，构造函数为：
```Java
ComposeShader(Shader shaderA, Shader shaderB, PorterDuff.Mode mode)
```
> ComposeShader 需要在关闭硬件加速的情况下才支持渲染两个相同类型的 Shader

关键参数为 `PorterDuff.Mode mode`，可以分为 Alpha 合成和 Blending 两类。
Alpha 合成效果如图：

![[Android Shader.png]]

Blending 效果如图：

![[Android Shader-1.png]]











---
# References
