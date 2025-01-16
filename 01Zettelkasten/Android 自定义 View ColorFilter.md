20250115
Status: #methods
Tags: [[Android 自定义View]]
aliases: 
# Android 自定义 View ColorFilter
为绘制设置颜色过滤。
## LightingColorFilter
用于模拟简单的光照效果，构造函数为：
```Kotlin
LightingColorFilter(int mul, int add)
```
实现原理为：
```Kotlin
R1 = R * mul.R / 0xff + add.R
G1 = G * mul.G / 0xff + add.G
B1 = B * mul.B / 0xff + add.B
```
## PorterDuffColorFilter
使用一种颜色与 PorterDuff. Mode 来绘制，构造函数为：
```Java
PorterDuffColorFilter(int color, PorterDuff.Mode mode)
```
## ColorMatrixColorFilter
通过一个 $4 \times 5$ 的矩阵：
```Java
[ a, b, c, d, e,
  f, g, h, i, j,
  k, l, m, n, o,
  p, q, r, s, t ]
```
转换成 argb：
```Java
R’ = a*R + b*G + c*B + d*A + e;
G’ = f*R + g*G + h*B + i*A + j;
B’ = k*R + l*G + m*B + n*A + o;
A’ = p*R + q*G + r*B + s*A + t;
```
可以通过 `{Java icon}ColorMatrix` 自带的一些方法来做简单的转换，例如设置饱和度等。












---
# References
