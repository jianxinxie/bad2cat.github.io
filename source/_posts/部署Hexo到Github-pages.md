---
title: 搭建个人博客（2）- 部署Hexo到Github pages
date: 2022-03-16 15:01:54
tags:
- hexo
- 个人博客搭建
category:
- 博客搭建
---

完成上面的操作之后，博客系统就可以在本地进行访问了；但是如果想将博客系统放到公网，可以将 `Hexo`部署到`Github Pages`上。

<!-- more -->

#### 将 Hexo 部署到 GitHub Pages

###### GithubPages 说明

`GitHub Pages`就是一个免费的静态网站托管和发布平台，提供了两种托管的方式：

- 通过 `Github`个人或者企业账号托管，这种情况下每个`Github`账号只能托管一个，并且`Repository`的名称必须为`username.github.io`
- 通过`project`托管，这样每个`project`都可以托管一个静态网站，在这种情况下，默认托管在`gh-pages`分支下面

具体可以参考[Github pages官网](https://pages.github.com/)，当然使用`github pages`也会有一些限制，比如：

- 发布的`Git Pages`站点不超过`1GB`
- 每月带宽限制为`100GB`或`100,000`次请求
- 每小时限制构建次数不超过`10`次

我选择使用`Github`个人账号托管博客，下面就是详细的将本地`Hexo`部署到 `GitHub Pages`的步骤

###### 1. 在 `Github`创建仓

登录到 [Github](https://github.com/)，创建仓库

![01](.\部署Hexo到Github-pages\01.png)

这个仓库必须创建为`public`的，仓库的名称就是`<username>.github.io`，`username`就是你`Github`的账号

###### 2. 更改 Hexo 配置

现在进入`hexo`博客的根目录，打开根目录下的配置文件`_config.yml`

![02](.\部署Hexo到Github-pages.\02.png)

打开之后，滑倒文件底部，找到`deploy`属性，这一块的内容更改为：

```
deploy:
  type: git
  repository:  #你的仓库地址
  branch: main
```

更改之后的结果如下所示：

![03](.\部署Hexo到Github-pages.\03.png)

###### 3. 发布到`GithubPages`

完成上面的操作之后，在根目录打开`git bash`，安装部署插件命令如下：

```
npm install hexo-deployer-git --save
```

安装完成之后，输入一下三条命令进行部署

```
hexo clean   #清除缓存文件 db.json 和已生成的静态文件 public
hexo g       #生成网站静态文件到默认设置的 public 文件夹(hexo generate 的缩写)
hexo d       #自动生成网站静态文件，并部署到设定的仓库(hexo deploy 的缩写)
```

完成之后，就可以发现在`<username>.github.io`仓库中已经有内容了，说明`hexo`博客已经成功的部署到`github`上了，接下来在浏览器中输入`https://<username>.github.io`，就可以看到刚才部署的博客了