# Guanruiting.github.io
我的博客，建于2019年3月25日凌晨3点

《记录Hexo搭建GitHub博客的步骤》: http://localhost:4000/20190416/build-a-blog-by-Hexo/

## 常用操作
### 添加一篇文章
```
hexo new "My New Post"
```
### 添加一篇草稿
```
hexo new draft 'A New Draft'
```
### 发布一篇草稿
```
hexo publish [layout] <title>
// 比如
hexo publish post 'How to Learn English'
```
### 置顶文章
Add `top: true` to the top of the post you want

### 启动本地服务
```
hexo server
```

### hexo分支备份代码
```
git add .
git commit -m "注释"
git push origin hexo

```

### 部署网站
```
hexo g -d
```

### 拉取代码到本地
```
git clone <hexo分支>

npm install hexo

npm install

npm install hexo-deployer-git

// 记得，不需要hexo init这条指令
```
