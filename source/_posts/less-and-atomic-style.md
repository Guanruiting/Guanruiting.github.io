---
title: Less递归批量生成原子样式（Atomic style）
date: 2019-04-20 23:30:07
tags:
- Less
- CSS
category: 中文
---

*什么是原子样式？*

原子样式指的是定义一些常用的基本样式，在标签里通过组合CLASS引用。

<!-- more -->

如,定义表示颜色的原子样式：

```
.red{color:#80211d;}
.yellow{color:#dee934;}
```
定义表示边距的原子样式:

```
.ml5{margin-left:5px;
.ml10{margin-left:10px}
```

引用的时候通过组合CLASS的形式：

```
<div class="red ml10"></div>
```

这样做当然有利也有弊，具体不多分析了。但它有一个好处是我抗拒不了的：

> 省去了给部分标签起CLASS名


有时候有些标签元素不需要很多样式，比如仅仅需要加个边距，这个时候原子样式无疑是十分方便的😝

我就很喜欢使用表示边距的原子样式。但是，边距有内边距外边距、上边距下边距、左边距右边距，还有不同数值大小的边距……

定义边距相关的原子样式的时候，可能都要一两百行以上，OMG！

好在有CSS预处理器这种东西，比如LESS。下面用使用LESS，通过递归的方法批量生成原子样式。

注意：

*// 变量说明*

**@n**：循环次数、**@a**：每次递增、**@name**：Class名称前缀、@pro：属性名、**@i**：Class名称后缀&开始数字*

```
@px:0px;
.space(@n, @a, @name, @pro, @i) when (@i =< @n){
    .@{name}@{i} {
        @{pro}: @px + @i;
    }
    .space(@n, @a, @name, @pro, (@i + @a));
}
//调用函数
.space(20,1,p,padding,1);
.space(20,1,pl,padding-left,1);
.space(20,1,pr,padding-right,1);
.space(20,1,pt,padding-top,1);
.space(20,1,pb,padding-bottom,1);

.space(20,1,m,margin,1);
.space(20,1,ml,margin-left,1);
.space(20,1,mr,margin-right,1);
.space(20,1,mt,margin-top,1);
.space(20,1,mb,margin-bottom,1);

.space(100,5,p,padding,25);
.space(100,5,pl,padding-left,25);
.space(100,5,pr,padding-right,25);
.space(100,5,pt,padding-top,25);
.space(100,5,pb,padding-bottom,25);

.space(100,5,m,margin,25);
.space(100,5,ml,margin-left,25);
.space(100,5,mr,margin-right,25);
.space(100,5,mt,margin-top,25);
.space(100,5,mb,margin-bottom,25);

.space(500,50,p,padding,150);
.space(500,50,pl,padding-left,150);
.space(500,50,pr,padding-right,150);
.space(500,50,pt,padding-top,150);
.space(500,50,pb,padding-bottom,150);

.space(500,50,m,margin,150);
.space(500,50,ml,margin-left,150);
.space(500,50,mr,margin-right,150);
.space(500,50,mt,margin-top,150);
.space(500,50,mb,margin-bottom,150);
```
