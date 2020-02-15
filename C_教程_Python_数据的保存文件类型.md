# Python数据的保存文件类型



最近在用python扫描参数计算，在用MATLAB的时候，比较喜欢保存为CSV文件或者是txt文件，这些文件的好处是可以用记事本或者excel打开看，缺点是占用的空间太大。后来MATLAB我比较倾向于用“.mat”文件来保存，这样文件就会比较小。MATLAB保存为.mat文件只要如下命令



```matlab

save('xxx.mat','matA','matB',...) %依次保存matA,matB文件

save('xxx.mat') %保存工作区的所有文件

```



python也支持以上所有的文件格式，还支持npy文件。用法如下，首先导入包



```python

import numpy as np

import scipy.io as scio

```



## txt 格式



```python

# 保存为txt

np.savetxt("filename.txt", matA)

## 读取为txt

data=np.loadtxt("filename.txt")

```

## mat 格式



```python

# 保存为mat文件

scio.savemat("filename.mat", {'NameA':matA})

# 读取为mat文件

data=scio.loadmat("filename.mat")

# 此处的data文件是一个字典，不同的矩阵、数值需要依次取出来。

matA = data['matA']

matB = data['matB']

matC = data['matC']

```



## npy 格式



```python

# 保存为npy文件

np.save("filename.npy", matA)

np.save("filename.npy", matA,matB,matC) #多个矩阵

# 读取npy文件

np.load("filename.npy")

```



因此python不仅支持读取与保存mat文件，还有自己独有的npy文件，这两种文件都是不能用记事本打开，但是都占开年较小，比如我计算的文件，保存为txt文件时占355kB,但是保存成npy格式或者mat格式，都只占114kB.这种方法适合保存一些比较大的数据，比较节省空间。

