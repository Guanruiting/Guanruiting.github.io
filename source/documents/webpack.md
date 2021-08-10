
Webpack前端构建⼯具原理剖析

## ⼀、什么是webpack
webpack是⼀个打包⼯具，他的宗旨是⼀切静态资源皆可打包。

![image-20210720144103400](https://raw.githubusercontent.com/macshion/PicBed/main/2021/image-20210720144103400.png)

## ⼆、原型分析
⾸先我们通过⼀个制作⼀个打包⽂件的原型。

假设有两个js模块，这⾥我们先假设这两个模块是复合commomjs标准的es5模块。

我们的⽬的是将这两个模块打包为⼀个能在浏览器端运⾏的⽂件，这个⽂件其实叫bundle.js。

⽐如

```javascript
// index.js
var add = require('add.js').default
console.log(add(1 , 2))
// add.js
exports.default = function(a,b) {return a + b}
```

假设在浏览器中直接执⾏这个程序肯定会有问题 主要的问题是浏览器中没有exports对象与require⽅法所以⼀定会报错。

我们需要通过模拟exports对象和require⽅法

### 1.模拟exports对象
⾸先我们知道如果在nodejs打包的时候我们会使⽤sfs.readfileSync()来读取js⽂件。这样的话js⽂件会是
⼀个字符串。⽽如果需要将字符串中的代码运⾏会有两个⽅法分别是new Function与Eval。
在这⾥⾯我们选⽤执⾏效率较⾼的eval。

```javascript
exports = {}
eval('exports.default = function(a,b) {return a + b}') // node⽂件读取后的代码字符串
exports.default(1,3)
```

![image-20210720144245345](https://raw.githubusercontent.com/macshion/PicBed/main/2021/image-20210720144245345.png)

上⾯这段代码的运⾏结果可以将模块中的⽅法绑定在exports对象中。由于⼦模块中会声明变量，为了不污染全局我们使⽤⼀个⾃运⾏函数来封装⼀下。

```javascript
var exports = {}
(function (exports, code) {
eval(code)
})(exports, 'exports.default = function(a,b){return a + b}')
```



### 2.模拟require函数

require函数的功能⽐较简单，就是根据提供的file名称加载对应的模块。

⾸先我们先看看如果只有⼀个固定模块应该怎么写。

```javascript
function require(file) {
 var exports = {};
 (function (exports, code) {
 eval(code)
 })(exports, 'exports.default = function(a,b){return a + b}')
 return exports
}
var add = require('add.js').default
console.log(add(1 , 2))
```



完成了固定模块，我们下⾯只需要稍加改动，将所有模块的⽂件名和代码字符串整理为⼀张key-value表，就可以根据传⼊的⽂件名加载不同的模块了。

```javascript
(function (list) {
 function require(file) {
 var exports = {};
 (function (exports, code) {
 eval(code);
 })(exports, list[file]);
 return exports;
 }
 require("index.js");
})({
 "index.js": `
 var add = require('add.js').default
 console.log(add(1 , 2))
 `,
 "add.js": `exports.default = function(a,b){return a + b}`,
});
```




当然要说明的⼀点是真正webpack⽣成的bundle.js⽂件中还需要增加模块间的依赖关系。

叫做依赖图（Dependency Graph）

类似下⾯的情况。

```javascript
{
 "./src/index.js": {
 "deps": { "./add.js": "./src/add.js" },
 "code": "....."
 },
 "./src/add.js": {
 "deps": {},
 "code": "......"
 }
}
```

另外，由于⼤多数前端程序都习惯使⽤es6语法所以还需要预先将es6语法转换为es5语法。

总结⼀下思路，webpack打包可以分为以下三个步骤：

1. 分析依赖
2. ES6转ES5
3. 替换exports和require



## 三、功能实现
我们的⽬标是将以下两个个互相依赖的ES6Module打包为⼀个可以在浏览器中运⾏的⼀个JS⽂件(bundle.js)

处理模块化
多模块合并打包 - 优化⽹络请求

/src/add.js

```javascript
export default (a, b) => a + b
```

/src/index.js

```javascript
import add from "./add.js";
console.log(add(1 , 2))
```

### 1.分析模块
分析模块分为以下三个步骤：

模块的分析相当于对读取的⽂件代码字符串进⾏解析。这⼀步其实和⾼级语⾔的编译过程⼀致。需要将模块解析为抽象语法树AST。我们借助babel/parser来完成。

AST （Abstract Syntax Tree）抽象语法树 在计算机科学中，或简称语法树（Syntax tree），是源代码语法结构的⼀种抽象表示。它以树状的形式表现编程语⾔的语法结构，树上的每个节点都表示源代码中的⼀种结构。（https://astexplorer.net/）

```bash
yarn add @babel/parser
yarn add @babel/traverse
yarn add @babel/core
yarn add @babel/preset-env
```

- 读取⽂件
- 收集依赖
- 编译与AST解析

```javascript
const fs = require("fs");
const path = require("path");
const parser = require("@babel/parser");
const traverse = require("@babel/traverse").default;
const babel = require("@babel/core");
function getModuleInfo(file) {
 // 读取⽂件
 const body = fs.readFileSync(file, "utf-8");
 // 转化AST语法树
 const ast = parser.parse(body, {
 sourceType: "module", //表示我们要解析的是ES模块
 });
 // 依赖收集
 const deps = {};
 traverse(ast, {
 ImportDeclaration({ node }) {
 const dirname = path.dirname(file);
 const abspath = "./" + path.join(dirname, node.source.value);
 deps[node.source.value] = abspath;
 },
 });
运⾏结果如下：
2. 收集依赖
上⼀步开发的函数可以单独解析某⼀个模块，这⼀步我们需要开发⼀个函数从⼊⼝模块开始根据依赖关
系进⾏递归解析。最后将依赖关系构成为依赖图（Dependency Graph）
 // ES6转成ES5
 const { code } = babel.transformFromAst(ast, null, {
 presets: ["@babel/preset-env"],
 });
 const moduleInfo = { file, deps, code };
 return moduleInfo;
}
const info = getModuleInfo("./src/index.js");
console.log("info:", info);
```



运⾏结果如下：

![image-20210720144822288](https://raw.githubusercontent.com/macshion/PicBed/main/2021/image-20210720144822288.png)

### 2.收集依赖
上⼀步开发的函数可以单独解析某⼀个模块，这⼀步我们需要开发⼀个函数从⼊⼝模块开始根据依赖关
系进⾏递归解析。 后将依赖关系构成为依赖图（Dependency Graph）

```javascript
/**
 * 模块解析
 * @param {*} file
 * @returns
 */
function parseModules(file) {
 const entry = getModuleInfo(file);
 const temp = [entry];
 const depsGraph = {};
 getDeps(temp, entry);
 temp.forEach((moduleInfo) => {
 depsGraph[moduleInfo.file] = {
 deps: moduleInfo.deps,
 code: moduleInfo.code,
 };
 });
 return depsGraph;
3. ⽣成bundle⽂件
这⼀步我们需要将刚才编写的执⾏函数和依赖图合成起来输出最后的打包⽂件。
最后可以编写⼀个简单的测试程序测试⼀下结果。
}
/**
 * 获取依赖
 * @param {*} temp
 * @param {*} param1
 */
function getDeps(temp, { deps }) {
 Object.keys(deps).forEach((key) => {
 const child = getModuleInfo(deps[key]);
 temp.push(child);
 getDeps(temp, child);
 });
}
```



### 3.⽣成bundle⽂件
这⼀步我们需要将刚才编写的执⾏函数和依赖图合成起来输出最后的打包⽂件。

```javascript
function bundle(file) {
 const depsGraph = JSON.stringify(parseModules(file));
 return `(function (graph) {
 function require(file) {
 function absRequire(relPath) {
 return require(graph[file].deps[relPath])
 }
 var exports = {};
 (function (require,exports,code) {
 eval(code)
 })(absRequire,exports,graph[file].code)
 return exports
 }
 require('${file}')
 })(${depsGraph})`;
}
!fs.existsSync("./dist") && fs.mkdirSync("./dist");
fs.writeFileSync("./dist/bundle.js", content);
```



最后可以编写⼀个简单的测试程序测试⼀下结果。

<script src="./dist/bundle.js"></script>



后⾯有兴趣的话⼤家可以在考虑⼀下如何加载css⽂件或者图⽚base64 Vue SFC .vue。

ESM vs Webpack https://juejin.cn/post/6947890290896142350
⼿写webpack原理 https://juejin.cn/post/6854573217336541192
看完这篇还搞不懂webpack https://juejin.cn/post/6844904030649614349
webpack系列之打包原理 https://blog.csdn.net/weixin_41319237/article/details/116194091
