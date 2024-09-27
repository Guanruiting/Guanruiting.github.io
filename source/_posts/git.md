---
title: git config配置用户
date: 2019-04-17 22:14:10
tags:
- Git
category: 中文
---

用户配置

```
git config --global user.name "name"
git config --global user.email 123@xxx.com
```

配置级别

`--local` [默认]：优先级高，只影响本仓库

`--global` [中优先级]：影响到所有当前用户的git仓库

`--system` [低优先级]：影响到全系统的git仓库



