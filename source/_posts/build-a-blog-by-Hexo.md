---
title: 简单记录Hexo搭建GitHub博客的步骤
date: 2019-04-16 01:58:09
tags:
- Hexo
- Github
category: 中文
---


简单记录下Hexo搭建GitHub博客的步骤：

（nodejs、git安装的前提下）

1、Github新建账号同名Repo，设置Repository name为：账号名.github.io

2、创建Hexo分支并设为默认分支，用来存放网站的原始文件、备份，master分支用来存放生成的静态网页

<!-- more -->

3、设置ssh

4、git clone Hexo分支到本地

5、进入目录执行以下命令

 ```
 npm install hexo
 npm install -g hexo-cli
 
 hexo init
 
 npm install
 
 npm install hexo-deployer-git
 
 ```

提示：如果执行 ` hexo init ` 命令时报文件夹不能为空的错误，可以先在本地一个空文件夹执行第一、二条命令，执行完后把文件夹里的东西拷贝过来再往下执行

6、修改_config.yml中的deploy参数，为master

### 7、Hexo分支执行以下命令提交代码以备份(常用)

```
git add .
git commit -m "注释"
git push origin hexo

```
### 8、执行以下命令生成网站并部署到GitHub（常用）

 ```
 hexo g -d
 ```


------------------------华丽丽的分割线-------------------------

如果想在其他电脑上修改博客，可以使用下列步骤：

- 使用git clone 拷贝仓库（默认分支hexo）

- 在本地新拷贝的文件夹下通过Git bash依次执行下列指令：


```
npm install hexo

npm install

npm install hexo-deployer-git

// 记得，不需要hexo init这条指令

```