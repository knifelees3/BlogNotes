---
title: Linux设置远程桌面连接
date: 2019-06-26 11:22:10
tags:
- Linux
categories: 
- 技术
mathjax: true
---
本笔记更新地址：
https://knifelees3.github.io/2019/06/26/Linux%E8%BF%9C%E7%A8%8B%E6%A1%8C%E9%9D%A2%E8%BF%9E%E6%8E%A5/

## 介绍

本篇笔记记述了如何在Ubuntu上面配置好xrdp，并且通过windows或者Ubuntu访问。这种方法对于访问linux服务器比Teamviewer要好用，登录后借助于第三方桌面系统，虚拟了一个桌面出来，所以与原来的ubuntu桌面是不一样的，能够满足我们偶尔连接一下，进行少量的图形桌面操作。对于原理讲的比较清楚的是下面这篇博文
https://www.linuxidc.com/Linux/2017-09/147112.htm
我在自己的电脑ubuntu 16.04以及另外一台服务器ubuntu 18.04上面分别试验了一下，方法有所区别。
1. 18.04的配置方法：
https://baijiahao.baidu.com/s?id=1619271691270163095&wfr=spider&for=pc

按照上面这篇博文的方法一步步的做就可以，不做过多说明。
2. 16.04的配置方法
https://www.linuxidc.com/Linux/2017-09/147112.htm
https://www.cnblogs.com/zeze/p/8416448.html
https://www.bnxb.com/linuxserver/27460.html

## 具体配置方法
### Ubuntu16.04与18.04相同的部分
首先是开启远程访问的权限，在Ubuntu打开Desktop sharing(桌面共享)设置如下勾选：
Sharing: 全部勾选
Security: 勾选 Automatically configure......
Show Notification Area Icon: 勾选 Only when someone is......

然后是安装相应的软件，命令都一样，依次输入以下命令安装：
安装tightvncserver，安装xrdp，安装xubuntu-desktop
```
sudo apt-get install tightvncserver
sudo apt-get install xrdp -y 
sudo apt-get install xubuntu-desktop
```

更改配置文件
```
echo unity>~/.xsession 
```

### Ubuntu16.04与18.04不相同的部分
#### 对于16.04 
更改startwm.sh文件
```
sudo subl  /etc/xrdp/startwm.sh
```

在'. /etc/X11/Xsession'前面输入'xfce4-session'，最后文件内容如下
```
#!/bin/sh

if [ -r /etc/default/locale ]; then
  . /etc/default/locale
  export LANG LANGUAGE
fi

xfce4-session #在此处添加
. /etc/X11/Xsession

```
然后重启服务
```
sudo service xrdp restart  
```

#### 对于Ubuntu18.04
更改startwm.sh文件，但是与Ubuntu16.04的文件不太一样，是在‘test -x /etc/X11/Xsession && exec /etc/X11/Xsession’这一句前面添加'xfce4-session'
```
#!/bin/sh
# xrdp X session start script (c) 2015, 2017 mirabilos
# published under The MirOS Licence

if test -r /etc/profile; then
        . /etc/profile
fi

if test -r /etc/default/locale; then
        . /etc/default/locale
        test -z "${LANG+x}" || export LANG
        test -z "${LANGUAGE+x}" || export LANGUAGE
        test -z "${LC_ADDRESS+x}" || export LC_ADDRESS
        test -z "${LC_ALL+x}" || export LC_ALL
        test -z "${LC_COLLATE+x}" || export LC_COLLATE
        test -z "${LC_CTYPE+x}" || export LC_CTYPE
        test -z "${LC_IDENTIFICATION+x}" || export LC_IDENTIFICATION
        test -z "${LC_MEASUREMENT+x}" || export LC_MEASUREMENT
        test -z "${LC_MESSAGES+x}" || export LC_MESSAGES
        test -z "${LC_MONETARY+x}" || export LC_MONETARY
        test -z "${LC_NAME+x}" || export LC_NAME
        test -z "${LC_NUMERIC+x}" || export LC_NUMERIC
        test -z "${LC_PAPER+x}" || export LC_PAPER
        test -z "${LC_TELEPHONE+x}" || export LC_TELEPHONE
        test -z "${LC_TIME+x}" || export LC_TIME
        test -z "${LOCPATH+x}" || export LOCPATH
fi

if test -r /etc/profile; then
        . /etc/profile
fi

xfec4-session #在此处添加
test -x /etc/X11/Xsession && exec /etc/X11/Xsession
exec /bin/sh /etc/X11/Xsession

```

然后重启服务
```
sudo systemctl restart xrdp.service  
```

## 用法
具体使用时，我们可以在windows和linux上面使用远程桌面。方法也有区别
1. Windows上的使用
直接打开windows的远程桌面连接软件，win+r健启动后输入：mstsc命令执行，输入对应的ip地址，进去之后需要再输入用户名和密码，并且连接的方式有区别。16.04的方法是‘sesman-Xvnc’,18.04是‘Xorg’，都使用默认的就好，不用自己改。
2.  Ubuntu上的使用
需要安装一个软件Remmina,一般ubuntu默认就有，没有的话安装一下就好（sudo apt install remmina）。同样的输入ip地址、用户名、密码即可访问。

### 注意
1. 具体使用时，有时候会有bug，比如我连接18.04时没办法调出命令行，这个时候可以点击桌面左上角的application>terminal emulator即可，或者找另外的terminal也行，比如xterm-terminal等，都在application列表里面。
2. 这种连接方式在你退出软件之后，不会断开登录，你打开的桌面还会继续存在下去，如果要退出登录，点击右上角的用户名之后，点'logout'即可。
# 固定ip地址的方法
将申请到的ip信息在自己的系统上更改即可，更改有两种方式，一种是在图形界面更改，点击Ubuntu对应的网络设置，注意*网口的mac地址要与申请的ip所用的mac地址相符合*。另外一种方法就是按照下面的一些教程来改，我没有自己亲自试过。
https://www.jb51.net/article/143115.htm
https://blog.csdn.net/qq_36937342/article/details/80876385
https://blog.csdn.net/qq_43483975/article/details/89597371

## 补充说明
这种借助于windows自带远程桌面软件的方式，也可以用来在一台windows控制另外一台windows,体验可能比teamviewer差一点，延迟、缩放什么的会有小问题，特别是在两个windows屏幕大小不一样的情况下。另外一个缺点就是一些软件比如MATLAB你在远程是没有办法启动的，因为一般MATLAB等软件的破解都是选择的非server版本的licsence。这时候需要用比如teamview来首先启动MATLAB，再用远程桌面连接。

