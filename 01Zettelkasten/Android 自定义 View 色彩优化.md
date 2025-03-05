20250116
Status: #public-knowledge
Tags: [[Android 自定义View]]
aliases: 
# Android 自定义 View 色彩优化

## setDither(Boolean dither)
设置图像的抖动
![[Android 自定义 View 色彩优化.png]]
只有向自建的 Bitmap 中绘制，并且选择 16 位色的 ARGB_4444 或者 RGB_565 的时候，开启它才会有比较明显的效果。

## setFilterBitmap(Boolean filter)
设置是否使用双线性规律来绘制 `Bitmap`。
![[Android 自定义 View 色彩优化-1.png]]













---
# References
