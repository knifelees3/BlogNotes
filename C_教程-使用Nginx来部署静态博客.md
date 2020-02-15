# 使用Nginx来部署静态博客



# 介绍



以前一直不懂，我想做一个网页的时候，为啥要购买服务器？购买域名？有什么联系？实际上



* 购买服务器是因为服务器稳定，如果你让自己的电脑作为服务器也是可以的。但是得有公网ip,不然别人的内网穿透之后，才能访问你的服务器。

* 要域名是因为域名便于记忆，也可以彰显个性。直接输入ip访问也是可以的。



我想把静态网页部署在课题组的服务器上，局域网访问，网络上搜索一遍之后，采用了nginx,



>Nginx("engine x")是一款是由俄罗斯的程序设计师Igor Sysoev所开发高性能的 Web和 反向代理 服务器，也是一个 IMAP/POP3/SMTP 代理服务器。

>在高连接并发的情况下，Nginx是Apache服务器不错的替代品

nginx的用处很大，但是我只是拿它来部署我自己的静态网页。

# 安装



nginx不仅可以在Linux上使用，也可以在windows上使用，下面分别介绍安装,我们可以在这里下载：[Nginx](http://nginx.org/en/download.html)



## Windows



windows下载下来是一个压缩包，不用安装，你可以将其拷贝到C盘的`program fiels`,但是修改配置文件会不方便，我建议还是放在其他位置，然后可以创建快捷方式到桌面，并且将其添加到环境变量。这样就可以在命令行使用了。直接运行`nginx.exe`文件即可。



## Ubuntu



ubuntu安装可以直接输入命令即可：



```python

sudo apt-get install nginx

```

查看nginx服务是否已经启动



```python

ps -ef | grep nginx

```



查看nginx版本



```python

nginx -v

```



# 配置并使用



无论是ubuntu还是windows，都只需要修改配置文件即可，配置文件也有讲究，你可以另外新建一个配置文件。我要实现的功能很简单，就直接修改`conf/nginx.conf`文件，主要是修改`http`大括号里面的`server`字段,如果没有`server`字段,自己添加也可以



```python

server {

    listen       80;

    server_name  localhost;



    #charset koi8-r;



    #access_log  logs/host.access.log  main;



    location / {

        # root   C:\Users\xiail\OneDrive\Blog\Blog_Sphnix\build\html;

        root C:\Users\xiail\AppData\Local\Programs\Python\Python37\Lib\site-packages\streamlit\static;

        index  index.html;

    }

```

我们需要修改的主要是两个：



* `listen`: 端口号，默认是80，不需要修改

* `server_name`: 默认为`localhost`,你也可以改成你的电脑ip地址，这样至少局域网可以访问

* `root`: 主要是修改`root`后面的文件夹路径，这里就是你要部署的网页文件夹路径



修改好了之后，就可以启动了。下面是一些常见的命令



```bash

nginx -s reload #重新载入文件

nginx -t #检查文件有没有问题

nginx -s stop # 停止服务

```
