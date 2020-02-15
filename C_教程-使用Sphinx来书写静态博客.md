# 使用Sphinx来书写静态博客



# 初衷



学会了hexo发布静态博客以后，再也没有折腾博客的事情了，最近被疫情困在家里，想尝试下当初没有成功的sphinx。



# 步骤



## 安装包和主题



这种步骤CSDN的教程很多都写的很烂，感觉还是知乎更加靠谱，这是知乎的一个教程：[用sphinx快速编写一份技术手册](https://www.zhihu.com/search?type=content&q=sphinx)。



首先是要安装好对应的软件和包。假设你已经安装好了python 3，pip,那么直接安装即可



```python

pip install sphinx

```

然后需要安装一个主题，sphinx的主题可以从[https://sphinx-themes.org/](https://sphinx-themes.org/)查看，种类很多，但是都很简朴，没有那么花里胡哨。安装也很简单，比如我们要安装主题sphinx_rtd_theme,直接使用



```python

pip install sphinx_rtd_theme

```

该主题很多官方软件都在用，比如开源FDTD软件[MEEP](https://meep.readthedocs.io/en/latest/)的说明文档,就是用这个。



## 创建项目



安装好了之后，就得创建项目了。选择一个文件夹作为你的网页文件夹，在该文件夹打开命令行，然后输入



```python

sphinx-quickstart

```

之后就会有一系列的确认的东西，有的是插件的添加，可以按照默认的选，也可以全选`y`,这样的话配置的会多一些，还有一些网页基本信息的输入，如`project name`等，需要自己填，全部弄好之后，会有如下的文件夹：



* build 目录：运行make命令后，生成的文件都在这个目录里面

* source： 你的文档、图片啥的都在该文件夹下书写

* make.bat： 批处理命令文件，不需要管

* makefile： 也不需要管



项目创建基本完成。在当前文件夹下打开命令行窗口，输入`make html`, 就可以生成html形式的文档。你可以在build文件夹打开`index.html`,就可以看见默认的页面了。



## 个性化配置、修改



### 修改主题

配置文件名为source文件夹下的`conf.py`,将`html_theme='alabaster'`改为`html_theme='sphinx_rtd_theme'`.如果想添加插件，也是需要在该配置文件修改。



### 添加插件



sphinx的很多功能需要插件支持，插件可以分两类插件

* 内置官方插件，使用方法可以从该网页查看[sphinx-extensions](https://www.sphinx-doc.org/en/master/usage/extensions/index.html)，可以直接在配置文件添加。

* 开源非官方插件，可以从该网页下载安装[sphinx-contrib](https://bitbucket.org/birkenfeld/sphinx-contrib)，安装方法可以参见如下支持markdown的例子。



### 添加插件例子：支持markdown



[Markdown support](https://www.sphinx-doc.org/en/1.6/markdown.html)

下面是安装顺序



> **Configuration**

>To configure your Sphinx project for Markdown support, proceed as follows:

>Install recommonmark:

>```python

>pip install recommonmark

>```

>Add the Markdown parser to the source_parsers configuration variable in your Sphinx configuration file:

>```python

>source_parsers = {

>   '.md': 'recommonmark.parser.CommonMarkParser',

>}

>```

>You can replace .md with a filename extension of your choice.

>Add the Markdown filename extension to the source_suffix configuration variable:

>```python

>source_suffix = ['.rst', '.md']

>You can further configure recommonmark to allow custom syntax that standard CommonMark doesn’t >support. Read more in the recommonmark documentation.

>```

>



# 总结



sphinx是一个广泛使用的网页生成软件，其可玩性也高，不仅适合做一些博客，也可作为静态网页存在本地，作为笔记来查阅、使用。
