---
title: Parallel computing summary
date: 2019-04-17 15:55:59
tags:
- MATLAB
- Python
categories: 
- 技术
- EnglishNotes
---

## Introduction

In this note I am going to summarize the parallel computing in MATLAB and python. We need emphasize that the parallel computing needs no iteration or causal relationship between different loops.

## MATLAB

In MATLAB we just need to use 'parfor' to realize parallel computing. Here is a simple example

```matlab
poolnum=10; % numbers of kernels
kernum=parpool(poolnum)
parfor l=1:numloop
%do something here
end
delete(kernum)
%the delete step is very important because in cluster we may use  more than a dozen cores.If we stop the program directly without closing the parallel pool, the cluster may crash or take a long time to become normal.
```

There are many constrains on the "parfor" loop, for example, the expression "A(:,l)=B" may not be used in "parfor" loop. Here is only a very simple summary about how to use "parfor".

## Python

Python may be faster compared with MATLAB in some cases  when a part of the program directly calls the C language. If we want to use Python to do parallel computation, we need use the 'multiprocessing' package.
Very detailed introduction and examples can be found in this 

https://docs.python.org/3.4/library/multiprocessing.html?highlight=process

There are many different ways of achieving multiprocessing (not multi threads which will be restriced by GIL in python), here I show the simplest realization by using "pool"

```python
import multiprocessing as mp
import numpy as np
%use a function to define what we want to do
def fun=(a,b,c,d):
#do something here
    return fun
# number of process you are going to use
processnum=10

if __name__ == '__main__':#this is needed in windows
    pool = mp.Pool(processes=processnum) 
    #results1 = [pool.apply(fun, args=(l,loop_mat)) for l in range(numloop)] 
    #get the  ordered values directly and store the results in results1
    results2 = [pool.apply_async(fun, args=(l,loop_mat)) for l in range(numloop)] 
    #get the values arbitrarily
    value_1= [p.get() for p in results2]# use this get function to obtain the calculated value
    pool.terminate() #shut down
```

What needs to be emphasized is that the paralleling computing should be used in which the single process is very slow and  each core do the job very slowly. We shouldn't distribute many small jobs which needs very short time to complete. Then most of the time will be used to distribute works.

