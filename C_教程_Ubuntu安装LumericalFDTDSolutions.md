#   Ubuntu安装Lumerical FDTD Solutions



参看网址：



https://kx.lumerical.com/t/how-to-install-on-ubuntu-systems/2471

https://docs.nomagic.com/display/NMDOC/FlexNet+license+server+installation



## 转换包rpm包为deb格式



Lumerical官网对于linux的包只有rpm文件，即是为redhat等系统准备的，对于Debian/Ubuntu系统，需要将rpm转为deb包，工具为alien，安装方式为



```bash

sudo apt-get update

sudo apt-get install alien

```



转换方式为，cd到对应的rpm包所在目录后输入



```bash

sudo alien ./*/rpm

```



就会生成对应的deb包，这种方法一般不推荐，因为在装换的时候可能会遇到各种各样的小问题（有时候会报错），但是没有其他更好的办法了。



## 逐个安装软件



现安装文件.rpm文件已转换为.deb文件，位于install子文件夹内。利用安装命令逐个安装对应的软件：Device, FDTD-Solutions, INTERCONNECT, MODE_Solutions共四个 (顺序无所谓)，最后安装Lumerical_FlexLM，都只需要进入相应.deb文件所在文件夹内，利用如下命令进行安装



```bash

sudo dpkg -i *.deb

```



如果安装由于依赖问题失败，常见于因某软件包版本过底或未安装，可用如下方法解决。



```bash

sudo apt --fix-broken install

```



有时候该方式仍不起作用，或者由于网络限制原因，可以利用synaptic安装，仍存在问题则可到[该网站](https://packages.ubuntu.com/)下载相应软件包利用dpkg命令进行安装，注意在下载的软件包版本应尽可能匹配Ubuntu版本以及硬件架构，否则可能安装失败。对于有些软件包，如`libpng12-0`，没有Ubuntu 18.10对应的版本，此时可尝试其它Ubuntu版本下的`libpng12-0`包



## 尝试启动lumerical flex license manager,



```bash

sudo /etc/init.d/lumlmadmin start

```



并尝试关闭：



```bash

sudo /etc/init.d/lumlmadmin stop

```



* 如果关闭后出现` Shutting down License Manager Daemon:-e [OK]`, 说明该软件已经成功。

* 若出现 [failed] 字样说明失败，此时做以下尝试

    参见：https://docs.nomagic.com/display/NMDOC/FlexNet+license+server+installation

    安装`libc6-i386`，`lsb-core`，`lsb`三个软件包，可利用之前的方法，也可利用如下方式进行安装

    

```bash

sudo apt-get install libc6-i386

sudo apt-get install lsb-core

sudo apt-get install lsb

```







## 尝试启动fdtd-solutions



方法：进入`/opt/lumerical/fdtd/bin/`文件夹，输入`./fdtd-solutions`



* 若此时报错缺少库文件：`libxmlsec1.io.1`，到[该网站](https://packages.ubuntu.com/)下载软件包`libxmlsec1-openssl`（同理，注意此处下载的deb文件的版本应与所安装Ubuntu的版本一致）

* 若启动时提示需要激活，则说明能成功启动



## 激活软件



关闭lumerical flex license manager，然后将文件夹里面的破解文件复制到对应的目录覆盖即可。即将Crack中的lumerical文件夹复制到/opt/lumerical中，方法为进入Crack中的opt文件夹内，利用如下命令复制



```bash

sudo cp -r ./lumerical  /opt

```



## 启动fdtd-solutions



现在启动lumerical flex license manager，然后再启动fdtd-solutions，应该能成功打开fdtd-solutions界面



## 添加到环境变量

在用户文件夹内的隐藏文件.bashrc的末尾在写入一行



```bash

export PATH=$PATH:/opt/lumerical/fdtd/bin

```



## 开机启动设置



还有一个问题是这个Manager不会自动开机启动，所以需要用的时候需要手动开启，怎么设置开机启动可以看另外一篇 [笔记](https://knifelees3.github.io/2019/03/02/Linux%E8%AE%BE%E7%BD%AE%E5%AE%9A%E6%97%B6%E8%BF%90%E8%A1%8C%E8%84%9A%E6%9C%AC/#more)



## 命令行运行



```bash

mpiexec -n 6 fdtd-engine-mpich2nem -t 4 example.fsp

```



表示FDTD会用6个processor以及4个thread进行计算
