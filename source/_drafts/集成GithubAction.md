---
title: 搭建个人博客(5) - 集成GithubAction
date: 2022-03-17 18:33:35
tags:
- hexo
- 个人博客搭建
category:
- 博客搭建
---

这样，博客已经搭建好了，可以在本地的根目录下通过命令创建博客，如下：

```
hexo new post 'Fisrt Blog'
```

执行完命令之后就会在`Blog/source/_posts`下面生成一个`md`文档了，然后在该文档中写入想发表的内容之后保存；同样的执行命令：

```
hexo clean
hexo g
hexo d
```

然后就可以发布博客到`Github`了，通过之前购买的域名刷新就可以看到发表的博客了；如果每次都这样写博客会很难受，并且如果更换了电脑，需要重新再打造之前的环境了。那如何解决这个问题呢？

<!-- more -->

#### Hexo 持续集成`GithubAction`

为了能够在各个地方都很容易的发表博客，那就需要实现`Hexo`持续集成；现在有两种集成的方式：

##### 持续集成 `Travis CI`

这种方式可以参考，Hexo [官方文档](https://hexo.io/zh-cn/docs/github-pages)

##### 持续集成 `Github Action`

说明：Github Action 是`Github` 的一种执行任务的脚本，将`hexo`持续集成`Gihub Action`之后，需要将本地的博客系统`push`到`Github`的一个仓库中（也可以是仓库`<username>.github.io`的一个分支）；之后每次写博客时，只需要将这个博客系统拉到本地，写完之后`push`上去即可，脚本`Github Actions`就会自动发布博客的更新

下面就介绍使用`Github Action`持续集成的例子

1. ###### 添加仓库

   本文选择将博客系统推送的一个新的分支，所以需要创建一个新的仓库，可以将这个仓库设置为`private`，因为没必要让别人看到博客的源码，新建的仓库为`blog`

2. ###### 推送源码，设置 secret

   在本地的跟目录下面，打开`git bash`界面，将本地的源码推送到`blog`仓库；

   注：在这里要注意一点，之前下载主题是，在主题那个文件夹会有一个`.git`隐藏文件，在你推送之前一定要把这个`.git`文件删除掉，否则推送上去之后主题就会失效

   接下来，打开`blog`仓库的`setting`，添加`secret`，如下：

   ![01](D:\我的\github\blog\source\_drafts\集成GithubAction\01.png)

   此时需要为`Github`生成一对公私密钥，[参考这里](https://www.cnblogs.com/yuqiliu/p/12551258.html)，点击添加之后，`key`为`ACCESS_TOKEN`，值就是生成的私钥

3. ###### 设置 Deploy keys

   1. 打开仓库`<username>.github.io`，打开`setting`，选择`Deploy keys`添加，`key`为`ACTIONS_DEPLOY_KEY`,值就是刚才生成的公钥，如下：

      ![02](D:\我的\github\blog\source\_drafts\集成GithubAction\02.png)

      注：如果是在同一个仓库的不同分支则可以使用`Github Personal Token`，因为这是在不同仓库所以只能使用公私密钥

4. ###### 添加`Github Action`脚本

   最后，就是添加`GithubAction`脚本在`blog`仓库当中了，打开`blog`仓库，点击到`Action`，新建`Action`脚本

   ![03](D:\我的\github\blog\source\_drafts\集成GithubAction\03.png)

   脚本的内容如下所示：

   ```
   name: Github Pages
   on:
     push:
       branches:
         - main # main 分支 push 行为时就触发这个 action
     pull_request:
   
   jobs:
     build-and-deploy:
       runs-on: ubuntu-latest
       concurrency:
         group: ${{ github.workflow }}-${{ github.ref }}
       steps:
         - uses: actions/checkout@v2
         
         - name: Setup Node
           uses: actions/setup-node@v2
           with:
             node-version: '16'
             
         - name: Cache dependencies
           uses: actions/cache@v2
           with:
             path: ~/.npm
             key: ${{ runner.os }}-node-${{ hashFiles('**/package-lock.json') }}
             restore-keys: |
               ${{ runner.os }}-node-
         - run: npm ci
         - run: npm run build
         
   
         - name: Deploy
           uses: theme-keep/hexo-deploy-github-pages-action@master 
           env:
             PERSONAL_TOKEN: ${{ secrets.ACCESS_TOKEN }}
   
              # The repository the action should deploy to.
             PUBLISH_REPOSITORY: bad2cat/bad2cat.github.io //这就是push 到博客仓库
   
             # The branch the action should deploy to.
             BRANCH: main   //push 到那个分支
   ```

5. 重新部署

   现在到本地的博客根目录下，新建一个博客，然后直接将博客源码推送到`blog`仓库，然后就会触发这个脚本了，这个脚本的作用就是把博客的内容部署到`<username>.github.io`仓库下面，等一会刷新页面就可以看到部署的结果了