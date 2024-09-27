---
title: Typescript手册指南阅读笔记 - 类型与接口
date: 2020-12-22 09:53:00
tags:
- Typescript
categories: 中文
---



TypeScript支持与JavaScript几乎相同的数据类型。

<!--more-->

## 基础类型

TypeScript支持的类型：

![](https://raw.githubusercontent.com/macshion/PicBed/main/images/%E5%9F%BA%E7%A1%80%E7%B1%BB%E5%9E%8B.jpg)

#### 类型断言

通过*类型断言*这种方式告诉编译器，“相信我，我知道自己在干什么”。 TypeScript会假设你已经进行了必须的检查，编译时不再对其进行特殊的数据检查和解构。

类型断言有两种形式。 其一是“尖括号”语法：

```ts
let someValue: any = "this is a string";

let strLength: number = (<string>someValue).length;
```

另一个为`as`语法：

```ts
let someValue: any = "this is a string";

let strLength: number = (someValue as string).length;
```

两种形式是等价的。 然而，当你在TypeScript里使用JSX时，只有 `as`语法断言是被允许的。



## 接口

TypeScript的核心原则之一是对值所具有的*结构*进行类型检查。接口的作用就是为这些类型命名定义契约。

类型检查器不会去检查属性的顺序，只要相应的属性存在并且类型也是对的就可以。

使用接口描述：必须包含一个`label`属性且类型为`string`：

```ts
interface LabelledValue {
  label: string;
}

function printLabel(labelledObj: LabelledValue) {
  console.log(labelledObj.label);
}

let myObj = {label: "Size 10 Object"};
printLabel(myObj);
```

#### 可选属性

带有可选属性的接口与普通的接口定义差不多，只是在可选属性名字定义的后面加一个`?`符号。可选属性的好处之一是可以对可能存在的属性进行预定义，好处之二是可以捕获引用了不存在的属性时的错误。 

```ts
interface SquareConfig {
  color?: string;
  width?: number;
}
```

#### `readonly`

在属性名前用 `readonly`来指定只读属性。 赋值后， 属性值不能被改变了。

```ts
interface Point {
    readonly x: number;
    readonly y: number;
}
```

#### `ReadonlyArray<T>`

TypeScript具有`ReadonlyArray<T>`类型，它与`Array<T>`相似，只是把所有可变方法去掉了，因此可以确保数组创建后再也不能被修改。

```ts
let a: number[] = [1, 2, 3, 4];
let ro: ReadonlyArray<number> = a;
```

#### 字符串索引签名

如果对象可能具有某些做为特殊用途使用的额外属性，或者带有任意数量的其它属性，则可添加一个字符串索引签名。

```ts
interface SquareConfig {
    color?: string;
    width?: number;
    [propName: string]: any;
}
```

#### 绕过接口检查

跳过这些检查的方式，就是将这个对象赋值给一个另一个变量（不建议这样做）。

```ts
let squareOptions = { colour: "red", width: 100 };
let mySquare = createSquare(squareOptions);
```

#### 函数类型

表示函数类型需要给接口定义一个调用签名。 它就像是一个只有参数列表和返回值类型的函数定义。参数列表里的每个参数都需要名字和类型。函数的参数名不需要与接口里定义的名字相匹配。函数的返回值类型是通过其返回值推断出来的。

```ts
interface SearchFunc {
  (source: string, subString: string): boolean;
}

let mySearch: SearchFunc;
mySearch = function(src: string, sub: string): boolean {
  let result = src.search(sub);
  return result > -1;
}
```

#### 可索引类型

可索引类型描述那些能够“通过索引得到”的类型，它具有一个 *索引签名*，它描述了对象索引的类型，还有相应的索引返回值类型。

```ts
interface StringArray {
  [index: number]: string;
}

let myArray: StringArray;
myArray = ["Bob", "Fred"];

let myStr: string = myArray[0];
```

将索引签名设置为只读，防止给索引赋值。下面代码你不能设置`myArray[2]`，因为索引签名是只读的。

```ts
interface ReadonlyStringArray {
    readonly [index: number]: string;
}
let myArray: ReadonlyStringArray = ["Alice", "Bob"];
```

#### 类类型

```ts
interface ClockInterface {
    currentTime: Date;
    setTime(d: Date);
}

class Clock implements ClockInterface {
    currentTime: Date;
    setTime(d: Date) {
        this.currentTime = d;
    }
    constructor(h: number, m: number) { }
}
```

操作类和接口的时候，有两个类型：静态部分与实例部分。

接口也可以相互继承，一个接口可以继承多个接口，创建出多个接口的合成接口。

当接口继承了一个类类型时，它会继承类的成员但不包括其实现。

