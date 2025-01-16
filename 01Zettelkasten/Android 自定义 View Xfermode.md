20250115
Status: #methods
Tags: [[Android 自定义View]] 
aliases: 
# Android 自定义 View Xfermode
Xfermode 即 Transfermode
以绘制的内容作为源图像，以 View 中已有的内容作为目标图像，选取一个 `PorterDuff.Mode` 作为绘制内容的颜色处理方案。

使用方法：
```Java
Xfermode xfermode = new 	PorterDuffXfermode(PorterDuff.Mode.DST_IN);
```
> 1. 需要使用离屏缓冲，可能会涉及到硬件加速有关的内容。
> 2. 需要控制透明区域，使其能够覆盖到要和它结合绘制的内容。












---
# References
