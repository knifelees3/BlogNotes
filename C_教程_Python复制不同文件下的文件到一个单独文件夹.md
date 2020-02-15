# 用python模糊匹配文件夹下的文件并复制文件到另外的文件夹

# 目的



自己目前在用[VNote](https://github.com/tamlok/vnote)写笔记，这个笔记软件非常便于我们管理本地Markdown文件，具体的用法后续会单独介绍，今天我要记录的是，怎么用python来复制特定的文件。



我的Hexo博客文件夹是Onedrive同步的，单独的文件夹。博客笔记要更新或者修改，我一般不直接对Hexo的文件操作，而是有一个单独的笔记本文件夹，觉得可以分享到网络上的笔记，我会复制到Hexo文件夹下的`_post`文件目录。这样的缺点是有时候会不小心直接在Hexo文件夹下改，而原来的本地文件夹的文件没有修改，造成版本混乱。而且手动复制也很麻烦。有没有更加自动化的操作呢?



用过Linux的都知道，Linux下有通过`*`来模糊匹配的方法，并且有`cp`命令来进行文件的复制。windows我不太清楚，打算通过python来实现，也算是一个学习python的机会。这是本片笔记的目的



# 方法



通过[网络上查询](https://stackoverflow.com/questions/3964681/find-all-files-in-a-directory-with-extension-txt-in-python)，知道了可以通过[os](https://docs.python.org/3/library/os.html)，[shutil](https://docs.python.org/3/library/shutil.html)包来操作文件，具体的

* `os.listdir()` 可以展示某一个文件夹下的文件以及文件夹。缺点是只能展示一级文件夹。

* `os.walk()` 可以遍历某一个文件夹下的所有文件以及文件夹，其返回值根据该[介绍](https://www.geeksforgeeks.org/os-walk-python/)

    >OS.walk() generate the file names in a directory tree by walking the tree either top-down or bottom-up. For each directory in the tree rooted at directory top (including top itself), it yields a 3-tuple (`dirpath`, `dirnames`, `filenames`).



即`os.walk()`返回值有三个，其中



     * `dirpath` 是目标路径下所有文件的路径

     * `dirnames` 是目标路径的所有目录名称

     * `dilenames` 是各个路径下的文件名称列表.

* `shutil.copy` 复制文件从一个文件夹到另外一个文件夹，但是文件的时间都是新的。

* `shutil.copy2` 复制文件从一个文件夹到另外一个文件夹，但是文件的时间保留以前的。



具体的用法google以下就行，不在此赘述。



# 具体实现



具体实现时，首先插入所需要的包



```python

import os

from shutil import copy2

```



然后定义好要操作的文件夹`rootdir`以及目标文件夹`dstdir`，



```python

rootdir = r'C:\Users\...'

dstdir = r'C:\Users\...'

# 我这里缺省掉了，具体的得替换自己的文件夹即可

```



然后需要定义一个函数来遍历文件，复制文件，其定义如下



```python

def get_files(rootdir, dstdir):

    counter = 0 #用来计数一共复制了多少个文件

    for filepath, dirnames, filenames in os.walk(rootdir): #遍历文件夹

        for filename in filenames: #遍历文件

            if 'A_En' in filename or 'B_随笔' in filename or 'C_教程' in filename or 'D_收集' in filename and filename.endswith('.md'): 

            #设置条件，文件含有“A_En”或'B_随笔'...并且以“.md”文件结尾

                counter = counter+1

                # 结合文件夹和文件生成完整的绝对的路径

                long_name = os.path.join(filepath, filename) 

                #f复制文件

                copy2(long_name, dstdir)

                print('已经复制了文件： '+long_name)



    print('一共复制了'+str(counter) + '个文件')

```



注释已经写的很详细，就不再这里多讲了。



# 完整的代码



最后，附上完整代码



```python

import os

from shutil import copy2





def get_files(rootdir, dstdir):

    counter = 0

    for filepath, dirnames, filenames in os.walk(rootdir):

        for filename in filenames:

            if 'A_En' in filename or 'B_随笔' in filename or 'C_教程' in filename or 'D_收集' in filename and filename.endswith('.md'):

                counter = counter+1

                long_name = os.path.join(filepath, filename)

                copy2(long_name, dstdir)

                print('已经复制了文件： '+long_name)



    print('一共复制了'+str(counter) + '个文件')





if __name__ == "__main__":

    rootdir = r'C:Users\test1\'

    dstdir = r'C:\Users\test\'

    get_files(rootdir, dstdir)

```

