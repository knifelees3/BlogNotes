# APS用RevTex投稿全记录



本笔记详细技术了如何用latex写一篇论文并投稿。在准备论文的时候，需要用到的软件有



* [Texlive](https://www.tug.org/texlive/) ，用来编译Latex。

* [RevTex](https://journals.aps.org/revtex)，APS官方写作包，对于Texlive，一般都会默认安装有Texlive，只是不是最新版的。

* Latex编辑器，我比较推荐Sublime或者Vs code等。

* 文献管理软件，我比较推荐Endnote以及Mendeley,文献管理软件很多，找一个适合自己的，我自己用的是Endnote。



当然，实际准备论文时候，还需要准备论文绘图，绘制数据图的时候，我使用了MATLAB和python一起来绘制的，二者都不能完全相互替代。绘制示意图时，用到了Corel draw绘制二维矢量图，Blender绘制三维图。



## 准备阶段



在准备阶段，需要安装一系列软件。每个人用的软件可能会有区别，比如写latex我喜欢用sublime来书写，其在插入文献的时候有其他软件无法比拟的功能。我在此以我用的软件为例，写一下准备一篇文章需要经过哪些步骤。



安装texlive2018： 用来编译latex文件



安装sublime并且配置好相关的插件： 用来书写文章，安装插件后，有很多补全功能。



安装Endnote： 用来管理文献、插入文献











## 用Endenote建立自己的文献库



我们需要用Endnote来将自己阅读的文献进行整理、分类、命名，这样自己平时阅读的时候 比较方便，需要用到的时候，也可以快速的提取到。具体Endnote使用，可以参见我的另外一个博客：



最终确定要插入哪些文献以后，需要将要插入的文献，导出为bibtex格式，具体做法为，选择“output style”为"export bibtex",然后带格式的复制对应的参考文献，新建一个名为“reference.bib”的文件，粘贴复制的内容到该文件即可，其文件的内容一般如下：



```latex

@article{RN24,

   author = {Bradford, Matthew and Shen, Jung-Tsung},

# e = {Single-photon frequency conversion by exploiting quantum interference},

   title = {Single-photon frequency conversion by exploiting quantum interference},

   journal = {Physical Review A},

   volume = {85},

   number = {4},

   ISSN = {1050-2947

1094-1622},

   DOI = {10.1103/PhysRevA.85.043814},

   year = {2012},

   type = {Journal Article}

}



@article{RN25,

   author = {Bradford, Matthew and Shen, Jung-Tsung},

# e = {Spontaneous emission in cavity QED with a terminated waveguide},

   title = {Spontaneous emission in cavity QED with a terminated waveguide},

   journal = {Physical Review A},

   volume = {87},

   number = {6},

   ISSN = {1050-2947

1094-1622},

   DOI = {10.1103/PhysRevA.87.063830},

   year = {2013},

   type = {Journal Article}

}

```



内容包含了作者、杂志、期刊号等，是一些基本的格式。



## 使用sublime来写手稿



投稿时，需要用到APS的官方revtex的包，我们安装的texlive默认就安装了该包，不用再额外的安装了。我们一般的文章的一个例子如下：



```latex

%\documentclass[aps,prl,reprint,superscriptaddress,showpacs]{revtex4-1}

\documentclass[%

reprint, %preprint, twocolumn% 其中reprint提供双栏最接近出版论文的格式，preprint显示的字体和行距则相对大一些，是方便审稿人将论文打印出来仔细阅读的，twocolumn选项与此类似。

superscriptaddress, %groupedaddress,% 现在通用是前一种作者名录格式，这样在显示多个作者或者一个作者从属于多个机构时比较紧凑方便。

showpacs,% 显示PACS代码

amsmath, amssymb, %都是用于显示数学公式环境

aps, %这个是指APS风格，另一个可选项应该是AIP

prl,%pra, prb, rmp, % 这里是对不同期刊的选择

]{revtex4-1}% 这个格式就是APS对应的latex文档格式

\usepackage{graphicx}% Include figure files

\usepackage{dcolumn}% Align table columns on decimal point

\usepackage{bm}% bold math

\usepackage{natbib}%to cite

\usepackage{hyperref}% add hypertext capabilities

\usepackage{float}

%\usepackage{stix}

\usepackage{mathrsfs}%花体的插入方法

\hypersetup{colorlinks=true, citecolor=blue, urlcolor=blue, linkcolor=blue}

\bibliographystyle{apsrev4-1.bst}% 注意这个.bst风格文件是需要从官网单独下载的，可以控制文章末尾参考文献的现实风格。下载之后放到工作目录下即可(即.tex文档所在的目录)

\begin{document}

# Quantum Photonic Node for On-Chip State Transfer}% Force line breaks with \\

\title{Quantum Photonic Node for On-Chip State Transfer}% Force line breaks with \\

# s{A footnote to the article title}%

%\thanks{A footnote to the article title}%

\author{Youself}% You, the writer of this paper. 第一作者

%\noaltaffiliation

%\altaffiliation{School of Physics, Huazhong University of Science and Technology, Luoyu Road 1037, Wuhan, 430074, People’s Republic of China}



\author{Xiao Ming}% Boss with communication email 通讯作者，注意这里的Email一定要放在通讯作者后的第一个位置，这样邮箱地址的链接才会正确显示。

\email{12345678@gmail.com}

%\affiliation{School of Physics, Huazhong University of Science and Technology, Luoyu Road 1037, Wuhan, 430074, People’s Republic of China}

\author{Leehoom Wang} % Boss with communication email 通讯作者，注意这里的Email一定要放在通讯作者后的第一个位置，这样邮箱地址的链接才会正确显示。

\email{Leehoom_wang@gmail.com}	

%\homepage{http://www.Second.institution.edu/~Charlie.Author}

\affiliation{School of Physics, Huazhong University of Science and Technology, Luoyu Road 1037, Wuhan, 430074, People’s Republic of China}%



\date{\today}%This date can be changed.

\begin{abstract}% 摘要

This is abstract This is abstract This is abstract This is abstract This is abstractThis is abstract This is abstract  

\end{abstract}

\pacs{42.50.Ct, 42.50.Ex, 42.50.Pq, 42.79.Gn}% PACS, the Physics and Astronomy

%\keywords{Suggested keywords}% Not always required.

# tle

\maketitle





\begin{acknowledgments}

This is acknowledgments This is acknowledgments This is acknowledgments This is acknowledgments This is acknowledgments This is acknowledgments This is acknowledgments 

\end{acknowledgments}



\bibliographystyle{apsrev4-1}

\bibliography{reference.bib} % The reference file name

\end{document}

```



## 如何插入文献



写文章非常重要的一个部分就是插入文献。在word中插入文献，只需要安装好endnote之后，即可一
