---
title: First Step to Establish the Blog
categories: Note
tags:
  - Tools
---

让我们搭一个美美的博客，一起写写写吧~~~

<!-- more --> 

## Requirement

​	brew, hexo, Node.js

### Hexo项目

``` bash
$ hexo init           # 新建博客目录
$ hexo new "postname" # 生成postname.md文件
$ hexo clean          # 清空生成的网页
$ hexo generate       # 根据当前目录下文件生成静态网页
$ hexo server 	      # 启动服务器
```

通过访问localhost:4000可以在本地调试。文件目录`source`下的`_posts`中可以添加用户新增加的博客内容（Markdown语法）。

More info: [Heox](https://hexo.io/docs/)

### 修改主题

``` bash
$ git clone https://github.com/theme-next/hexo-theme-next themes/next
```

修改`Hexo`目录下的`config.yml`配置文件中的theme属性，将其设置为next。另外常见的Next主题中常见的属性：
``` bash
auto_excerpt:   # 可通过 <!-- more --> 标签自动截断, 增加阅读全文按钮。
  enable: true
  length: 150

busuanzi_count: # 监听网页浏览量。
  enable: true
```

### 添加新的导航栏

``` bash
$ hexo new page tags   # 添加tags标签页
```

修改`source`目录下的`tags`中的`index.md`如下：

```
---
title: tags
date: 2018-10-30 17:23:49
type: "tags"
---
```

在菜单中添加链接。编辑`Hexo`目录下的`config.yml`配置文件中的menu属性，如下：

```
menu:
  home: /
  archives: /archives
  tags : /tags
```

### 部署到github

修改`Hexo` 目录下的`config.yml` 配置文件中的deploy属性：

``` bash
deploy:
  type: git 
  repo: https://github.com/test/test.github.io.git  # github路径
```

通过下面的指令实现部署：
``` bash
$ npm install hexo-deployer-git --save
$ hexo deploy
```

### Google收录博客网站



skip_render: google10bb50e0b38f396b.html



