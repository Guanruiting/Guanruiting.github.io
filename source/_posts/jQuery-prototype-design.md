---
title: jQuery源码分析：无new构造实例及共享原型对象设计
date: 2019-04-27 12:21:47
tags:
- jQuery
- Javascript
category: 中文
---

### Javascript立即执行函数

> 立即执行函数常用于第三方库，好处在于隔离作用域。作用域隔离非常重要，是一个JS框架必须支持的功能。任何一个第三方库都会存在大量的变量和函数，为了避免变量污染（命名冲突），开发者们想到的解决办法就是使用立即执行函数。

<!-- more -->

立即执行函数两种常见形式：
`
(function(){})()
`
`
(functin(){}())
`
> 通过定义一个匿名函数，创建了一个新的函数作用域，相当于创建了一个“私有”的命名空间，该命名空间的变量和方法，不会破坏污染全局的命名空间。此时若是想访问全局对象，将全局对象以参数形式传进去即可:

```
(function(window){
	//将全局对象window以参数形式传进来
	console.log(window) //Window对象
}(window);
```
详见参考文章：[https://www.cnblogs.com/cnfxx/p/7337889.html](https://www.cnblogs.com/cnfxx/p/7337889.html)

### jQuery共享原型对象
我们在项目中引入jQuery框架后，可以通过`$.`或者`jQuery.`使用它提供的方法。这在jQuery中是怎么实现的呢？
jQuery共享原型设计：

![](/img/2019/04/jquery_prototype_design.png)

```
(function(root){ 

    var jQuery = function(){   
        // 如果直接返回jQuery构造函数的实例对象，就会进入死循环
        // 返回jQuery原型上扩展的init方法的实例对象
        return new jQuery.prototype.init();
    }
    
    jQuery.prototype = {
        init: function(){ 
            //init方法作为构造函数
        },
    }
    
    // jQuery原型上的init构造函数与jQuery构造函数共享原型对象
    jQuery.prototype.init.prototype = jQuery.prototype
    
    root.$ = root.jQuery = jQuery
    
})(this);
```

