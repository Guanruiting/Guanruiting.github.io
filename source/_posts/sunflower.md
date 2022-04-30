---
title: 用HTML+CSS画一朵向日葵
date: 2019-04-16 21:57:36
tags:
- CSS
- HTML
categories: 中文
---

某日深夜，一时兴起，想用CSS画画，撸了两三个小时，才有了这一幅向日葵，可以说是我的处女作了。

<!-- more -->

![向日葵](/img/2019/04/sunflower.png)

HTML代码：

```html
<html>
    <head>
        <title>Sunflower</title>
        <meta charset="utf-8"/>
        <link href="style.css" rel="stylesheet"/>
    </head>
    <body>
        <div id=wrap>
            <div class="flower f1">
                <!-- 脸 -->
                <div class="face">
                    <div class="eye"></div>
                    <div class="eye"></div>
                    <div class="mouth">
                        <div class="red"></div>
                        <div class="left"></div>
                        <div class="right"></div>
                    </div>
                </div>
                <!-- 花瓣 -->
                <div class="huaban">
                    <div class="piece1 p1"></div>
                    <div class="piece1 p2"></div>
                    <div class="piece1 p3"></div>
                    <div class="piece1 p4"></div>
                    <div class="piece1 p5"></div>
                    <div class="piece2 p6"></div>
                    <div class="piece2 p7"></div>
                    <div class="piece2 p8"></div>
                    <div class="piece2 p9"></div>
                    <div class="piece2 p10"></div>
                    <div class="piece3 p11"></div>
                    <div class="piece3 p12"></div>
                    <div class="piece3 p13"></div>
                    <div class="piece3 p14"></div>
                    <div class="piece3 p15"></div>
                    <div class="piece4 p16"></div>
                    <div class="piece4 p17"></div>
                    <div class="piece4 p18"></div>
                    <div class="piece4 p19"></div>
                </div>
                <!-- 枝叶 -->
                <div class="green">
                    <div class="left"></div>
                    <div class="right"></div>
                </div>
            </div>
        </div>
    </body>
</html>
```

CSS代码：

```CSS
*{margin:0;padding:0;}
html,body,#wrap{height:100%;}
#wrap{background: -webkit-linear-gradient(top, #73b2f9, #0b6602);position: relative;}
.flower{position:relative;}
.f1{width:260px;height:350px; top:30%;left:300px;}
.face{position:relative;width:200px;height: 150px;z-index:100;margin:0 auto;top:25px;border-radius: 50%;border:1px solid #823605;background: -webkit-linear-gradient(top,#f8dcc4, #f9d2c3,#fbd1c5,#f0bbb3,#f88d79);}
.eye{width:26px;height:46px;position:absolute;top:30px;background:-webkit-linear-gradient(top, #43354c, #1f1e2e);border-radius:12px/23px;}
.eye::before{content:"";position: absolute;width:10px;height:10px;background-color:#fff;left:4px;top:7px;border-radius:5px;}
.eye:first-child{left:60px;}
.eye:nth-child(2){right:60px;}
.mouth{width:120px;height:60px;border-radius:50%;border-bottom: 30px solid #282433;position:absolute; bottom:20px;left: 50%;transform: translateX(-50%)}
.mouth .red{width:44px;height:2px;position:absolute;left:38px;bottom:-31.5px;border-top:20px solid #f1548b;border-radius:50%;}
/* 叶子 */
.green{height:200px;width:15px;position:absolute;left:120px;bottom:0;z-index:0;background:-webkit-linear-gradient(left, #1e9658, #8dc79f);border-left:1px solid #823605;border-right:1px solid #823605;}
.green .left,.green .right{width:150px;height:70px;position:absolute;border-radius:50%;left:0;top:90px;background:-webkit-linear-gradient(left, #1e9658, #8dc79f);}
.green .right{width:130px;height:56px;left:-125px;top:70px;}
/* 花瓣 */
.huaban{width:260px;height: 200px;position:absolute;top:0;z-index:1;}
.huaban [class*="piece"]{background: #f6f543;position:absolute;border:1px solid #823605;}
.piece1{width:30px;height:50px;border-radius:100% 100% 0 0/100%;}
.piece2{width:50px;height:30px;border-radius:0 100% 100% 0/50%;}
.piece3{width:30px;height:50px;border-radius:0 0 100% 100%/100%;}
.piece4{width:50px;height:30px;border-radius:100% 0 0 100%/100%;}
.piece1:before{content:"";position:absolute;width:1px;height:10px;background-color:#823605;bottom:17px;left:15px;}
.piece2:before{content:"";position:absolute;width:10px;height:1px;background-color:#823605;left:17px;top:15px;}
.piece3:before{content:"";position:absolute;width:1px;height:10px;background-color:#823605;top:17px;left:15px;}
.piece4:before{content:"";position:absolute;width:10px;height:1px;background-color:#823605;right:17px;top:15px;}
.p1{left:113px;top:-8px}
.p2{left:83px;top:-5px}
.p3{left:53px;top:10px}
.p4{left:143px;top:-5px}
.p5{left:174px;top:5px}
.p6{left:193px;top:42px;}
.p7{left:203px;top:67px}
.p8{left:203px;top:90px}
.p9{left:206px;top:116px}
.p10{left:183px;top:140px;}
.p11{bottom:-5px;left:113px;}
.p12{bottom:-5px;left:83px;}
.p13{bottom:-5px;left:143px;}
.p14{bottom:4px;left:173px;}
.p15{bottom:5px;left:53px;}
.p16{bottom:38px;left:18px;}
.p17{bottom:65px;left:0;}
.p18{bottom:95px;left:3px;}
.p19{top:44px;left:12px;}
```

