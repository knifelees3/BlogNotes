---
title:  MATLAB 常见命令
categories:
- 技术
tags:
- MATLAB
- 科学绘图
---
<script type="text/javascript" src="http://cdn.mathjax.org/mathjax/latest/MathJax.js?config=TeX-AMS-MML_HTMLorMML"></script>
[TOC]

## 导出导入数据篇

1. 导入csv文件

```matlab
mat=csvread('file name',起始行,起始列)
```

1. 导出csv文件

```matlab
csvwrite('filename',matname)
```

1. 高精度的导出数据

```matlab
dlmwrite('filename',matname,'delimiter','\t','precision',9)
```

## 保存图片

```matlab
filename2png=['Beta1_radius',num2str(radius),'_width_',num2str(width),'_RR_1E6.png'];
print(num2str(filename2png), '-dpng', '-r600')
```

## 绘图

1. 设置坐标范围

```matlab
xlim([0,1]);
ylim([0,1]);
```

1. 设置坐标标签

```matlab
xlabel('');
ylabel('');
```

1. 设置字体

```matlab
'Fontname','Times new roman'
```

1. 线型粗细

```matlab
'Linewidth',15''
```

1. 设置坐标的范围

```matlab
xticks([-5 -2.5 -1 0 1 2.5 5])
```

1. 绘制多个图保存之后关闭

```matlab
figure(1)
close(figure(1))
```

1. 颜色图相关

```matlab
[x y]=meshgrid(X,Y);
pcolor(x,y,mat);
shading interp
colormap('jet');
colorbar
caxi([])
```



## 数据运算

一般应该将循环化为矩阵预算，对于二维嵌套循环，这里给一个例子

### 初始代码

```matlab
num1=1000;
num2=1000;
mat=zeros(num1,num2)
for l=1:num1
	for m=1:num2
		mat(l,m)=l*m
	end
end
```

### 转化矩阵

将其改为

```matlab
num1=1000;
num2=1000;
mlist=linspace(1,num1,num1);
llist=linspace(1,num2,num2)
mat=zeros(num1,num2);
mmat=zeros(num1,num2);
lmat=zeros(num1,num2);
mmat(:,:)=mlsit(1,:);
lmat(:,:)=llsit(1,:)';
mat=mmat*lmat;
```


## 常见的有用的例子
### 从文件导入数据并且绘图


## 学校服务器启动matlab live link

```bash
#！ /bin/bash/
comsol mphserver </dev/null> /dev/null &
/opt/matlab/bin/matlab -nodesktop -nosplash -r matlab_exe
```

## Using_Matlab_In_Batch_Mode

*2018 05 03*

###  输入命令

进入m文件所在目录后，运行

```bash
$ matlab -nojvm -nodesktop -nosplash -r matlabfile
```

只用文件名matlabfile，不能添加.m,也不用添加引号

### 修改.bashrc文件

```bash
vim ~/.bashrc
```

添加如下：

```bash
Add an "mrun" alias for running matlab in the terminal.
alias mrun="matlab -nodesktop -nosplash -logfile `date +%Y_%m_%d-%H_%M_%S`.log -r"
```
保存后，进入.m文件所在目录，运行

```bash
mrun matlabfile
```