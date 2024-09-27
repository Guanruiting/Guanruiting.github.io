---
title: 基于jQuery开发一个图片懒加载插件
date: 2019-05-25 20:40:44
tags:
- jQuery
- Javascript
category: 中文
---

图片懒加载（LazyLoad）一直是前端的优化方案之一。

其核心思想是：先将img标签中的src链接设为同一张图片，真正的图片地址存储在img标签的自定义属性中。当js监听到该图片元素进入可视窗口时，将自定义属性中的地址存储到src属性中。

<!-- more -->

如何基于jQuery开发一个图片懒加载插件？下面是我做的一个DEMO。 [下载demo](/down/imgLazyLoad.zip)

***记得引入jQuery***

##### HTML

```html
<!DOCTYPE html>
<html>
    <head>
        <title>图片懒加载</title>
        <meta charset="utf-8"/>
        <script src="jquery-1.12.4.js"></script>
        <script src="lazyload.js"></script>
    </head>
    <body>
        <div id="box1">
            <img src="loading.gif" data="1.jpg"/><br>
        </div>
        <div id="box2">
            <img src="loading.gif" data="1.jpg"/><br>
            <img src="loading.gif" data="2.jpg"/><br>
            <img src="loading.gif" data="3.jpg"/><br>
            <img src="loading.gif" data="4.jpg"/><br>
            <img src="loading.gif" data="5.jpg"/><br>
            <img src="loading.gif" data="6.jpg"/><br>
            <img src="loading.gif" data="7.jpg"/><br>
            <img src="loading.gif" data="1.jpg"/><br>
            <img src="loading.gif" data="2.jpg"/><br>
            <img src="loading.gif" data="3.jpg"/><br>
            <img src="loading.gif" data="4.jpg"/><br>
            <img src="loading.gif" data="5.jpg"/><br>
            <img src="loading.gif" data="6.jpg"/><br>
            <img src="loading.gif" data="7.jpg"/><br>
            <img src="loading.gif" data="1.jpg"/><br>
            <img src="loading.gif" data="2.jpg"/><br>
            <img src="loading.gif" data="3.jpg"/><br>
            <img src="loading.gif" data="4.jpg"/><br>
            <img src="loading.gif" data="5.jpg"/><br>
            <img src="loading.gif" data="6.jpg"/><br>
            <img src="loading.gif" data="7.jpg"/><br>
            <img src="loading.gif" data="1.jpg"/><br>
            <img src="loading.gif" data="2.jpg"/><br>
            <img src="loading.gif" data="3.jpg"/><br>
            <img src="loading.gif" data="4.jpg"/><br>
            <img src="loading.gif" data="5.jpg"/><br>
            <img src="loading.gif" data="6.jpg"/><br>
            <img src="loading.gif" data="7.jpg"/>
        </div>
    </body>
    <script>
        // 页面所有图片懒加载，默认延迟500毫秒
        //$('body').imgLazyLoad()

        // 指定容器里的图片懒加载，传参设置延迟毫秒数
        $("#box1").imgLazyLoad(100);
        $("#box2").imgLazyLoad(1000);
    </script>
</html>
```

##### lazyload.js
```javascript
 (function($) {
     function showImg(timer){
        var winHeight = $(window).height()
        var scrollHeight = $(window).scrollTop()
        var t = timer||500
        var imgs = $('img[data]')
        this.find(imgs).each(function() {
            if(($(this).offset().top < winHeight + scrollHeight)&&!$(this).attr("loaded")){
                setTimeout(()=>{
                    $(this).attr('src', $(this).attr('data'));
                    $(this).attr('loaded', "true");
                },t)
            };
        })
     }
     $.fn.extend({
         "imgLazyLoad":function(timer){
            var el = this
            showImg.call(el,timer);
            $(window).on('scroll',function(){
                showImg.call(el,timer);
            })
        }
     })
})(jQuery);
```