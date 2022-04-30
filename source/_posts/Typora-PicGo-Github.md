---
title: Markdown写作自动上传图片至Github - Typora编辑器 + PicGo河床
date: 2020-12-16 18:09:27
tags:
- Tools
categories: 中文
---

使用Typora+PicGo可以在Markdown写作过程中非常方便快速地插入图片。

<!--more-->

## 一、下载并设置PicGo

下载地址：[https://github.com/Molunerfinn/PicGo/releases](https://github.com/Molunerfinn/PicGo/releases)

设置PicGo，支持多个图床，我这里用Github：

![image-20201216172510671](https://raw.githubusercontent.com/macshion/PicBed/main/images/image-20201216172510671.png)

仓库名：Github用户名/Repo名

分支：一般为master或者main

指定存储路径：可不填，如果指定路径后上传失败，需要亲手创建文件夹

设定自定义域名：参考设置 https://raw.githubusercontent.com/macshion/PicBed/main

Token:  获取Github Token方法如下：

1、点击Github头像，选择 "setting", 点击左侧菜单进入 “Developer settings”，然后进入 “Personal access tokens”，在页面右上角点击 “Generate new token” 。

![](https://raw.githubusercontent.com/macshion/PicBed/main/images/screenshot.jpg)2、新建Token，勾选权限，生成Token后需复制保存好，未保存好以后要用只能重新生成。

![image-20201216175246455](https://raw.githubusercontent.com/macshion/PicBed/main/images/image-20201216175246455.png)

##  二、下载并设置Typora

从官网下载Typora：[https://typora.io](https://typora.io/)

打开Typora，进入“文件 - 偏好设置” 设置通过PicGo自动上传图片。

![image-20201216180402765](https://raw.githubusercontent.com/macshion/PicBed/main/images/image-20201216180402765.png)

## 参考：

[使用GitHub+PicGo自建免费图床](https://juejin.cn/post/6844904078468710413)

[Typora+PicGo配置最强Markdown编辑工具](https://juejin.cn/post/6844904095132680206)

[PicGo+GitHub：你的最佳免费图床选择！](https://www.cnblogs.com/shwee/p/11421336.html)

[图床的高效使用：Typora + OSS + PicGo](https://juejin.cn/post/6900967054967308302)


