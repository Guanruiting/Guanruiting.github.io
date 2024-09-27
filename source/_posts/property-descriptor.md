---
title: 初识属性描述对象——元属性
date: 2019-04-18 23:48:42
tags:
- Javascript
- Object
categories: 中文
---

假设有一个对象：

```
var obj = {
  name:"Book"
}
```

关于这个对象的属性`name`，我们提出以下问题：

1. 它的值是什么？
2. 它的值是否可以修改？
3. 它是否可以被 `for..in` 循环或者 `Object.keys()` 遍历？
4. 它是否可以被删除？

<!-- more -->

……

以上问题牵扯出了*【属性描述对象】*的概念。属性描述对象用来描述对象的属性，**控制**它的行为。每个属性都有自己对应的属性描述对象，保存该属性的一些元信息。

一个属性描述对象例子（默认值）：

```
{
  value: undefined,    // 该属性的属性值
  writable: true,      // 属性值是否可写
  enumerable: true,    // 该属性是否可遍历
  configurable: true,  // 可配置性，控制属性描述对象的可写性（是否可以被删除）
  get: undefined,      // 该属性的取值函数
  set: undefined       // 该属性的存值函数
}
```

这个属性描述对象里的属性称为*元属性*。

参考： [属性描述对象](https://wangdoc.com/javascript/stdlib/attributes.html)
