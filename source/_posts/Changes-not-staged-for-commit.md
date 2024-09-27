---
title: 使用“git add .”命令提交代码后仍报错：“Changes not staged for commit”
date: 2019-04-16 03:33:29
tags:
- Git
- Github
category: 中文
---

github仓库，本地删除了文件，使用  ` git add . `  命令提交代码后仍报错：

<!-- more -->

```

On branch master
Your branch is up to date with 'origin/master'.
Changes not staged for commit:

(use "git add/rm <file>..." to update what will be committed)

(use "git checkout -- <file>..." to discard changes in working directory)

  deleted:    ../test
  
no changes added to commit (use "git add" and/or "git commit -a")

```



最后指定报错的的文件解决了：


```
git add ../test
git commit -m 'delete test'

```