---
title: Python数据的保存文件类型
date: 2019-04-25 19:43:37
tags:
- Python
categories:
- 技术
---
最近在用python扫描参数计算，在用MATALAB的时候，比较喜欢保存为CSV文件或者是txt文件，这些文件的好处是可以用记事本或者excel打开看，缺点是占用的空间太大。后来MATLAB我比较倾向于用“.mat”文件来保存，这样文件就会比较小。MATLAB保存为.mat文件只要如下命令

```matlab
save('xxx.mat','matA','matB',...)
```

python也支持以上所有的文件格式，还支持npy文件。用法如下

```python
import numpy as np
import scipy.io as scio
## 程序主体部分
....
##保存部分
np.savetxt("MaxSym4CavSmallRange.txt", matA)
scio.savemat("MaxSym4CavSmallRange.mat", {'NameA':matA})
np.save("MaxSym4CavSmallRange.npy", matA)
np.savez("MaxSym4CavSmallRange.npy", matA,matB,matC)
```

因此python不仅支持读取与保存mat文件，还有自己独有的npy文件，这两种文件都是不能用记事本打开，但是都占开年较小，比如我计算的文件，保存为txt文件时占355kB,但是保存成npy格式或者mat格式，都只占114kB.这种方法适合保存一些比较大的数据，比较节省空间。
