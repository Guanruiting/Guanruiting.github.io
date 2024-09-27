---
title: 微前端探索
date: 2021-02-25 10:44:54
tags:
- 微前端
category: 中文
---



转自张泰峰的博客《微前端大赏》

一、[https://www.cnblogs.com/ztfjs/p/single-spa.html](https://www.cnblogs.com/ztfjs/p/single-spa.html)

二、[https://www.cnblogs.com/ztfjs/p/single-spa2.html](https://www.cnblogs.com/ztfjs/p/single-spa2.html)

三、[https://www.cnblogs.com/ztfjs/p/qiankun.html](https://www.cnblogs.com/ztfjs/p/qiankun.html)



## 微前端大赏

### 什么是“微”

什么是微前端？微前端解决了什么问题？要回答这两个问题，我们首先要解决的是：什么是“微”。大家可能已经听说过微服务的概念， 微服务是后端服务的一种架构模式，它想解决的问题是可用性问题、扩展性问题、耦合度问题，进而演变出“服务治理”，"服务发现"等技术。例如：

- 通过熔断、限流等机制保证高可用
- 微服务之间调用的负载均衡
- 分布式事务（2PC、3PC、TCC、LCN等）
- 服务调用链跟踪
- 配置中心
- 服务自动发现



“微”的基础能力：

 **单一职责**

 一个微服务应该都是单一职责的，这才是“微”的体现，**一个微服务解决一个业务问题（注意是一个业务问题而不是一个接口）。**

**面向服务**

将自己的业务能力封装并对外提供服务，这是继承SOA的核心思想，一个微服务本身也可能使用到其它微服务的能力

这两个基础的能力构成了微服务整个的架构体系，是围绕服务、围绕一个个单一的职责体系的，它将一个、多个不同业务体系内的服务连接起来合并成一个大的业务模块，再分而治之，对每个服务做相应的技术、业务处理，合并成了一整个面向服务的业务。当服务发生故障，熔断机制产生作用，兜底服务马上启用，然后调用告警服务，将信息通知给通知服务，接着通知服务负责提醒对应的人员查看并解决问题。
这一系列的操作就是微服务的“微”字所要解决的问题，它把传统的大型项目拆分成各个不同的业务模块，再由各种一致性组件、可用性组件把它们组合起来使用。

“微”是分治的意思，那微前端是什么呢？

### 前端的历史

#### 后端jsp时代

JSP时代没有太多的悬念，我依稀还记得那个年代，当我clone下后端爸爸的代码，笨拙的在windows电脑上按照csdn的步骤安装java的jdk，打开百度搜索“JRE和JDK的区别是什么，我有没有装错”...一言难尽。总之那个年代，我们前端的代码大多数必须经过后端同学在jsp里面的标签处理才可以在线上使用这个时候拆分、分治的工作都集中在js，会分为很多套不同的js代码，在script中依次引入操作的。
这个阶段前端其实并不“微”，只是作为一个界面脚本标记存在的而已。

#### iframe时代

渐渐的ajax、jQuery、require.js的出现打破了前端生态的模式，ajax使前后端分离，jQuery使前端变得更加容易编写，而AMD的模块规范以及require.js的出现让前端从此变得不一样了，前端进入了模块化的时代。

require.js是遵循AMD协议的一个前端模块化库。

最早的时候，所有Javascript代码都写在一个文件里面，只要加载这一个文件就够了。后来，代码越来越多，一个文件不够了，必须分成多个文件，依次加载。下面的网页代码，相信很多人都见过。

```html
<script src="1.js"></script>
<script src="2.js"></script>
<script src="3.js"></script>
```

requireJS的写法：

模块代码：

```JavaScript
// main.js

require(['moduleA', 'moduleB', 'moduleC',function (moduleA, moduleB, moduleC){

　// some code here

});
```

requireJS可以通过我们现在熟悉的request()，类似的写法去引入一个模块，在这个时候，它的理念跟iframe相结合，就有了第一个“微前端”的架构模式，当然这个时候的微前端并不很“微”。

通过一张阿里云的控制台的图来解释这套架构的模式：

![avatar](https://raw.githubusercontent.com/macshion/PicBed/main/images/893115-20201018210033817-48394595.jpg)

主应用负责框架、通信、路由、资源分配。
子应用负责实现业务。
两者之间通过一套特定的sdk进行交互。

已经非常接近微服务的整体概念了。 通过主框架解决共性问题，拆分各个不同的微模块、微应用解决各个单一职责的问题，这个时候每个应用是**面向应用**的,即应用本身只对应用本身负责，它有很多特性：

1、技术栈无关，遵循同一套通信机制即可
2、应用解偶，团队之间通过主框架基座进行交互
3、热更新插拔，不需要全部更新主框架，只需要更新对应的应用即可
4、可动态降级熔断

......

可以说这一时期的前端已经进入了微前端时代。当然不是所有的应用都适用于这一个庞大的开发模式，毕竟阿里云几十上百个不同的应用模块是需要庞大的业务支撑的。

#### 打包技术与SSR(服务端渲染)

然后gulp、webpack出现了，angular、vue、react单页应用也出现了。

但问题来了，我们知道一个单页应用里资源是很重的。首页的加载速度需要很大的代价去优化它。这个时候iframe会带来比较严重的体验问题。

**Single-spa出现了**

Single-spa是一个用于前端微服务化的JavaScript前端解决方案。

同样的技术栈无关，在同一个页面中使用多种技术框架(React, Vue, AngularJS, Angular, Ember等任意技术框架)，并且不需要刷新页面。
也同样无需重构现有代码，使用新的技术框架编写代码，现有项目中的代码无需重构。
更好的资源控制，每个独立模块的代码可做到按需加载，不浪费额外资源。
每个独立模块可独立运行。大致是这样的：
![avatar](https://raw.githubusercontent.com/macshion/PicBed/main/images/2029960-61faa258ec37bf2f.png)

让我们再去盗几张别人的图：（图片来自网络，侵权通删）

![image-20210225105459886](https://raw.githubusercontent.com/macshion/PicBed/main/images/image-20210225105459886.png)

**Loader**

Loader是核心模块的加载器，可以通过loader来进行子应用的加载，目前的微前端方案设计里面一般有两种模式。

第一种是非侵入式(iframe模式)，通过加载对应子应用的 index.html 文件，再通过对首页html文件进行解析，获取到子应用的js文件和css文件，进行加载。

另一种是子应用打包成一个js文件，按照规范的导出格式,主应用只加载 index.js 文件。获取到对应的render和destroy方法。

**External**

在SPA微前端中有一个需要解决的问题就是，子应用间的公共依赖，我们如何抽离项目间的公共依赖呢，由于我们将一个应用拆分成了多个子应用，那子应用之间的依赖如何复用。如果了解commonJS的同学应该知道，commonJS具备加载模块缓存能力，加载过的模块会将其缓存起来，那么是不是我们可以将子模块以commonJS的规范进行打包。在加载子模块时，提供全局的exports和require方法，将子应用导出的exports进行收集,在require时加载我们配置的external资源。

### 核心问题

#### * 通信 *

**消息总线**，简单理解就是一个消息收发中心，众多应用可以连接到总线上，应用可以往消息中心发送或接收信息（通过订阅监听或主动推拉）。比如：应用A发送一条消息到总线上，总线判断应该送给应用B,应用B可以接收到信息（应用B订阅或拉取到了应用A的消息），这样的话，消息总线就充当一个中间者的角色，使得应用A和应用B解偶了，很方便。

在前端可使用的技术大致有：

1、通过window交互，需要注意的是domain域名的设置，比较复杂，维护成本高，不可控性高。

2、通过socket，主应用和子应用连接socket，通过服务端实现通信，一般没有人这么用，比较复杂, 成本高。

3、通过url进行简单的交互，大多应用采用的是由路由参数进行交互的，实现简单且体验较好。

4、localstorage等存储媒介。

#### 鉴权问题

微前端怎样在各个模块之间统一权限体系？这个问题前端解决的难度不低，玩的不好容易崩溃。
一般情况下由后台爸爸，通过cookie识别，从后台接口带出对应的权限数据在前端进行二次判断。

#### 污染问题

1、全局环境污染
2、事件污染
3、style污染
4、定时器污染
5、localstorage污染

解决全局环境污染和style污染，通常采用**快照模式**和**代理劫持**，在新的api中还可以采用**shadowbox**。

#### Sandbox

有一个核心的模块是沙盒，由于多个子应用会反复的展示在同一个容器内，子应用中会造成对当前环境的副作用，例如：全局样式、全局变量、监听事件、定时器等。沙盒在这里主要是为运行中的程序提供隔离环境，避免应用之间相互影响。在应用的运行环境中做资源隔离，监听应用的生命周期进行清理、加载操作。

### 小结：什么是微前端

微前端（Micro-Frontends）是一种类似于微服务的架构，它将微服务的理念应用于浏览器端，即：

**将 Web 应用由单一的单体应用转变为多个小型前端应用聚合为一的应用。各个前端应用还可以独立运行、独立开发、独立部署。微前端不是单纯的前端框架或者工具，而是一套架构体系**。

这个概念最早在2016年底被提出，可以参考在Google上搜索Micro-Frontends, 排名靠前的https://micro-frontends.org的博客文章，提出了早期的微前端模型。

**微前端能做什么？**

1、拆分和细化
2、整合历史系统
3、独立构建发布
4、治理、熔断、降级
……

### 相关资源

前端微服务化解决方案2 - Single-SPA：[https://www.jianshu.com/p/c0f4b837dbea](https://www.jianshu.com/p/c0f4b837dbea)
前端必看的微前端：[https://zhuanlan.zhihu.com/p/162726399](https://zhuanlan.zhihu.com/p/162726399)
微前端-最容易看懂的微前端知识：[https://zhuanlan.zhihu.com/p/141530392](https://zhuanlan.zhihu.com/p/141530392)

下期我们可以具体实践实践，自己动手搭建一个基于single-spa的微前端框架，敬请期待。



## 微前端大赏二：single-spa实践

#### single-spa

single-spa是一个javascript库，它可以让很多小页面、小组件、不同架构的前端组件在一个页面应用程序中共存。

这里有一个演示: ([https://single-spa.surge.sh](https://single-spa.surge.sh/))

这个库可以让你的应用使用多个不同的技术栈（vue、react、angular等等）,这样我们就可以做同步开发，最后再使用一个公用的路由即可实现路由完美切换。也可以使用一样的技术栈，分不同的团队进行开发，只需要最后使用这个库把它们整合在一起，设置不用的路由名称就可以了。

**优点:**

- 敏捷
  
    独立开发和更快的部署周期： 开发团队可以选择自己的技术并及时更新技术栈。 一旦完成其中一项就可以部署，而不必等待所有事情完毕。
    
- 风险下降
  
    降低错误和回归问题的风险，相互之间的依赖性急剧下降。
    
- 更小单元
  
    更简单快捷的测试，每一个小的变化不必再触碰整个应用程序。
    
- 持续交付
  
    更快交付客户价值，有助于持续集成、持续部署以及持续交付。

**缺点：**

- 配置复杂
  
    single-spa相对来说配置复杂，当然我们还有更简单一点的qiankun，也可以基于single-spa封装一套更适合自己的框架。
    
- 一定的资源浪费
  
    由于核心逻辑还是在于请求manifest，拿到js文件后执行渲染，这个过程不可避免会产生一些冗余，对于C端的应用来说，这个问题比较致命，当然，对于B端来说，这个是可以接受的，在可控制的范围之内

#### single-spa核心逻辑

几张图可以解决single-spa的核心逻辑

![avatar](https://raw.githubusercontent.com/macshion/PicBed/main/images/o_2011301725479072df3196964d51abc0e7f250332962.jpg)

第一张图，很显然，第一步，在我们的webpack应用里生成一个manifest.json文件，这个文件内容差不多如下：

```json
{
  "files": {
    "static/js/0.chunk.js": "/static/js/0.chunk.js",
    "static/js/0.chunk.js.map": "/static/js/0.chunk.js.map",
    "static/js/1.chunk.js": "/static/js/1.chunk.js",
    "static/js/1.chunk.js.map": "/static/js/1.chunk.js.map",
    "main.js": "/static/js/main.chunk.js",
    "main.js.map": "/static/js/main.chunk.js.map",
    "runtime-main.js": "/static/js/bundle.js",
    "runtime-main.js.map": "/static/js/bundle.js.map",
    "index.html": "/index.html",
    "static/media/logo.svg": "/static/media/logo.103b5fa1.svg"
  },
  "entrypoints": [
    "static/js/bundle.js",
    "static/js/0.chunk.js",
    "static/js/main.chunk.js"
  ]
}
```

关键点在 entrypoints 这个属性，我们可以通过manifest拿到项目的依赖表并可以使用script标签动态加载出来，这个时候我们就可以实现动态加载不同的微前端应用了。

![image-20210225105932045](https://raw.githubusercontent.com/macshion/PicBed/main/images/image-20210225105932045.png)

第二张图，我画出了更加具体的，single-spa在渲染过程中的核心逻辑：

1、 首先我们有 main（主app）和 child（子app），主app只有一个，子app可以有多个

2、 其次，主app上一般我们可以在index.html里面，写多几个空间，也就是多几个div

例如：

```html
<div id=”react-app”></div>
<div id=”vue-app”></div>
```

3、然后，在我们的child上，要用webpack插件，生成一个带有所有需要加载的依赖文件的manifest.json 

4、主应用去加载manifest.json，获取到具体的js，使用script标签把它放到主应用上，进行渲染

至此，我们就可以完全搞清楚，为什么single-spa这么神奇了，接下来让我们搭建一个简易版的single-spa。

### 搭建single-spa

#### vue main

由于我们需要使用webpack配置，而最新版本的vue-cli默认只有babel，我们用这个步骤来安装一个vue版本的主应用

1、装包

```
 npm install @vue/cli @vue/cli-init  -g
```

2、创建一个项目

```
vue init webpack demo-single
```

3、进入目录

```
cd demo-single
```

4、装包

```
npm i single-spa single-spa-vue axios --save
```

5、在src目录创建一个single-spa配置文件 single-spa-config.js

```javascript
// single-spa-config.js
    import * as singleSpa from 'single-spa'; //导入single-spa
    import axios from 'axios'

    /*
        runScript：
        一个promise同步方法。可以代替创建一个script标签，然后加载服务
    */
    const runScript = async (url) => {
        return new Promise((resolve, reject) => {
            const script = document.createElement('script');
            script.src = url;
            script.onload = resolve;
            script.onerror = reject;
            const firstScript = document.getElementsByTagName('script')[0];
            firstScript.parentNode.insertBefore(script, firstScript);
        });
    };

    const getManifest = (url, bundle) => new Promise(async (resolve) => {
        const { data } = await axios.get(url);
        // eslint-disable-next-line no-console
        const { entrypoints } = data;

        for (let i = 0; i < entrypoints.length; i++) {
            await runScript('http://127.0.0.1:3000/' + entrypoints[i]).then(() => {
                if (i === entrypoints.length - 1) {
                    resolve()
                }
            })
        }
    });

    singleSpa.registerApplication( //注册微前端服务
        'singleDemoVue', async () => {
            let singleVue = null;
            await getManifest('http://127.0.0.1:3000/asset-manifest.json').then(() => {
                singleVue = window.singleReact;
            });
            return singleVue;    
        },
        location => location.pathname.startsWith('/react') // 配置前缀
    );

    singleSpa.start(); // 启动
```
**注： 可以看到，runScript就是个创建script标签的方法，getManifest是一个简单的获取manifest并创建script的方法**。

6、在main.js里引入这个文件

```
import './single-spa-config'
```

7、运行

```
npm run dev
```

最终得到这样一个工程

![avatar](https://raw.githubusercontent.com/macshion/PicBed/main/images/o_201130181531fc277894-9970-4acc-9170-0aef2e457fd5.png)

这样我们就完成了一个入口的配置，当然它还很简单，更复杂的操作我们应该放在具体的工程上去做。

#### react child

上面的代码可以看到，我们register了一个vue主应用并且访问了它的manifest文件，现在我们需要创建一个react子应用，也是直接通过几个步骤来完成，我们使用create-react-app来快速搭建：

1、装包

```
npm install create-react-app -g
```

2、创建

```
npx create-react-app my-app
```

3、创建完成后，注意我们需要对webpack做一点修改，默认create-react-app会有一个git本地分支，让我们先提交到本地仓库

```
git status
git add .
git commit -m ttt
```

4、拿到webpack配置文件，create-react-app默认隐藏了webpack配置文件

```
yarn eject 或 npm run eject
```

5、修改webpack文件
修改 /config/webpack.config.js 在output增加：

```
output: {
    ...这里忽略了原有的
    library: 'singleReact',
    libraryTarget: 'window'
}
```

![avatar](https://raw.githubusercontent.com/macshion/PicBed/main/images/o_2011301817110891255a-2940-44f5-a1b1-6bec5423c06d.png)

修改 /scripts/start.js文件，在 `const devServer = new ...` 这个地方，增加一个header的设置：

```javascript
const devServer = new WebpackDevServer(compiler, {
      ...serverConfig,
      // 这里上增加的header设置
      headers: {
        'Access-Control-Allow-Origin': '*',
      }
  
    });
```

![avatar](https://raw.githubusercontent.com/macshion/PicBed/main/images/o_20113018181813834fbd-2943-4980-aa4c-a0038b242b66.png)

6、修改src/index.js，要把root改为动态渲染，还要注册生命周期

```javascript
import React from 'react';
import ReactDOM from 'react-dom';
import './index.css';
import App from './App';
import reportWebVitals from './reportWebVitals';
import single-spaReact, {single-spaContext} from 'single-spa-react';

const rootComponent = () => {
  ReactDOM.render(
      <React.StrictMode>
        <App />
      </React.StrictMode>
    ,
    document.getElementById('react-root')
  );
}

// ReactDOM.render(
//   ,
//   document.getElementById('root')
// );


const reactLifecycles = single-spaReact({
  React,
  ReactDOM,
  rootComponent,
  errorBoundary(err, info, props) {
    // https://reactjs.org/docs/error-boundaries.html
    console.error(err)
    return (
      <div>This renders when a catastrophic error occurs</div>
    );
  },
});
export const bootstrap = reactLifecycles.bootstrap;
export const mount = reactLifecycles.mount;
export const unmount = reactLifecycles.unmount;


// If you want to start measuring performance in your app, pass a function
// to log results (for example: reportWebVitals(console.log))
// or send to an analytics endpoint。Learn more: https://bit.ly/CRA-vitals
reportWebVitals();
```

7、运行

```
npm run start
```

8、在main的vue那里，访问/react 你会看到下面有一个react渲染和vue的一起出现，大功告成

#### 生命周期

生命周期函数共有4个：bootstrap、mount、unmount、update。生命周期可以传入，返回Promise的函数也可以传入返回Promise函数的数组。
引用一个大佬完整的说明, 非常的详细：[https://github.com/YataoZhang/my-single-spa/issues/4](https://github.com/YataoZhang/my-single-spa/issues/4)

### 结论

single-spa可以给我们提供一整套方案，去搭建微前端集成框架，但它并不是一个开箱即用的封装，它有很多的坑等着我们去踩。
一般情况下，我们选择使用qiankun，它的封装程度更好，api更加友好一些。待积攒足够多的使用经验，可以考虑自研一套自己的微前端框架，增加整体的前端研发效率。下节我将给大家带来qiankun对single-spa的封装，在具体应用中的实践。待完结框架篇后，我们可以再深入探究single-spa的实现原理以及各种概念。

### 参考文章

single-spa 文档: [https://single-spa.js.org/docs/getting-started-overview/](https://single-spa.js.org/docs/getting-started-overview/)

微前端 single-spa: [https://juejin.cn/post/6844903896884707342](https://juejin.cn/post/6844903896884707342)

这可能是你见过最完善的微前端解决方案！: [https://www.infoq.cn/article/o6GxRD9iHQOplKICiDDU](https://www.infoq.cn/article/o6GxRD9iHQOplKICiDDU)

single-spa微前端: [http://www.soulapp.tech/2019/09/25/single-spa微前端/](http://www.soulapp.tech/2019/09/25/single-spa微前端/)

Single-Spa + Vue Cli 微前端落地指南 (项目隔离远程加载，自动引入) : [https://juejin.cn/post/6844904025565954055](https://juejin.cn/post/6844904025565954055)



## 微前端终篇：qiankun指南以及微前端整体探索

### qiankun原理和API介绍

qiankun是基于single-spa框架的一个上层应用，它提供了完整的生命周期，和一些钩子函数，通过路由匹配来动态加载注册微应用，同时提供了一系列api对微应用做管理和预加载等，它相对single-spa来说进步是比较大的。

所以---qiankun实质上是single-spa的一个封装，基于我们在上一节看到的，single-spa是通过输出一个manifest.json 通过标识入口信息动态构造script渲染实现的微前端应用，类似下面的图：

![image-20210225112744682](https://raw.githubusercontent.com/macshion/PicBed/main/images/image-20210225112744682.png)

回顾一下single-spa在渲染过程中的核心逻辑
1、 首先我们有 main（主app） child（子app），主app只有一个，子app可以有多个
2、 其次，主app上一般我们可以在index.html里面，写多几个空间，也就是多几个div

例如：

```html
<div id\=”react-app”\></div\>
<div id\=”vue-app”\></div\> 
```

3、然后，在我们的child上，要用webpack插件，生成一个带有所有需要加载的依赖文件的manifest.json

4、主应用去加载这个manifest.json，获取到具体的js，使用script标签把它放到主应用上，进行渲染

在qiankun中对这套逻辑做了基本的封装, 让我们只需要经过简单的几个api就可以控制single-spa中比较复杂的配置和概念。

#### **注册**

```javascript
import { registerMicroApps, start } from 'qiankun';
registerMicroApps([
  {
    name: 'react app', // 应用名称
    entry: '//localhost:7100', // 应用入口，应用需要增加cors选项
    container: '#yourContainer', // 应用单独的appid的div
    activeRule: '/yourActiveRule', // 匹配路由
  },
  {
    name: 'vue app',
    entry: { scripts: ['//localhost:7100/main.js'] },
    container: '#yourContainer2',
    activeRule: '/yourActiveRule2',
  },
]);
start();
```

#### main

main是一个qiankun的主体部分，它也是不限制框架种类的，可以用react也可以用vue和angular，只需要在entry.js里面注册它就可以了。

一般情况下main的作用是存放公共代码，例如：
1、消息触发器
2、公共路由
3、权限触发器
4、存放例如全局管理、皮肤、用户管理等公共页面

你也可以把站点的首页写在这里，可以加快主体加载速度

#### 生命周期

##### bootstrap

boostrap相当于init，子应用在第一次加载的时候会调用这个方法， 一般可以在里面做一些项目的初始化操作。

##### mount

每次在加载到子应用的时候都会调用它，就像是componentDidMount,一般情况下我们要把ReactDOM.render这样的初始化函数写在里面，每次mount时调用render。

##### unmount

这个跟mount正好相反，每一次注销/切换子应用的时候会调用它，一般我们在这里 ReactDOM.unmountComponentAtNode 注销这个应用，然后把整个项目的容器让出来

#### update

这是个可选的生命周期，子应用发生变化的时候会调用。

#### 路由匹配

路由规则有两种，需要手动调用对应的子应用渲染就行了，通过一个叫loadMicroApp的方法挂载一个子应用组件，这样就可以在main中像配置一个正常的应用那样配置子应用的view了。

```react
import { loadMicroApp } from 'qiankun';
import React from 'react';
class App extends React.Component {
  containerRef = React.createRef();
  microApp = null;
  componentDidMount() {
    this.microApp = loadMicroApp(
      { name: 'app1', entry: '//localhost:1234', container: this.containerRef.current, props: { name: 'qiankun' } },
    );
  }
  componentWillUnmount() {
    this.microApp.unmount();
  }
  componentDidUpdate() {
    this.microApp.update({ name: 'kuitos' });
  }
  render() {
    return <div ref={this.containerRef}></div>;
  }
}
```

#### 处理样式

##### 沙箱

qiankun的沙箱模式是在start的api配置项里面开启的。

sandbox 选项可选

```javascript
start({
  sandbox: true // true | false | { strictStyleIsolation?: boolean, experimentalStyleIsolation?: boolean }
})
```

默认情况下沙箱可以确保单实例场景子应用之间的样式隔离，但是无法确保主应用跟子应用、或者多实例场景的子应用样式隔离。当配置为 { strictStyleIsolation: true } 时表示开启严格的样式隔离模式。这种模式下 qiankun 会为每个微应用的容器包裹上一个 shadow dom 节点，从而确保微应用的样式不会对全局造成影响。
**shadow dom coco大神写过一篇文章介绍：[https://www.cnblogs.com/coco1s/p/5711795.html](https://www.cnblogs.com/coco1s/p/5711795.html)

##### 样式冲突解决方案

qiankun 会自动隔离微应用之间的样式（开启沙箱的情况下），你可以通过手动的方式确保主应用与微应用之间的样式隔离。比如给主应用的所有样式添加一个前缀，或者假如你使用了 ant-design 这样的组件库，你可以通过这篇文档中的配置方式给主应用样式自动添加指定的前缀。

以 antd 为例：

配置 webpack 修改 less 变量

```javascript
{
  loader: 'less-loader',
+ options: {
+   modifyVars: {
+     '@ant-prefix': 'yourPrefix',
+   },
+   javascriptEnabled: true,
+ },
}
```

配置 antd ConfigProvider

```react
import { ConfigProvider } from 'antd';
export const MyApp = () => (
  <ConfigProvider prefixCls="yourPrefix">
    <App />
  </ConfigProvider>
);
```

#### webpack配置的问题

微应用的打包工具还需要增加如下配置：

```javascript
const packageName = require('./package.json').name;
  module.exports = {
    output: {
      library: `${packageName}-[name]`,
      libraryTarget: 'umd',
      jsonpFunction: `webpackJsonp_${packageName}`,
    },
  };
```

### qiankun实践 - react微前端应用

起始，准备2个react应用，直接用create-react-app创建两个app应用，可以得到一个文件夹里有两个项目。

```
npx create-react-app main-app
npx create-react-app micro-app
```

我们用main做主应用，micro做子应用，按照我们的api，子应用只需要配置一个register就可以引入子应用。
**其中子应用需要调出webpack配置，create-react-app默认是不允许手动配置的，使用命令就可以了**。
进入micro-app的文件夹目录运行(create-react-app也有overload的办法更改配置，这里为了方便直接用命令调出来)：

```
npm run eject
```

这样项目的准备工作就做好了。

### 子应用配置

配置子应用两个步骤，一个是生命周期的配置。 我们把生命周期函数写好放到main.js中:

![image-20210225113127374](https://raw.githubusercontent.com/macshion/PicBed/main/images/image-20210225113127374.png)

然后把reactDom.render放到mount生命周期里调用，让qiankun在准备好加载mount的时候再去初始化应用：

![image-20210225113208656](https://raw.githubusercontent.com/macshion/PicBed/main/images/image-20210225113208656.png)

unmount的注销操作也不能忘记:

![image-20210225113250407](https://raw.githubusercontent.com/macshion/PicBed/main/images/image-20210225113250407.png)

我们更改一下子应用的根节点id，在父应用中再去引用它(不要忘了html里也需要更改):

![image-20210225113335581](https://raw.githubusercontent.com/macshion/PicBed/main/images/image-20210225113335581.png)

最后再把webpack中的配置修改一下：
1、修改devserver支持cors 修改端口
`headers: { 'Access-Control-Allow-Origin': '*', }`

![image-20210225113406029](https://raw.githubusercontent.com/macshion/PicBed/main/images/image-20210225113406029.png)

![image-20210225113433309](https://raw.githubusercontent.com/macshion/PicBed/main/images/image-20210225113433309.png)  
2、修改增加bundle的导出,在webpack.config.js增加配置：

![image-20210225113504237](https://raw.githubusercontent.com/macshion/PicBed/main/images/image-20210225113504237.png)

### 父应用配置

然后我们就可以去在main应用中，注册了首先要

```
npm install qiankun --save
```

然后在main文件index.js中注册子应用：

![image-20210225113612030](https://raw.githubusercontent.com/macshion/PicBed/main/images/image-20210225113612030.png)


别忘了我们还需要在public/index.html中写一个div容器，id是我们子应用的那个id，用来承载子应用的渲染:

![image-20210225113650792](https://raw.githubusercontent.com/macshion/PicBed/main/images/image-20210225113650792.png)

然后我们就可以开始运行看一看了:

![image-20210225113731843](https://raw.githubusercontent.com/macshion/PicBed/main/images/image-20210225113731843.png)

运行成功，随便改一下micro的样式看看效果：

![image-20210225113803662](https://raw.githubusercontent.com/macshion/PicBed/main/images/image-20210225113803662.png)


接下来我们需要处理一下路由跳转的问题。

### 路由的处理实践

前文有提到，在react中使用qiankun可以使用apiloadMicroApp,这里我们也用它来处理路由的跳转。
我们主要是在main-app中操作：
首先新建micro-app的view文件（每多一个子应用就新建一个）：

![image-20210225113839377](https://raw.githubusercontent.com/macshion/PicBed/main/images/image-20210225113839377.png)

然后使用react-router直接配置：
由于create-react-app默认没有直接提供react-router，我们手动下一个

```
npm install react-router react-router-dom --save
```

改完index.js长这样：

![image-20210225113942064](https://raw.githubusercontent.com/macshion/PicBed/main/images/image-20210225113942064.png)


再试一下：

![image-20210225114020401](https://raw.githubusercontent.com/macshion/PicBed/main/images/image-20210225114020401.png)

大功告成！ 

### 结论和源码

相比较上一次我们看见的 single-spa的配置要简单了很多，而且更加直白，新增子应用更加无缝。  
需要demo源码的同学私信我哦

#### 应用场景和坑:静态资源问题解决

微应用打包之后 css 中的字体文件和图片加载如果使用的加载路径是相对路径，会导致css 中的字体文件和图片加载 404。

而 css 文件一旦打包完成，就无法通过动态修改 publicPath 来修正其中的字体文件和背景图片的路径。

主要有三个解决方案：

- 所有图片等静态资源上传至 cdn，css 中直接引用 cdn 地址（推荐）
- 借助 webpack 的 url-loader 将字体文件和图片打包成 base64（适用于字体文件和图片体积小的项目）（推荐）
- 使用绝对地址，nginx中设置静态目录

#### 结束语

qiankun整体的思路是比较ok的，它大大简化了single-spa的使用逻辑，让微前端的门槛变得更低，但它仍然有一些缺点，例如部分api总是会有莫名其妙的问题、api文档不是特别直观等，这些都是待改进的地方。而对于微前端来说，做到能够技术栈无关、渐进升级旧项目、分离不同业务等功能就已经能发挥它的最大价值了。