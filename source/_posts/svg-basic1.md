---
title: SVG 基础知识（一） - SVG 视口
date: 2019-08-12 00:09:12
tags:
- SVG
categories: 中文
---

SVG 是可缩放矢量图形（Scalable Vector Graphics, SVG），一种用来描述二维矢量图形的 XML 标记语言。SVG 图像在放大或改变尺寸的情况下其图形质量不会有所损失。SVG是万维网联盟的标准，与诸如 DOM 和 XSL 之类的 W3C 标准是一个整体。

<!--more-->
## SVG 是什么？
+ SVG 指可伸缩矢量图形（Scalable Vector Graphics）；
+ SVG 用来定义用于网络的基于矢量的图形；
+ SVG 使用XML格式定义图形；
+ SVG 图像在放大或改变尺寸的情况下其图形质量不会有所损失；
+ SVG 是万维网联盟的标准；
+ SVG 与诸如 DOM 和 XSL 之类的 W3C 标准是一个整体。

## SVG 的优势
+ SVG 可被非常多的工具读取和修改（比如记事本）；
+ SVG 图像中的文本是可选的，同时也是可搜索的（很适合制作地图）；
+ SVG 与 JPEG 和 GIF 图像比起来，尺寸更小，且可压缩性更强（小）；
+ SVG 图像可在任何的分辨率下被高质量地打印，可在图像质量不下降的情况下被放大（可伸缩）；
+ SVG 文件是纯粹的 XML，可以与Java技术一起运行，与其他标准（比如 XSL 和 DOM）相兼容（开放标准）。

## SVG 视口
### viewport
  SVG 可见区域的大小，或者可以想像成舞台大小，画布大小。

  ``` html
  <svg width="800" height="600"></svg>
  ```
SVG单位：em/rem, ex, px, in, cm, mm

|单位|含义|
|:-:|:-|
|em|相对于父元素的字体大小|
|ex|相对于小写字母“x”的高度|
|px|相对于屏幕分辨率而不是视窗的大小：通常为1个点或1/72英寸|
|in|inch, 表英寸|
|cm|centimeter, 表厘米|
|mm|millimeter, 表毫米|


### viewBox
视区盒子，SVG就像是我们的显示器屏幕，viewBox 就是截屏工具选中的那个框框， 最终的呈现就是把框框中的截屏内容再次在显示器中全屏显示！

```javascript
viewBox="x,y,width,height"
// x: 左上角横坐标, y: 左上角纵坐标, width: 宽度, height: 高度
```

### preserveAspectRatio
使用 preserveAspectRatio 属性来让 viewBox 保持宽高比。
```
preserveAspectRatio=[defer]<align><meetOrSlice>
```
defer 参数是可选值，它仅仅在 image 元素上应用 preserveAspectRatio 属性时才使用。在使用其他元素时会被忽略。
align 参数控制 viewBox 是否强制进行均匀的缩放。

|取值|描述|
|:-:|:-|
|xMin|viewBox 的最小 X 值对齐 viewport 的左边部|
|xMid|viewBox 的 X 轴中点对齐 viewport 的 X 轴中点|
|xMax|viewBox 的最大 X 值对齐 viewport 的右边部|
|YMin|viewBox 的最小 Y 值对齐 viewport 的顶边|
|YMid|viewBox 的 Y 轴中点对齐 viewport 的 Y 轴中点|
|YMax|viewBox 的最小 Y 值对齐 viewport 的底边|

![SVG preserveAspectRatio align 参数图解](/img/2019/08/Screen Shot 2019-08-12 at 01.19.47.png)

align 参数的3x3种组合取值

|取值|描述|类比|
|:-:|:-|:-|
|xMinYMin|viewBox 的 &lt;min-x&gt; 对齐 viewport 的最小 X 值，min-y 对齐 viewport 的最小 Y 值|background-position: 0% 0%;|
|xMinYmid|viewBox 的 &lt;min-x&gt; 对齐 viewport 的最小 X 值，viewBox 的 Y 轴中点 对齐 viewport 的 Y 轴中点|background-position: 0% 50%;|
|xMinYMax|viewBox 的 &lt;min-x&gt; 对齐 viewport 的最小 X 值，min-y+&lt;height&gt; 对齐 viewport 的最小Y值|background-position: 0% 100%;|
