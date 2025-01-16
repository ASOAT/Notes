20250116
Status: #methods
Tags: [[Android 自定义View]] 
aliases: 
# Android 自定义View 获取绘制的Path
获取添加了线条宽度和 PathEffect 的**实际 Path**。
![[Android 自定义View 获取绘制的Path.png|400]]
## getFillPath
构造函数为：
```Java
getFillPath(Path src, Path dst)
```
其中 `src` 是想要获取的 Path，`dst` 用于保存结果
## getTextPath
![[Android 自定义View 获取绘制的Path-1.png|500]]
构造函数为：
```Java
getTextPath(String text, int start, int end, float x, float y, Path path)
getTextPath(char[] text, int index, int count, float x, float y Path path)
```











---
# References
