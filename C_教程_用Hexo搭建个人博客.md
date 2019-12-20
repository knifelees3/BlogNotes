---
title: 用Hexo搭建个人博客
date: 2019-03-01 18:11:45
tags:
- Git
categories:
- 技术
---
## Motivation

（闲扯，无关技术）
从2016年接触github之后，就有写一个自己的博客的想法。目前市面上的博客平台也还是有很多的，比如新浪博客、豆瓣、知乎专栏、CSDN、博客园、简书....
这些网站各有优劣，而且侧重点不同。有的偏技术，比如CSDN、博客园，有的很文艺，比如豆瓣、新浪博客，有的更加具有严谨性和学术性，比如知乎。我的要求是：

1. 要可以记录一些自己安装软件、学习软件的教程，所以要对代码高亮支持的很好。
2. 可以写一下自己的随笔、感悟。
3. 可以写自己对学术问题的思考，比较浅显的思路那种。

想来想去还是你自己搭建一个博客吧，这些功能都可以实现，网上搜索了很多搭建个人博客的例子，有用wordpress的，有用python的，提到的最多的就是github.一步步按照注册、安装，最开始的jkelly实现，老是报错和失败，就放弃了。 
去年过年回去比较闲，又开始捣鼓，生命不息、捣鼓不止。。。。尝试打算用Python，被一篇文章吸引https://blog.csdn.net/BF02jgtRS00XKtCx/article/details/81611904
由于这种方法需要一些python的库，而且编译需要c++14,我不想再笔记本装太多东西，选择放弃。
开始尝试Hexo，还详细比较了Jkelly和Hexo的区别。真的不想再弄jkelly了,不记得耽误了多久的时间依然各种报错。。。Hexo搭建主要借助了知乎上的一篇文章：
https://zhuanlan.zhihu.com/p/26625249
这篇文章讲的很细致，实现基本的功能很快，后来为了捣鼓评论、背景图片，又花了很久。总共花了有三天，慢慢的把网站弄好了，功能也更加齐全，在这里将做的过程以及中间遇到的问题详细列下来，希望对自己、对别人都会有帮助~
（2019 03 01 今天就写到这里吧，慢慢补充）

## 准备工作

### 下载cmder

cmder是一款可以在windows系统输入linux命令的软件，我们直接在官网下载安装，
https://cmder.net/
我下载的是含有git的版本，文件较大，下载下来之后，解压放在一个不需要管理员权限的位置，然后将对应的路径添加到环境变量，就可以“win+R”里输入cmder打开了，不过这还不方便，我们希望也可以像ubuntu一样，右键之后在当前文件夹打开，此时需要管理员权限运行cmd，输入

```bash
Cmder.exe /REGISTER ALL
```

这样Cmder就配置完成了.

### 安装Hexo

我们使用Hexo来生成静态网页，为了安装Hexo，我们需要首先安装node.js:
https://nodejs.org/en/download/
下载安装之后，可以在命令行（Win+R然后输入CMD）用

```bash
node -v
npm -v
```

来查看版本，确定node.js和npm是否安装成功。接下来安装Hexo,同样在命令行里面输入

```bash
npm install -g hexo-cli 
```

安装好之后，我们就可以找文件夹创建网页了。

## 基本功能的实现

### 创建网页部署在本地

有了Hexo，此时选择一个我们打算用来放网站的文件夹，命令行中输入

```bash
hexo init blog
```

就会生成一个名字为"blog"的文件夹，打开这个文件夹，我们会发现里面已经有了基本的文件，暂时不管每个文件的功能，在blog文件夹里面输入

```bash
hexo g
```

就会生成一个静态的网页，再输入

```bash
hexo s
```

就会将静态博客部署再本地了，打开浏览器，输入地址：http://localhost:4000/ 就可以查看预览网页了。此时我们可以尝试插件一篇文章

```bash
hexo new <文章名字>
```

此时查看站点文件夹source目录的_post文件夹，可以看见已经多了一个<文章名字>.md的文件，稍微编辑下，就可以浏览器看到了。

## 部署到github

### 设置github

上面的静态的网页需要部署到网络上别人才可以访问，我们选用github来托管。首先当然是注册github,注册之后，添加一个Repositories,命名为"<你的github用户名>.github.io".注册好之后，我们就可以用来托管我们的网页了。前面我们安装的cmder已经安装了git,为了可以使用git,我们还需要初始化git,设置user.name和user.email配置信息,打开cmder,输入

```bash
git config --global user.name "你的GitHub用户名"
git config --global user.email "你的GitHub注册邮箱"
```

生成ssh密钥文件

```bash
ssh-keygen -t rsa -C "你的GitHub注册邮箱"
```

找到生成的.ssh的文件夹中的id_rsa.pub密钥，将内容全部复制,打开自己github的设置，新建new ssh key,名称可以随便写，再key的一栏输入刚才复制的内容保存即可。

### 安装deployer插件

和此时需要再安装一个插件来deploy我们的网页到github,安装软件

```bash
npm install hexo-deployer-git --save
```

安装成功之后，更改blog文件夹里面的_config.yml,里面是我们的配置信息，里面搜索关键字deploy,修改为如下所示

```bash
deploy:
  type: git
  repo: git@github.com:<your name>/<your name>.github.io.git
  branch: master

```

这一步非常重要，格式不正确就会出错，比如type是git,不是github,冒号后面还有一个空格等。此时我们就可以将我们的网页发布到github了。输入

```bash
hexo clean #清除生成的网页文件
hexo g #生成静态网页
hexo d #发布到github
```

此时打开对应的网页：https://<your name>.github.io 就可以看到已经部署成功了。当然，此时网站还只是默认设置，怎么发布新文章，怎么修改主题，变成我们需要的风格呢？接下来介绍一些花里胡哨的功能的实现~

## Next主题的配置

Hexo主题很多，网页上选择非常多，https://hexo.io/themes/ 查阅了很多的文章，大家比较推崇的主题是Next，主要是功能齐全，对于不会太多网页编程知识的人来说，最好了。

### Next主题的安装

找一个文件夹下载主题

```bash
git clone https://github.com/theme-next/hexo-theme-next.git
```

删除掉里面.github的文件之后，复制到我们博客文件的themes文件夹内，里面已经有了一个默认的主题文件landscape.为了使用next主题，我们到站点目录的配置文件_config.yml里面，知道theme那一行，改为

```bash
theme: next
```

此时，再输入命令

```bash
hexo g 
hexo s
```

就可一查看我们的新的主题文件了。

### 配置个人信息

为了让博客具有我们的个人风格，我们需要将一些地方改成自己的信息，首先修改站点目录的配置文件

```bash
# Site
title: Knifelees3's blog #博客名字
subtitle: #副标题
description: #类似于个性签名？
keywords: #关键词
author: Zhao Hua #作者名字
language: zh-CN #语言
timezone: #时间轴
```

然后修改/theme/next/_config.yml文件，里面的内容就更加丰富了，不过都有注释，会点英语的应该都可以看得懂。这篇文章
https://zhuanlan.zhihu.com/p/30836436 也有非常详细的介绍，我就不再赘述。在这里我需要强调的是关于怎么更换头像的问题，貌似新版的语法不一样了，以前的写法

```bash
avatar: /images/avatar.gif
```

但是next 7.0版本却是

```bash
avatar:
	url: /images/avatar.gif
```

在这里浪费了好久的时间....

### 添加评论系统

评论系统本来貌似蛮多的，不过后来都相继的死掉了，我用的是Valine,在这之前需要注册Leancould,验证邮箱和绑定手机号，然后点击创建应用>开发版，建好之后点击进入到应用中，依次点击设置>应用Key得到AppID和AppKey，这是安全域名，设置自己的网页地址即可。由于next最新版本的主题已经自己集成了Valine，只需要在主题配置文件找到Valine字段，改成下面的形式即可(输入刚才的Leancould的appid,appkey)：

```bash
# Valine
# You can get your appid and appkey from https://leancloud.cn
# More info available at https://valine.js.org
valine:
  enable: true # When enable is set to be true, leancloud_visitors is recommended to be closed for the re-initialization problem within different leancloud adk version.
  appid:  # your leancloud application appid
  appkey:   # your leancloud application appkey
  notify: false # mail notifier, See: https://github.com/xCss/Valine/wiki
  verify: false # Verification code
  placeholder: Just go go # comment box placeholder
  avatar: mm # gravatar style
  guest_info: nick,mail,link # custom comment header
  pageSize: 10 # pagination size
  visitor: true # leancloud-counter-security is not supported for now. When visitor is set to be true, appid and appkey are recommended to be the same as leancloud_visitors' for counter compatibility. Article reading statistic https://valine.js.org/visitor.html
  comment_count: true # i
```

### 添加阅读统计

还是使用前面注册的leancloud,插件新的应用，在应用里面新建Class，命名为"Counter"（必须命名为Counter,Next主题才可以识别）,然后和前面的一样，在配置文件搜索Leancloud,加入appid,appkey,如下
```bash
leancloud_visitors:
  enable: true
  app_id: your appid
  app_key: your appkey
  # Dependencies: https://github.com/theme-next/hexo-leancloud-counter-security
  # If you don't care about security in leancloud counter and just want to use it directly
  # (without hexo-leancloud-counter-security plugin), set `security` to `false`.
  security: true
  betterPerformance: false
```

至此我们的网页就设置好了，一些其他的设置都可以参考这篇博文
https://zhuanlan.zhihu.com/p/30836436 

## 插入图片

Markdown插入图片，可以通过将图片一起上传到github，这样图片多了，每次发布都会比较慢，所以插入在线的图片最好，图床很多人推荐七牛云，我没有选择这种方式，而是创建了一个新的Repositories,专门用来存放图片，图片的图床地址可以通过在github下载图片得到。需要注意的是，自己的非常注意图片的命名分类，不然以后多了就会难以找到自己想要的图片了。

以后有新的问题和心得也会在这篇文章里面持续更新。