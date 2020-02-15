# Linux设置定时运行脚本以及软件开机自动启动

# 有关ubuntu平台上定时运行某一软件，以及开机启动软件的方法



*Zhaohua Tian*

*2018 05 31*



## 开机启动的设置方法



在windows开机启动设置比较简单，只需要在任务管理器设置就可以，在ubuntu里面也可以实现类似的功能，只需要安装一个软件：Tweak Tool.不过此方法可以设置的软件有限，只能是系统的一些特殊软件，我们要实现的是开机启动一部分脚本命令。

我此次主要目的是为了开机启动Lumerical的Licence Manager,因为只有这个开启之后才能打开FDTD软件。手动开启的代码为：



```bash

sudo /etc/init.d/lumlmadmin start

```



通过网上查找相关资料，得知开机启动的设置一共有两种方法：



### 修改/etc/rc.local文件



该文件中只需要手动加入你需要开机运行的代码就可以了，该文件的格式如下：



```bash

#!/bin/sh -e

#

# rc.local

#

# This script is executed at the end of each multiuser runlevel.

# Make sure that the script will "exit 0" on success or any other

# value on error.

#

# In order to enable or disable this script just change the execution

# bits.

#

# By default this script does nothing.

nohup echo password | sudo -S /home/tzh/software/Su_for_Linux_V1.31/rjsupplicant.sh -u 校园网账户 -p 密码 -d 1 &

exit 0

```



上面是我设置的开机运行校园网的代码，由于需要用Root来运行，所以必须输入密码，为了设置开机启动，就运用了命令：



```bash

echo  passwd | sudo -S command

```



这种方法可以实现自动输入密码，方法的坏处是自己的密码以明文保存在文件里，不是很安全。



### 创建自己的启动服务项



在/etc/init.d 文件夹里面都是一些需要用到的服务，为了让自己的代码也可以像该文件夹下面的文件一样自动启动，可以在该文件夹下面创建自己的执行脚本文件



```bash

vi /etc/init.d/my_service.sh

```



我以我用到的代码为例，



```bash

#! /bin/sh

### BEGIN INIT INFO

# Provides:          my_service.sh

# Required-start:    $local_fs $remote_fs $network $syslog

# Required-Stop:     $local_fs $remote_fs $network $syslog

# Default-Start:     2 3 4 5

# Default-Stop:      0 1 6

# Short-Description: starts the my_service.sh daemon

# Description:       starts my_service.sh using start-stop-daemon

### END INIT INFO

sudo /etc/init.d/lumlmadmin start

exit 0

```



代码的前面必须要加那么一段，不然不会成功，然后再加入自己要运行的代码即可。然后需要将我们自己加入的服务添加进list,



```bash

sudo update-rc.d -f myservice.sh defaults 90

```



数字90代表的是次序，貌似应该弄大一点才可以成功，具体的细节我也不是很清楚。



## 定时运行脚本的方法



crontab单词的意思是：定时任务。



crontab命令常见于Unix和类Unix的操作系统之中，用于设置周期性被执行的指令。该命令从标准输入设备读取指令，并将其存放于“crontab”文件中，以供之后读取和执行。该词来源于希腊语 chronos(χρόνος)，原意是时间。





通常，crontab储存的指令被守护进程激活， crond常常在后台运行，每一分钟检查是否有预定的作业需要执行。这类作业一般称为cron jobs。



有了上面的概念，再来看crontab的使用就会清晰些。



既然是系统每分钟都要检查一下，那么必然要有一个检查的依据，如配置文件或者什么的。

还是来看看百科：



crontab文件包含送交cron守护进程的一系列作业和指令。每个用户可以拥有自己的crontab文件；同时，操作系统保存一个针对整个系统的crontab文件，该文件通常存放于/etc或者/etc之下的子目录中，而这个文件只能由系统管理员来修改。

　　crontab文件的每一行均遵守特定的格式，由空格或tab分隔为数个领域，每个领域可以放置单一或多个数值。

好了，开始使用了。估计有些人从定义就知道他要怎么用了。不过我还是想记录下。



使用步骤：

1、终端运行crontab -e [解释：编辑配置文件]

2、选择你要用的编辑器，一般人会选择vi。

3、此时配置文件已打开，只需要按照他的格式写配置即可。



好吧，简单到我都觉得。。



举个例子：



在我的home目录下有一个python脚本，helloworld.py



```bash

   #coding:utf-8

  print 'hello world by crontab!'

```



我想要这个脚本在每天的早上7点30执行。

因此这个 任务的crontab配置文件就是：



```bash

   # m h  dom mon dow   command

   30 7 * * * python /home/the5fire/testcrontab.py /home/the5fire/testcrontab.log 2&1

```



简单解释下，这个配置的意思就是在每天的7：30用python运行我的家目录下的testcrontab.py文件，并将输出内容输出到testcrontab.log中，后面那个2&1的意思是把错误的输出也输出到标准输出（2表示错误，2表示错误输出，&表示等同于，1表示正确），因此如果运行出错也会把错误输出到之前定义的log中。



另外关于合适执行命令还有些要说。



上面只是定时几点执行，那么我怎么设置它按照某一频率执行。比如每分钟执行依次。

对应的配置就是



```bash

  # m h  dom mon dow   command

 */1 * * * * python /home/the5fire/testcrontab.py /home/the5fire/testcrontab.log 2&1

```



再来一个场景，我想在每天的早上六点到八点之间，每隔3分钟执行一次的配置怎么写：



```bash

  # m h  dom mon dow   command

 */3 6-8 * * * python /home/the5fire/testcrontab.py /home/the5fire/testcrontab.log 2&1

```



到此应该都会使用了吧，五个星号表示不同的执行单位(分、时、日、月、年)，而那个反斜线表示频率。





上面是我参考的文章https://blog.csdn.net/babydavic/article/details/8446886



我设置的锐捷网络客户端每隔一段时间运行的代码如下



```bash

# Edit this file to introduce tasks to be run by cron.

#

# Each task to run has to be defined through a single line

# indicating with different fields when the task will be run

# and what command to run for the task

#

# To define the time you can provide concrete values for

# minute (m), hour (h), day of month (dom), month (mon),

# and day of week (dow) or use '*' in these fields (for 'any').#

# Notice that tasks will be started based on the cron's system

# daemon's notion of time and timezones.

#

# Output of the crontab jobs (including errors) is sent through

# email to the user the crontab file belongs to (unless redirected).

#

# For example, you can run a backup of all your user accounts

# at 5 a.m every week with:

# 0 5 * * 1 tar -zcf /var/backups/home.tgz /home/

#

# For more information see the manual pages of crontab(5) and cron(8)

#

# m h  dom mon dow   command

* */5 * * * /home/xwc/software/rj >>/home/tzh/cronlog/the_cron.log 2>&1

```



需要注意的是，不同用户的定时运行软件是不一样的，这里我用的是root用户编辑的，因为锐捷网络客户端只能root才能执行。
