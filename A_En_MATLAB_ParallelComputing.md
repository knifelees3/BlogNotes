# MATLAB Parallel Computing Summary





# Simple Introduction



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
