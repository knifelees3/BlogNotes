---
title:   Ubuntu软件安装以及使用注意事项
categories:
- 技术
tags:
- Linux
---

### 语法参考

https://www.jianshu.com/p/b03a8d7b1719


## 常用软件列表

作为光学研究方向的研究生，常用的光学仿真以及数值计算软件有如下：

* COMSOL5.1/5.4
* MATLAB2018a
* Fdtd2016a
* 
接下来将分别介绍对应的安装方法。

## 安装FDTD


### A.转换包rpm包

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

### B. 逐个安装Lumerical的包

逐个安装对应的软件Mode solutions ,Fdtd-solutions等一共四个（顺序无所谓），然后最后安装Lumerical_FlexLM-1.6.700，都只需要：

```bash
sudo dpkg -i *.deb
```

至此软件已经全部安装完毕，接下来要做的就是破解激活。

### C. 确保Lumerical flex license manager工作正常

尝试启动Lumerical flex license manager

```bash
sudo /etc/init.d/lumlmadmin start
```

这时候如果成功，再次尝试关闭：

```bash
sudo /etc/init.d/lumlmadmin stop
```

如果以上两步都出现：*ok* 字样，那就说明该软件已经成功了，剩下的就是激活了。但是我实际操作的时候，遇到了如下问题：
* 启动的时候报错：缺少库文件：libxmlsec1.io.1(还缺少另外一个文件，具体是啥忘记了)，这时候Google之后终于找到答案
https://packages.ubuntu.com/trusty/amd64/libxmlsec1-openssl/filelist
解决办法即直接在网站上面下载对应的包安装。即去网站将所需要的库下载即可。
* 如果上面启动时候不报错，但是关闭还是报错：没有什么pid.log什么的，具体是啥忘记了，总之就是还没有真正启动lumerical flex license manager，这个地方花了我好久的时间，最终也是在Google上面找到的答案：
https://kx.lumerical.com/t/unable-to-start-license-manager-on-debian-ubuntu-linux/2692/8
这里面讲需要安装一个叫lsb的东西，具体原因我也不是很懂，因为我自己的电脑安装完全没有问题，安装好之后就可以启动lumerical flex license manager。

### D. 复制文件覆盖

关闭lumerical flex license manager，然后将安装文件夹里面的破解文件复制到对应的目录覆盖即可。再重启lumerical flex license manager：

```bash
sudo /etc/init.d/lumlmadmin start
```

这时候就可以再安装文件的/opt/lumerical/bin目录里面启动fdtd-solutions了。

### E :开机启动设置

还有一个问题是这个Manager不会自动开机启动，所以需要用的时候需要手动开启，怎么设置开机启动可以看另外一篇笔记：
https://knifelees3.github.io/2019/03/02/Linux%E8%AE%BE%E7%BD%AE%E5%AE%9A%E6%97%B6%E8%BF%90%E8%A1%8C%E8%84%9A%E6%9C%AC/#more


## 安装MATLAB

### sudo 权限开始安装

接下来是安装MATLAB,我是在北邮BT下载的最新版本：MATLAB2018a,这个软件装起来比较简单，
文件夹一共有两个盘：xxxxdvd1.iso,xxxxdvd2.iso,首先挂载iso文件1,可以在根目录下新建一个专门用来挂载的文件夹：

```bash
sudo mkdir /mnt/temp/
```

挂载文件到新建的目录

```bash
sudo mount -o loop ./*dvd1.iso /mnt/temp
```

用sudo权限安装,直接运行里面的安装文件，

```bash
sudo /mnt/temp/install
```

开始安装之后选择我有序列号，将Crack文件里面的standalone下面的序列号粘贴进去，开始安装，安装到一半的时候提示插入第二个iso，这时候再次将dvd2.iso挂载，

```bash
sudo mount -o loop ./*dvd2.iso /mnt/temp
```

然后点击确定就可以继续安装了，安装好之后记得卸载挂载的MATLAB iso文件，命令为

```bash
sudo umount /mnt/temp/
```

### 激活覆盖

安装完成之后打开matlab

```bash
sudo /usr/local/MATLAB/matlab2018a/bin/matlab
```

提示激活，选择本地激活，然后选中Crack文件里面的Standlone.lic文件。
最后将Crack文件里面的文件覆盖到对应的安装文件夹即可.
打开MATLAB可能会报错、闪退等，一般都是缺少一些库或者安装包，或者驱动有问题，不同系统、服务器问题不一样，需要google。
我遇到的问题：打开MATLAB可能会遇到问题，命令行里面一排红字，关于显卡的，具体是啥忘记了，打开COMSOL也会对3D什么的报错，这都是由于我们的新系统显卡驱动没有装好的缘故，解决办法：
打开软件源，选择Additional Drivers,选择里面推荐的Nvidia驱动安装即可。重启生效。有时候会出现重启无法开机的情况，这是由于安装的推荐的显卡驱动不对，这时候需要卸载掉已安装的驱动，重新安装其他版本（我自己的电脑最开始就是这个原因一直死机，换了好几个驱动才找到合适的）。
 
## 安装COMSOL

安装最简单的就是COMSOL了，和前面挂载MATLAB一样，挂载iso文件到temp文件夹，运行里面的setup文件

```bash
sudo mount -o loop ./*.iso /mnt/temp
sudo /mnt/temp/setup
```

安装时候选择破解文件夹里面对应的lic文件，然后安装。
最重要的一步，安装COMSOL livelink with MATLAB,选择MATLAB所在文件夹，

```bash
/usr/local/MATLAB/matlab2018a/
```

测试是否安装成功，只需要在命令行输入：comsol,如果可以打开即安装成功，然后输入：

```bash
comsol mphserver matlab
```

如果可以启动matlab，那么就代表成功了。而且第一次打开需要输入用户名即密码，随便输入即可。

## 做对应的快捷方式

安装好软件之后一般不会自动在桌面形成对应的快捷方式，需要手动的添加快捷方式，添加方式为，在桌面编辑对应的文件（以matlab为例）

``` bash
sudo gedit ./Mtalab.Desktop
```

然后添加下面的命令

``` bash
[Desktop Entry]
Name=Matlab 2018a
Exec=/usr/local/MATLAB/R2018a/bin/matlab -desktop %启动文件所在位置
Icon=/usr/local/MATLAB/R2018a/bin/matlab.png %图标所在位置
Type=Application
Name[zh_CN]=Matlab_2018ab
```

保存之后修改权限：

```bash
sudo chmod +x ./Matlab.Desktop
```

即可点击打开了。

## 添加到环境变量

为了可以在命令行使用，还需要将安装的软件执行文件添加到环境变量。给某个用户和给所有用户添加环境变量是不一样的。

### A.用于当前用户：

在对应用户主目录下有一个 .bashrc 隐藏文件，可以在此文件中加入 PATH 的设置如下：

```bash
vi ~/.bashrc
```

加入：

```bash
export PATH=/usr/local/MATLAB/R2018a/bin/:$PATH
```

如果要加入多个路径，只要：

```bash
export PATH=<你要加入的路径1>:<你要加入的路径2>: ...... :$PATH
```

当中每个路径要以冒号分隔。这样每次登录都会生效，此时还需要注销再登录或者使用

```bash
source ~/.bashrc
```

 使得更改生效


### B.用于所有用户：

如果需要环境变量更改对所有用户有效，那么需要更改“/etc/profile”文件

```bash
sudo vi /etc/profile
```

在其中加入：

```bash
export PATH=<你要加入的路径>:$PATH
```

终端输入：echo $PATH 可以查看环境变量此时还需要注销再登录或者使用

```bash
source /etc/profile
```

使得更改生效。

## 安装多个版本软件

有时候我们可能需要安装COMSOL或者MATLAB的多个版本，多个版本软件的安装目录默认是不冲突的，如MATLAB在“/usr/local/MATLAB”下会有“R2018a”或者“R2018b”来区分，COMSOL在“/usr/local/”下有“comsol51”和“comsol54”加以区分。当我们将安装路径加入环境变量之后，由于启动的文件名相同，比如都是“comsol”，为了区别出到底是想启动COMSOL的哪个版本。我们可以将文件名做更改，比如将comsol5.4版本的bin目录下的comsol文件改名为comsol54:

```bash
sudo mv /usr/local/comsol54/multiphysics/bin/comsol /usr/local/comsol54/multiphysics/bin/comsol54
```

这样我们在命令行输入“comsol54”就可以指定启动COMSOL5.4版本了。其他软件的做法也类似。

