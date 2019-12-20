---
title: Linux服务器常见命令
date: 2019-12-16 19:55:30
tags:
- Linux
categories: 
- 技术
mathjax: true
---
[TOC]





## 服务器重要命令

###  1. 远程重启或者关机

立即远程重启

```bash
sudo shutdown -r now
```

立即远程关机

```bash
sudo shutdown -h now
```



### 2. 添加或者删除用户

添加用户

```bash
sudo adduser <username>
```

然后按照提示输入密码等信息即可。此种方法创建用户之后，可以在home目录生成一个和用户名同名字的文件夹。

删除用户

```bash
sudo userdel -r <username>
```

此种方法删除用户之后，home目录和用户名同名字的文件夹也会删。



### 3. 查看服务器的硬盘大小

查看运行内存大小, 以Gb为单位

```bash
free -g 
```

或者是`free -m`（以m为单位），`cat /proc/meminfo`（详细信息）

查看磁盘占用情况

```bash
df -hl 
```

查看当前文件夹的大小

```bash
du --max-depth=1 -h
```

查看单个文件夹或目录大小

```bash
du -sh <folername>
```

以下是一些运行结果

```bash

root@hwsrv-645334:~# free -g
              total        used        free      shared  buff/cache   available
Mem:              0           0           0           0           0           0
Swap:             0           0           0
root@hwsrv-645334:~# free -m
              total        used        free      shared  buff/cache   available
Mem:            992          46         178          10         767         733
Swap:             0           0           0
root@hwsrv-645334:~# cat /proc/meminfo
MemTotal:        1016012 kB
MemFree:          182528 kB
MemAvailable:     750804 kB
Buffers:          145532 kB
Cached:           471356 kB
SwapCached:            0 kB
Active:           427940 kB
Inactive:         217128 kB
Active(anon):      31112 kB
Inactive(anon):    10340 kB
Active(file):     396828 kB
Inactive(file):   206788 kB
Unevictable:        3660 kB
Mlocked:            3660 kB
SwapTotal:             0 kB
SwapFree:              0 kB
Dirty:                16 kB
Writeback:             0 kB
AnonPages:         31876 kB
Mapped:            22608 kB
Shmem:             10848 kB
Slab:             169512 kB
SReclaimable:     148692 kB
SUnreclaim:        20820 kB
KernelStack:        1920 kB
PageTables:         2444 kB
NFS_Unstable:          0 kB
Bounce:                0 kB
WritebackTmp:          0 kB
CommitLimit:      508004 kB
Committed_AS:     259952 kB
VmallocTotal:   34359738367 kB
VmallocUsed:           0 kB
VmallocChunk:          0 kB
HardwareCorrupted:     0 kB
AnonHugePages:      4096 kB
CmaTotal:              0 kB
CmaFree:               0 kB
HugePages_Total:       0
HugePages_Free:        0
HugePages_Rsvd:        0
HugePages_Surp:        0
Hugepagesize:       2048 kB
DirectMap4k:       46960 kB
DirectMap2M:     1001472 kB
DirectMap1G:           0 kB
root@hwsrv-645334:~# df -hl
Filesystem      Size  Used Avail Use% Mounted on
udev            487M     0  487M   0% /dev
tmpfs           100M   11M   89M  11% /run
/dev/sda1        30G  2.1G   27G   7% /
tmpfs           497M     0  497M   0% /dev/shm
tmpfs           5.0M     0  5.0M   0% /run/lock
tmpfs           497M     0  497M   0% /sys/fs/cgroup
tmpfs           100M     0  100M   0% /run/user/0
```

### 4. 查看服务器的核心数等

查看CPU个数

```bash
cat /proc/cpuinfo |grep "physical id"|sort|uniq|wc -l
```

查看每个物理CPU含有的核心个数

```bash
cat /proc/cpuinfo |grep "cpu cores"|uniq|wc -l
```

查看每个CPU核心含有的线程数

```bash
cat /proc/cpuinfo |grep "processor"|wc -l
```

那么cpu支持的线程数为 cpu数目 * 每个cpu含有的核心数目* 每个核心含有的线程数



### 5. 重启服务器网络

可以输入

```bash
/etc/init.d/network restart
```

或者

```bash
/etc/init.d/network restart
```



### 6. 给某一用户管理员权限

只需要修改`/etc/sudousers`文件即可，该文件默认是不可编辑的，首先得更改其权限为可写

```bash
sudo chmod +w /etc/sudoers
```

读、写、执行权限可以通过$\pm$`rwx`来控制，其文件内容大致如下

```bash
#
Defaults        env_reset
Defaults        mail_badpass
Defaults        secure_path="/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin:/snap/bin"

# Host alias specification

# User alias specification

# Cmnd alias specification

# User privilege specification

root    ALL=(ALL:ALL) ALL

# Members of the admin group may gain root privileges

%admin ALL=(ALL) ALL

# Allow members of group sudo to execute any command

%sudo   ALL=(ALL:ALL) ALL

# See sudoers(5) for more information on "#include" directives:

#includedir /etc/sudoers.d
```

只需要在 `root    ALL=(ALL:ALL) ALL`一行下按照同样的方式输入对应的用户名即可

```bash
<username> ALL=(ALL:ALL) ALL 
```

保存退出以后，将文件更改问只读

```bash
sudo chmod -w /etc/sudoers
```

### 7. 添加到环境变量的方法

为了可以在命令行使用，还需要将安装的软件执行文件添加到环境变量。给某个用户和给所有用户添加环境变量是不一样的。

#### A.用于当前用户：

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

#### B.用于所有用户：

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

### 8. 安装多个版本软件

 有时候我们可能需要安装COMSOL或者MATLAB的多个版本，多个版本软件的安装目录默认是不冲突的，如MATLAB在“/usr/local/MATLAB”下会有“R2018a”或者“R2018b”来区分，COMSOL在“/usr/local/”下有“comsol51”和“comsol54”加以区分。当我们将安装路径加入环境变量之后，由于启动的文件名相同，比如都是“comsol”，为了区别出到底是想启动COMSOL的哪个版本。我们可以将文件名做更改，比如将comsol5.4版本的bin目录下的comsol文件改名为comsol54:

```bash
sudo mv /usr/local/comsol54/multiphysics/bin/comsol /usr/local/comsol54/multiphysics/bin/comsol54
```

这样我们在命令行输入“comsol54”就可以指定启动COMSOL5.4版本了。其他软件的做法也类似。

