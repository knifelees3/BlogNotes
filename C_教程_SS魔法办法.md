# 用shadowsocks搭建自己的代理服务教程



## 服务器的购买



关于购买何种服务器，有比较多的人讨论，因为最近很多服务器涨价，以及很多服务器的ip被封，曾经大家非常推崇的搬瓦工目前已经不太能用了，我是在看了[该介绍](https://zhuanlan.zhihu.com/p/70025050)之后，按照[该方法](https://www.vps234.com/hostwinds-purchase-tutorial/)购买了[hostwinds](https://www.hostwinds.com/)一个服务器，选择的是最便宜的版本，安装了ubuntu 16.04. 选择hostwind而不是搬瓦工等其他的，是基于



(1) 并且hostwind有24小时在线的客服，有啥问题可以直接问



(2) hostwind有针对ip被封的解决办法，我最开始填的地址在美国，导致分配的ip地址中国ping不了，在和客服说了以后更改了位置并且重启网络部署之后，ip就可以访问了。



# shadowsocks的安装



有了一台国外的远程服务器，接下来就可以用其作为代理了。需要下载并且安装shadowsocks，我是根据[该教程](https://www.2cto.com/kf/201808/774027.html)，下载并且安装部署好了shadowsocks，一切都比较顺利~



# 本地登录



本地登录需要首先有一个shadowsocks客户端，自己去github搜索下载即可，虽然原本的[shadowsocks](https://github.com/shadowsocks/shadowsocks)已经被删除了，但其实还有很多的备份，比如[这个](https://github.com/ziggear/shadowsocks),下载安装windows版本之后，就可以输入自己部署的ip，密码，端口，然后科学上网了。







## IOS设备使用代理



Windows,安卓平台都有Shadows Socks客户端，而IOS商店中国区是没有该软件的，需要自己租界或者购买一个海外的IOS账户，安装使用即可。
