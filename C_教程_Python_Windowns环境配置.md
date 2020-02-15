#   Windows python 环境配置





## 说明



python在ubuntu的安装比较简单，我装的是Anaconda3, 然后设置环境变量就可以。在办公室的Windows电脑也设置好了，可以直接运行程序。但是在自己新买的HP-Eilte Book 735 G5  AMD 版本里面，总是会出现问题：  

1.第一个问题是在cmd命令里面没办法运行python,只能在Anaconda自带的命令窗口prompt里面用，发现可以通过将python加入环境变量解决。



2.第二个问题是即使我加入了环境变量，在命令行使用的时候，还是没办法插入插件包，比如numpy,晚上搜索了许多，发现可能是因为版本问题？反正我重新安装了一边numpy就好了。但是那么多插件全部都得自己重新安装，岂不费事？这样Anaconda的优势就体现不出来了。（也和python环境有关，我自己是搞不定）



3.第三个问题是conda更新出现HTTP ERROR,貌似可以通过更改镜像源来解决。以前linux死活不行是因为我设置了代理翻墙。



## 直接安装python3,然后pip一个个安装

由于上面的第二个问题没办法解决，干脆不装anaconda，直接轻量级安装python3，官网下载。安装之后手动将python3以及/python3/scripts都添加到环境变量即可，然后就可以使用了。安装方式为



```bash

pip install <package name>

```







### 安装缓慢解决方式

更换清华大学的源

临时使用

```

pip install -i https://pypi.tuna.tsinghua.edu.cn/simple some-package

```

注意，simple 不能少, 是 https 而不是 http,要设为默认，只需要将pip更新到最新然后输入

```

pip install pip -U

pip config set global.index-url https://pypi.tuna.tsinghua.edu.cn/simple

```



有时候在线安装会有问题，可以尝试去网站下载whl文件安装



https://www.lfd.uci.edu/~gohlke/pythonlibs/







更新 20190803



目前清华中科大的anaconda的镜像源不能用了，只能用官网的。回复anaconda镜像源为官网的方式为：删除掉对应的.condarc文件，windows中一半在用户目录下。
