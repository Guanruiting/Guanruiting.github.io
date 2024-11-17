---
title: jQuery源码分析：extend对象扩展函数
date: 2019-04-27 16:13:44
tags:
- jQuery
- Javascript
category: 中文
---

jQuery.extend() 函数用于将一个或多个对象的内容合并到target目标对象。如果多个对象具有相同的属性，则后者会覆盖前者的属性值。

<!-- more -->

##### 语法一：浅拷贝

`$.extend( target [, object1 ] [, objectN ] )`

*例：*

``` javascript
var obj = $.extend({name:"Tim"},{age:11,sex:"boy"})
cosole.log(obj) //输出 {name: "Tim", age: 11, sex: "boy"}
```

##### 语法二：指示是否深度合并

`$.extend( [deep ], target, object1 [, objectN ] )`

*例：*

```javascript
var ret = {name:"mm",list:{age:12}}
var res = {name:"mm",list:{sex:"boy",height:"140CM"}}
var obj = $.extend(true,{},ret,res)

console.log(obj) //{ name: "mm", list: { age: 12 height: "140CM" sex: "boy" } }
```

#### 如果只传递一个参数

> 如果只为`$.extend()`指定了一个参数，则意味着参数target被省略。此时，target就是jQuery对象本身。通过这种方式，我们可以为全局对象jQuery添加新的函数。

说完了用法，我们来剖析下源码的实现（你可能会对上一篇文章感兴趣：[jQuery源码分析：无new构造实例及共享原型对象设计](https:guanruiting.github.io/20190427/jQuery-prototype-design/)）：

``` javascript
(function(root){
    var jQuery = function(){   
        return new jQuery.prototype.init();
    }
    jQuery.fn = jQuery.prototype = {
        init: function(){
            // console.log(this)
        },
    }

    // extend 对象扩展
    // jQuery.fn.extend 与 jQuery.extend 是通过同一个匿名函数来实现
    jQuery.fn.extend = jQuery.extend = function(){
    	 // 把第一个参数赋值给target，若没有传参，则创建一个空对象
        var target = arguments[0] || {};
        // 获取参数个数
        var length = arguments.length;
        // i用于循环参数
        var i = 1;
        // 是否深拷贝
        var deep = false;
        var option,name,copy,src,copyIsArray,clone;
        // 判断第一个参数是否布尔值，是则设置deep为true
        if(typeof target === "boolean"){
            deep = target;
            target = arguments[1] // 设置第二个参数为target
            i = 2; // 因为第一个参数是布尔值，所以后面的for循环从第三个参数开始
        }
        // 传参异常处理
        if(typeof target !== "object"){
            target = {};
        }
        // 判断参数个数，传递1个参数的时候给jQuery实例对象进行扩展
        if(length === i){
            target = this; // 如果只有一个参数，则设置target为jQuery对象本身
            i--; // i = 0
        }

        
        // 如果第一个参数是布尔类型，i初始值为2
        // 如果只传入一个参数，i初始值为0
        // 如果传入2或2个以上参数，i初始值为1
        
        for(; i<length; i++){
        	  // 把参数存入一个变量option
            if((option = arguments[i]) != null){
                for(name in option){ // 循环需要拷贝的对象
                		// 把属性值赋给copy
                    copy = option[name];
                    
                    src = target[name];//第一次循环为undefined
                    //// 深拷贝
                    //判断参数（对，它是一个对象）的属性值是否也为对象或数组
                    if(deep && (jQuery.isPlainObject(copy) || (copyIsArray = jQuery.isArray(copy)))){
                        
                        if(copyIsArray){
                            copyIsArray = false;
                            clone = src && jQuery.isArray(src) ? src : [];
                        } else {
                            clone = src && jQuery.isPlainObject(src)?src:{};
                        }
                        
                        // 递归
                        target[name] = jQuery.extend(deep,clone,copy);
                    
                    //// 浅拷贝
                    } else if (copy != undefined){
                    	 // 替换目标属性的值
                        target[name] = copy;
                    }
                }
            }
        }
        return target;
    };

    jQuery.fn.init.prototype = jQuery.fn

    jQuery.extend({
        // 类型检测
        isPlainObject:function(obj){
            return toString.call(obj) === "[object Object]";
        },
        isArray: function(obj){
            return toString.call(obj) === "[object Array]";
        }
    });

    root.$ = root.jQuery = jQuery
})(this);
```