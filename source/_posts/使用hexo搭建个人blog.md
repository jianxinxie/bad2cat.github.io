---
title: 搭建个人博客（1）- 初始化博客
date: 2022-03-16 15:01:51
tags:
- hexo
- 个人博客搭建
category:
- 博客搭建
---

最近想着搭建一个个人博客，然后在网上找到了几种搭建个人博客的方式：

##### 静态网站生成器

这种就是在终端使用`hexo,hugo,Jekyll`等工具，生成一个博客系统，然后通过`Github pages`进行展示

优点：可以自己选择博客主题，并且有很多插件实现评论、搜索、流量统计等功能

缺点：没有后台管理系统，需要自己在本地写完之后，发布到`github pages`上；当然，如果集成`github Actions`之后，每次写完只需要推送到`github`就可以了

<!-- more -->

##### 内容管理系统

如：Wordpress，Ghost等，这种更多是企业级的应用，也可以搭建个人博客

这种博客是带有后台管理系统的，但是需要配置数据库、域名和服务器等，这些花费会比较大

##### 第三方平台

最简单就是使用第三方平台，如：掘金，简书等；并且会有站点的推广，当然也会受到平台的一些限制

#### Hexo 搭建个人博客

下面主要介绍通过`hexo`来搭建个人博客，同时添加`pure`作为该博客系统的主题，主题的样式可以看一下如下的`demo`

[hexo-pure 主题 demo]()

##### 搭建个人博客前提

- 一个`Github`的账号，因为现在`Github`不再支持账密操作了，所以你还需要生成一个`Github Personal Token`，生成方式：

  [Github不支持账密操作的解决方案]()

- 本地安装 `Git`

  - Windows：下载并安装 [git](https://git-scm.com/download/win).
  - Mac：使用 [Homebrew](http://mxcl.github.com/homebrew/), [MacPorts](http://www.macports.org/) 或者下载 [安装程序](http://sourceforge.net/projects/git-osx-installer/)。
  - Linux (Ubuntu, Debian)：`sudo apt-get install git-core`
  - Linux (Fedora, Red Hat, CentOS)：`sudo yum install git-core`

- 安装 Node.js

  [node.js 详细安装步骤](https://blog.csdn.net/antma/article/details/86104068)

##### 安装 Hexo

完成上面的操作之后，右键打开`Git Bash，`输入如下命令安装`hexo`：

```
npm install -g hexo-cli
```

##### 建站

通过上面的命令安装好`hexo`之后，就可以使用`hexo`的命令建站了，使用命令

```
hexo init <folder>
cd <folder>
npm install
```

执行完成之后，打开新建的目录，可以看到如下的目录列表：

```
.
├── _config.yml  //站点配置文件
├── package.json // npm 的依赖列表
├── scaffolds    // 文章模板
├── source      //这个下面就是具体的文章了
|   ├── _drafts  //草稿箱
|   └── _posts   // 发布的列表
└── themes       // 当前博客支持的主题，默认只有一个 landscape
```

此时，已经生成了一个静态的博客系统，可以通过如下的命令来访问本地搭建的博客

1. `hexo g`：生成静态文件
2. `hexo d`：部署网站
3. `hexo server`：在本地启动服务

然后在浏览器中输入`http://localhost:4000/`就可以访问本地搭建的博客系统了
