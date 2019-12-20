---
title: Ubuntu常见有用命令
date: 2019-03-03 01:35:01
tags:
- Linux
categories:
- 技术
---

# Some Useful Code In Linux

## 安装、卸载软件

```bash
sudo dpkg -i
sudo apt-get purge
```

## 挂载、卸载磁盘文件

```bash
mount -o loop /filename.iso /mnt/tmp
umount /mnt/tmp
```

## 文件可执行

```bash
chmod +x filename.sh
```

## 解压文件

```bash
tar -xvcf ./filename.tar
```


## 重启网络

```bash
sudo /etc/init.d/networking restart
```

## on-my-zsh下的模糊匹配

在 oh-my-zsh 下, 如果我们按照上述文件进行复制, 我们会得到这样的错误提示. zsh: no matches found:
我们只需要将 

```bash
remote_username@ip:path/*.csv local_dirname
```

这一字符串用引号包含起来进行

```bash
scp “remote_username@ip:path/*.csv” local_dirname
```

## PDF 插入图片

```
http://pages.uoregon.edu/noeckel/PDFmovie.html
```

## 在服务器运行脚本文件，不受连接与否的影响

```bash
nohup <command> &
```

这样就可以在即使关闭ssh连接之后，服务器依然计算了。特别的，当我们用的是MATLAB且不用图形界面时，需要输入

```bash
nohup matlab -nosplash -nodesktop -r <filename> &
```

即可。

## 查看文件大小以及磁盘容量

```bash
du -h #得到每个文件的大小
df -h #磁盘的大小容量等
```

## 显示文件以及文件夹，按照时间顺序倒序、显示文件大小以及权限

```ls -lrth```

## 更改系统环境变量

```bash
sudo vi /etc/profile
source /etc/profile
```

环境变量的写法：

```bash
export PATH=<the path>:$PATH
```

## 更改用户环境变量

```bash
vi ~/.bashrc
source ~/.bashrc
```

## Git 使用

git add .        （注：别忘记后面的.，此操作是把Test文件夹下面的文件都添加进来）**

**git commit  -m  "提交信息"  （注：“提交信息”里面换成你需要，如“first commit”）**

**git push -u origin master   （注：此操作目的是把本地仓库push到github上面，此步骤需要你输入帐号和密码）**

