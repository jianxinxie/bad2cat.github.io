---
title: 部署Hexo到Github pages（2）
date: 2022-03-16 15:01:54
tags:
- hexo
- 个人博客搭建
category:
- 博客搭建
---

完成上面的操作之后，博客系统就可以在本地进行访问了；但是如果想将博客系统放到公网，可以将 `Hexo`部署到`Github Pages`上

<!-- more -->

#### 将 Hexo 部署到 GitHub Pages

`GitHub Pages`就是一个免费的静态网站托管和发布平台，提供了两种托管的方式：

- 通过 `Github`个人或者企业账号托管，这种情况下每个`Github`账号只能托管一个，并且`Repository`的名称必须为`username.github.io`
- 通过`project`托管，这样每个`project`都可以托管一个静态网站，在这种情况下，默认托管在`gh-pages`分支下面

具体可以参考[Github pages官网](https://pages.github.com/)，当然使用`github pages`也会有一些限制，比如：

- 发布的`Git Pages`站点不超过`1GB`
- 每月带宽限制为`100GB`或`100,000`次请求
- 每小时限制构建次数不超过`10`次

