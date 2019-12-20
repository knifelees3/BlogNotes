---
title: gnuplot绘制gif动图
date: 2019-03-06 02:16:50
tags:
- gnuplot
- 科学绘图
categories: 
- 技术
---

大家都知道，gnuplot作图功能强大，但是有很多功能都是靠自己去摸索实验的，只有有创意，有想法，才会画出赏心悦目的图像。这个软件非常下，不过你所能想到的图形他都可以画。

首先提供一个有gnuplot教程的网址 http://www.gnuplotting.org/tag/animation/ ​

我是看了这些例子后自己摸索的。

画动图我分为两种，一种是直接输出很多张图片，然后用某些flash软件合成，我用的是Ulead gif animator。另外一种是直接用gif输出gif图片，这是本次教程的重点。

## 画很多图片，然后用软件合成

我直接给链接 http://www.gnuplotting.org/animation-iv-trajectory/
这个网站里面很多有意思的图片，还有源代码供下载。

## 直接输出动图

### 有公式的绘图

直接输出动图，需要在gnuplot里面用到循环。当我们直接画可以用公式表达的图像时，比如正弦图像等，下面是我的一个具体的例子,首先时创建一个plot的文件：‘plotfunction.plt’,内容如下

```matlab
set term gif animate delay 10 size 600,400 #设置图片大小以及间隔时间
set title 'the sin(x/3)exp(-4x) picture' font 'Times,25' #标题
set output "sinx_exps.gif" #文件名
set xlabel 'x' font 'Times,25' #横坐标
set ylabel 'y' font 'Times,25' #纵坐标
set size 1,1 #缩放比例
set xrange[0:8*pi] #x范围
set yrange[-1:1] #y范围
unset key #没有图例
i=1
load 'loop_sinx.plt' #循环画图的文件
set output #导出
```

上面调用了一个“loop_sinx.plt”的文件，文件内容为：

```matlab
plot sin(x/3+i*pi/5)*exp(-x/4) with lines lw 3 #画图
i=i+1 #变量加一
if(i<40) reread #若不满足则接着画，直到满足条件，不再读取文件为止
```

直接在gnuplot控制台输入：

```matlab
load 'plotfunction.plt'
```

就可以在对应文件夹得到我们需要的动图了：
![sin3x*exp(-x/4)](https://raw.githubusercontent.com/knifelees3/my_pictures/master/20190306_Gnuplot/20190306_gnuplot_1.gif)

### 没有公式的绘图

上面的plot命令时绘制的函数图像，我们还可以从数据点绘制，并且只要好好的安排数据点的排序，以及用好‘every’等命令，就可以画出很多有意思的图像，下面给出例子。

#### 例子一

```matlab
set term gif animate delay 20 size 960,960
set title 'the sin and cos'
set output "animate3.gif"
set xlabel 'x'
set ylabel 'y'
set zlabel 'z'
set xrange [-1:1]
set yrange [0:20]
set zrange [-1:1]
unset key
i=1
load 'looper1.plt'
set output
```

其中文件'looper1.plt'的内容为

```matlab
splot      'spiral.txt' every ::i::i with points pointsize  6 pointtype 7
#这里every的i::i画出来是一个点，如果要画点加线用到every 1::0::i
i=i+1
if(i<100) reread
```

画出来的动图如下：
![Particle Rotate](https://raw.githubusercontent.com/knifelees3/my_pictures/master/20190306_Gnuplot/20190306_Particle_sin.gif)
#### 例子二

```matlab
set term gif animate delay 20 size 500,700
set title 'the wave guide'
set output "animate4.gif"
set xlabel 'x'
set ylabel 'y'
set zlabel 'z'
#set xrange [40:120]
set yrange [40:120]
set zrange [-160:180]
unset key
i=6420
load 'looper1.plt'
set output
```

其中循环文件'looper1.plt'内容为

```matlab
splot      'wave.txt' every 1::6419::i with linespoints pointsize  1 pointtype 1
set hidden3d
i=i+120
if(i<19200) reread
```

画出来的动图如下：
![Line MAP](https://raw.githubusercontent.com/knifelees3/my_pictures/master/20190306_Gnuplot/20190306_Line_Map.gif)
当然我都没有提供我的原txt文件，这是本科时候弄得，文件弄丢了，本笔记与2016年7月26日首发于http://blog.sina.com.cn/s/blog_e5262fc80102w7z4.html

Gnuplot还是很小巧精美的工具，不过自己最近基本用的MATLAB了，配套的软件画图更方便一些。
