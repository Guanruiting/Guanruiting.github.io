---
title:  重新认识Javascript对象
date: 2019-04-25 03:11:45
tags: 
- Javascript
- Object
categories: 中文
---

最近参加了高级前端的培训，虽然是线上课程，但跟着大佬学习真的是事半功倍。课程中出现很多我听不懂的技术词语，比如[“属性描述对象”](https://guanruiting.github.io/20190418/property-descriptor/)，比如一些没见过的JS内置方法等等。通过课后查资料补习，我发现自己真的是……基础太差了😓😓😓！

<!-- more -->

虽然以前一直都知道自己Javascript基础很差，也买了很多书：《Javascript DOM 编程艺术》、《Javascript权威指南》、《Javascript 高级程序设计》、《Javascript 忍者秘籍》等，却因为枯燥乏味，或晦涩难懂，或长篇大论等原因，始终还没看完……

听了大佬的课，我意识到自己对Javascript对象、Javascript函数等的认识十分匮乏，简直只是窥见了冰山一角。今天就先重新认识下Javascript对象吧。

基础的创建、用法自不必说，今天参考[MDN的手册](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Object)看看Object有哪些东东。

## Object的属性

![Object propertype](/img/2019/04/object_propertype.png)

#### Object.propertype表示Object的原型对象。Object.propertype属性的属性特性就是所谓的**属性描述对象**了。

### 1、Object.propertype

>几乎所有的 JavaScript 对象都是 Object 的实例；一个典型的对象继承了Object.prototype的属性（包括方法），尽管这些属性可能被遮蔽（亦称为覆盖）。但是有时候可能故意创建不具有典型原型链继承的对象，比如通过Object.create(null)创建的对象，或者通过Object.setPrototypeOf方法改变原型链。
>
>改变Object原型，会通过原型链改变所有对象；除非在原型链中进一步覆盖受这些变化影响的属性和方法。这提供了一个非常强大的、但有潜在危险的机制来覆盖或扩展对象行为。

### 2、已被废除的属性

- *Object​.prototype.__proto__ 曾经用来存放对象的可枚举的属性的个数，但是已经被废除。*
- *Object.prototype.__noSuchMethod__ 曾经是指当调用某个对象里不存在的方法时即将被执行的函数，但是现在这个函数已经不可用。这个属性被移除之后，ECMAScript 2015 (ES6) 规范转而采用 Proxy 对象， 可以实现类似或更多的效果。*
- *Object.prototype.__parent__ 指向一个对象的上下文，已废弃。*

### 3、Object.prototype.\_\_proto\_\_

> 该特性已经从 Web 标准中删除，虽然一些浏览器目前仍然支持它，但也许会在未来的某个时间停止支持。
> 
> 如果你关心性能，你就不应该在一个对象中修改它的 [[Prototype]]。
> 
> 创建一个新的且可以继承 [[Prototype]] 的对象，推荐使用 Object.create()。
> 
> 为了更好的支持，建议只使用 Object.getPrototypeOf()。
> 
> 使用__proto__是有争议的，也不鼓励使用它。

虽然MDN这么说，但是不知道 Object.prototype.\_\_proto\_\_，就不可能理解Javascript原型链，但今天重点不是原型链。我们只看Object.prototype.\_\_proto\_\_ 是什么。

> \_\_proto\_\_的读取器(getter)暴露了一个对象的内部 [[Prototype]] 。
> 
> 对于使用对象字面量创建的对象，这个值是 Object.prototype。对于使用数组字面量创建的对象，这个值是 Array.prototype。对于functions，这个值是Function.prototype。对于使用 new fun 创建的对象，其中fun是由js提供的内建构造器函数之一(Array, Boolean, Date, Number, Object, String 等等），这个值总是fun.prototype。对于用js定义的其他js构造器函数创建的对象，这个值就是该构造器函数的prototype属性。
>
> \_\_proto\_\_ 的设置器(setter)允许对象的 [[Prototype]]被变更。前提是这个对象必须通过 Object.isExtensible() 判断为是可扩展的，如果不可扩展，则会抛出一个 TypeError 错误。要变更的值必须是一个object或null，提供其它值将不起任何作用。
>
> .\_\_proto\_\_属性是Object.prototype 一个简单的访问器属性，其中包含了get（获取）和set（设置）的方法，任何一个\_\_proto\_\_的存取属性都继承于Object.prototype，但一个访问属性如果不是来源于Object.prototype就不拥有.\_\_proto\_\_属性，譬如一个元素设置了其他的.\_\_proto\_\_属性在Object.prototype之前，将会覆盖原有的Object.prototype。

### 4、Object.prototype.constructor

> 返回创建实例对象的 Object 构造函数的引用。注意，此属性的值是对函数本身的引用，而不是一个包含函数名称的字符串。
> 
> 所有对象都会从它的原型上继承一个 constructor 属性。该值只可读。

## Object的方法

![Object propertype](/img/2019/04/object_function.png)

这么多的方法，真是吓到我了！一下子也学不完呀，粗略地过一遍咯？先混个眼熟😂。

### Object.assign()

> 用于将所有可枚举属性的值从一个或多个源对象复制到目标对象。它将返回目标对象。

### Object.create()
> 创建一个新对象，使用现有的对象来提供新创建的对象的__proto__。 

### Object.defineProperties()
> 直接在一个对象上定义新的属性或修改现有属性，并返回该对象。

### Object.defineProperty()
> 直接在一个对象上定义一个新属性，或者修改一个对象的现有属性， 并返回这个对象。

### Object.entries()
> 返回一个给定对象自身可枚举属性的键值对数组，其排列与使用 for...in 循环遍历该对象时返回的顺序一致（区别在于 for-in 循环也枚举原型链中的属性）。

### Object.freeze()
> 冻结一个对象。一个被冻结的对象再也不能被修改；
> 
> 冻结了一个对象则不能向这个对象添加新的属性，不能删除已有属性，不能修改该对象已有属性的可枚举性、可配置性、可写性，以及不能修改已有属性的值。
> 
> 此外，冻结一个对象后该对象的原型也不能被修改。
> 
> freeze() 返回和传入的参数相同的对象。

### Object.fromEntries()
> 把键值对列表转换为一个对象。
> 
> 返回一个包含提供的可迭代对象条目的对应属性的新对象。

###### *Object.getNotifer()*
> *用于创建可人工触发 change 事件的对象，但该方法在浏览器中已被废弃。*

### Object.getOwnPropertyDescriptor()

> 返回指定对象上一个自有属性对应的属性描述符。（自有属性指的是直接赋予该对象的属性，不需要从原型链上进行查找的属性）

### Object.getOwnPropertyDescriptors() 
> 获取一个对象的所有自身属性的描述符。

### Object.getOwnPropertyNames()
> 返回一个由指定对象的所有自身属性的属性名（包括不可枚举属性但不包括Symbol值作为名称的属性）组成的数组。

### Object.getOwnPropertySymbols()
> 返回一个给定对象自身的所有 Symbol 属性的数组。

### Object.getPrototypeOf()
> 返回指定对象的原型（内部[[Prototype]]属性的值。

### Object.is()
> 判断两个值是否是相同的值。

### Object.isExtensible()
> 判断一个对象是否是可扩展的（是否可以在它上面添加新的属性）。

### Object.isFrozen()
> 判断一个对象是否被冻结。

### Object.isSealed()
> 判断一个对象是否被密封。

### Object.keys()
> 会返回一个由一个给定对象的自身可枚举属性组成的数组，数组中属性名的排列顺序和使用 for...in 循环遍历该对象时返回的顺序一致 。

###### *Object.observe()*
> *用于异步地监视一个对象的修改。当对象属性被修改时，方法的回调函数会提供一个有序的修改流。然而，这个接口已经被废弃并从各浏览器中移除。你可以使用更通用的 Proxy 对象替代。*

### Object.preventExtensions()
> 让一个对象变的不可扩展，也就是永远不能再添加新的属性。

### Object.seal()
> 封闭一个对象，阻止添加新属性并将所有现有属性标记为不可配置。当前属性的值只要可写就可以改变。

### Object.setPrototypeOf()
> 设置一个指定的对象的原型 ( 即, 内部[[Prototype]]属性）到另一个对象或  null。
> 
> *由于现代 JavaScript 引擎优化属性访问所带来的特性的关系，更改对象的 [[Prototype]]在各个浏览器和 JavaScript 引擎上都是一个很慢的操作。*

###### *Object.unobserve()*
> 非标准。
> 
> *用来移除通过 Object.observe()设置的观察者的方法。*

### Object.values()
> 返回一个给定对象自身的所有可枚举属性值的数组，值的顺序与使用for...in循环的顺序相同 ( 区别在于 for-in 循环枚举原型链中的属性 )。

## Object.prototype的方法

### Object.prototype.hasOwnProperty()
> 返回一个布尔值，指示对象自身属性中是否具有指定的属性

### Object.prototype.isPrototypeOf()
> 用于测试一个对象是否存在于另一个对象的原型链上。

### Object.prototype.propertyIsEnumerable()
> 返回一个布尔值，表示指定的属性是否可枚举。

### Object.prototype.toLocaleString()
> 返回一个该对象的字符串表示。此方法被用于派生对象为了特定语言环境的目的（locale-specific purposes）而重载使用。

### Object.prototype.toString()
> 返回一个表示该对象的字符串。

### Object.prototype.valueOf()
> 返回指定对象的原始值。你很少需要自己调用valueOf方法；当遇到要预期的原始值的对象时，JavaScript会自动调用它。

###### 非标准/已废弃/避免使用的方法

> *Object.prototype.\_\_defineGetter\_\_ 方法可以将一个函数绑定在当前对象的指定属性上，当那个属性的值被读取时，你所绑定的函数就会被调用。*
> 
> 
> *Object.prototype.\_\_defineSetter\_\_ 方法可以将一个函数绑定在当前对象的指定属性上，当那个属性被赋值时，你所绑定的函数就会被调用。*
> 
> 
> *Object.prototype.\_\_lookupGetter\_\_ 方法会返回当前对象上指定属性的属性读取访问器函数（getter）。*
> 
> 
> *Object.prototype.\_\_lookupSetter\_\_ 方法是用来返回一个对象的某个属性上绑定了 setter （设置器）的钩子函数的引用。*
> 
> 
> *Object.prototype.eval() 方法用于在对象的上下文中对 JavaScript 代码字符串求值。*
> 
> 
> *Object.prototype.toSource()方法返回一个表示对象源代码的字符串。*
> 
> 
> *Object.prototype.unwatch() 删除一个 watch() 设置的 watchpoint.*
> 
> *Object.prototype.watch() 方法会监视属性是否被赋值并在赋值时运行相关函数。*
