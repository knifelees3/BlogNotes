# EndNote文献管理总结



# 介绍



​	对于搞科研的人来说，有很大一部分时间都花在读文献上，做不同的课题时，会收集相当数量的文献，如果可以高效的管理文献，将会对科研工作大有裨益。文献管理可以分为两种，一种是通过文件夹来管理，需要自己花额外大的事件来命名文件，比如作者、期刊、年份、卷号，有时候还想加上题目，文献很多时，会非常麻烦。我曾经也是用这种方法来管理文献，现在也没有完全舍弃。第二种方法是采用文献管理软件，用软件对文献进行分类保存。目前市面上的软件也是五花八门，比如大名鼎鼎的“Endnote”,免费的“Mendeley”,"Zotero",“Docear”,"Papers",以及最近比较火的“Citavi”,可以参考该[讨论](https://www.zhihu.com/search?type=content&q=%E6%96%87%E7%8C%AE%E7%AE%A1%E7%90%86)

​	我目前只用过Endnote、Mendeley以及短暂用过一点Citavi,最后选择了Endnote,本来前期很喜欢Mendeley，全平台支持，界面友好。因为课题组的人要统一工具，便于分享，最后用上了Endnote,果然是商业软件，用起来还是非常靠谱的。在自己准备第一篇文章的时候，慢慢的摸索查资料，逐渐知道了怎么用Endnote管理文献并且配合word以及latex工具去写一篇paper。为了防止自己忘记，写一篇note来总结记录下。



# 如何用Endnote建立自己的文献库



Endnote与其他的文献管理软件的不同点在于，它的文献管理操作都是基于Library，每一个library都会链接一个同文件目录下data文件夹，library包含所有文献的关键信息。而data是一些附加的数据，比如pdf文件。



## 创建Library: 



建立自己的文献库第一步就是，建立一个library，命名好library的名字，选择好存放位置。有了这样一个library之后，就可以添加文献进来了。



## 导入文献：



导入文献的方式有两种，一种是直接导入pdf文件，Endnote对大部分期刊的杂志的都能够比较准确高效的提取信息,部分期刊如nature、arxiv则不能，因为其卷号、期刊号不是很容易从pdf读取出来，这时候需要手动补充好一些期刊信息，很容易输入错误。另外一种方法就是直接导入ris文件，一般期刊都会直接提供ris文件引用信息供下载，也可以用google学术下载(google学术搜索到以后，点击那个引号就可以)，这种方法的缺点是导入之后，还需要手动给该文献附加pdf文件。



## 文献分组



为了便于查看，自己可以添加不同的group，用来对特定的project的文献进一步管理，就像有子文件夹一样，支持拖动。



## 文献标注



Endnote的主要功能是管理，只支持一些基本的操作，可以对pdf做批注、给不同文献排一个重要性的序等。批注时批注功能是由你系统默认代开的pdf阅读器来决定的，如果默认是sumatra pdf打开，则完全没有批注功能。







# 如何从word导入文献



如果你是用word来写作并投稿，那么安装好Endnote之后，就可以直接插入了，插入的方式有两种：



1. 直接再你要插入文献的地方，点菜单栏的*Endnote*的，然后点击*insert citation*，就会弹出一个endnote的插入文献的框，输入文献的关键字就会出现相应的文件，双击就可以了。

2. word保持打开并且游标位于你要插入文献的位置，直接打开endnote，选中你要插入的文献，点击上方的那个双引号图标，就会将你选中的文献插入进去。



# 如何从latex导入文献



如果你是用latex写作投稿，那么你需要将你要引用的文献，在Endnote里面导出为txt文件，格式选择为bibtex格式，导出后将后缀名改为bib，就有了你想要的bib文件，可以直接在latex中引用了。

*此方法的缺点*：在有一些特殊字符（如德文）的情况下，此方法导出的txt文件字符会变成乱码。这时候推荐你自己去文献源文章下载bibtex文件，拷贝内容到bib文件中即可。



# 如何给别人分享你的文献库



Endnote一个很重要的功能是可以比较方便的分享自己文献，每一个文献库有一个“enl”文件以及一个同名的data源文件夹构成，将文件夹和enl文件一起打包传输给别人，就可以将自己的文献分享给别人了。



# 如何更改引用的样式(citation style)

如果更改引用的样式，比如bibtex，比如APS旗下的Phys. Rev. Lett. 需要点击edit>output styles,选择你想要的样式，

![选择特定的引用样式](https://raw.githubusercontent.com/knifelees3/my_pictures/master/picgoup/Snipaste_2019-12-25_14-01-17.png)



如果展示的样式没有你想要的，点击edit>output styles>open style manager,有更多丰富的选择

![在mannager有更丰富的选择](https://raw.githubusercontent.com/knifelees3/my_pictures/master/picgoup/Snipaste_2019-12-25_14-01-53.png)





如果还是没有，可以点击get more on the web, 从[官网](http://endnote.com/support/enstyles.asp)搜索下载。然后将下载的文件复制到安装文件夹的style目录，我的是“C:\Program Files (x86)\EndNote X9\Styles”。



也可以双击style文件,点击file>save 就将style保存到对应目录了。



# 如何添加缩写（Abbreviation）

通过pdf添加的文献信息的杂志名字是一个全名，比如physical review letters,一般文章投稿都需要写成简写，可以从[CASSI](https://cassi.cas.org/search.jsp)查看标准杂志的缩写。要添加更改缩写，点击tool>open term list>journal term list,



![Term List](https://raw.githubusercontent.com/knifelees3/my_pictures/master/picgoup/Snipaste_2019-12-25_14-13-32.png)





可以为不同的文献添加多个缩写，比如我为Optics Letters添加的第一个缩写： Opt. Lett.

![示例](https://raw.githubusercontent.com/knifelees3/my_pictures/master/picgoup/Snipaste_2019-12-25_14-15-35.png)





这样还不够，还需要到对应的应用样式里面将style的缩写选成你想要的。点击edit>output styles>open style manager,选中你要更改的样式，邮件edit style,选中journal name,默认是全名，你可以选择你刚才定义的缩写。

![重新定义缩写](https://raw.githubusercontent.com/knifelees3/my_pictures/master/picgoup/Snipaste_2019-12-25_14-19-47.png)



# 巧用web of science

我们搜索文献除了可以去google学术，google, 以及对应期刊搜索外，还可以去web of science搜索，而endnote支持web of science搜索并下载全文，点击online search

![online search](https://raw.githubusercontent.com/knifelees3/my_pictures/master/picgoup/Snipaste_2019-12-25_14-34-37.png)



然后选择对应的库，我选择的是web of science core,点choose

![库选择](https://raw.githubusercontent.com/knifelees3/my_pictures/master/picgoup/Snipaste_2019-12-25_14-36-23.png)



就会有一个搜索框出来，和在本地搜索一样，可以按照标题、杂志、作者等搜索，一般按照作者搜索结果会特别多，推荐按照文章名字搜索，

![搜索示例](https://raw.githubusercontent.com/knifelees3/my_pictures/master/picgoup/search_web_of_science.gif)

然后选中自己要的文献，添加到自己的group即可，

![添加到group](https://raw.githubusercontent.com/knifelees3/my_pictures/master/picgoup/Snipaste_2019-12-25_14-47-10.png)

此时只是有了对应的文件信息，如果想要pdf文件，不需要再去手动下载，只需要选中刚才添加的文献，右键find fulltext,过一会儿就会发现pdf文件已经下载下来了。

![查找全文](https://raw.githubusercontent.com/knifelees3/my_pictures/master/picgoup/Snipaste_2019-12-25_14-48-41.png)

















