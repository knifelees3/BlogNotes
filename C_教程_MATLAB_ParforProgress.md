# MATLAB parfor 进度的提取

# MATLAB parfor 进度显示



用MATLAB的时候，经常会用到并行计算，用于加快速度。我们有时候还需要知道程序具体运行到哪一步，比如循环一个有100个，已经运行了多少个。如果不是parfor,我们可以采用每进行一次运算，就输出一些信息到文件的方法，比如



```matlab

    N=10;

    fid=fopen('progress.txt','at');

    for l=1:

    fprintf(fid,[datestr(now),' the loop step is %d \n'],l);

    end

    fclose(fid);

```



这样的话，就会在程序里面输出每一个循环已经执行的信息。可以看见输出的txt文件夹具有如下的内容：



```matlab

02-Mar-2019 23:50:17 the loop step is 1  

02-Mar-2019 23:50:17 the loop step is 2  

02-Mar-2019 23:50:17 the loop step is 3  

02-Mar-2019 23:50:17 the loop step is 4  

02-Mar-2019 23:50:17 the loop step is 5  

02-Mar-2019 23:50:17 the loop step is 6  

02-Mar-2019 23:50:17 the loop step is 7  

02-Mar-2019 23:50:17 the loop step is 8  

02-Mar-2019 23:50:17 the loop step is 9  

02-Mar-2019 23:50:17 the loop step is 10  

```



上面的



```matlab

datestr(now)

```



可以得到当前的时间。这是对于普通循环的用法，如果是parfor呢？因为并行计算会调用多个cpu进行计算，此时如果接着用上面的命令，就会出现多个内核同时对同一个文件处理，在服务器上面计算就会因为文件权限问题报错



```bash

错误使用 parfor_matlab (line 3)

文件标识符无效。使用 fopen 生成有效的文件标识符。

```



为了避免这种错误，我们可以将上面的对文件的操作放在parfor里面，即



```matlab

    N=10;

    parfor l=1:

    fid=fopen('progress.txt','at');

    fprintf(fid,[datestr(now),' the loop step is %d \n'],l);

    fclose(fid);

    end

```



这样每次运行出一个结果，就可以输出一个结果到文件，且不会相互冲突。还需要注意的是，我们这里输出的结果不是按顺序的，而是不同cpu计算的结果随机填充到文件里面,我们必须手动数一数输出了几行结果到文件里面了，如下。



```matlab

03-Mar-2019 00:02:45 the loop step is 10  

03-Mar-2019 00:03:03 the loop step is 4  

03-Mar-2019 00:03:03 the loop step is 7  

03-Mar-2019 00:03:03 the loop step is 1  

03-Mar-2019 00:03:03 the loop step is 3  

03-Mar-2019 00:03:03 the loop step is 6  

03-Mar-2019 00:03:03 the loop step is 5  

03-Mar-2019 00:03:03 the loop step is 2  

03-Mar-2019 00:03:03 the loop step is 8  

03-Mar-2019 00:03:03 the loop step is 10  

03-Mar-2019 00:03:03 the loop step is 9  

```



可以看见，上面的结果是随机的，为了具体知道到底计算了几个循环了，有两个办法，一是用文本编辑器打开txt文件，一般都会在左边显示行数，数有几行，就可以知道计算了几个了。第二个方法是我们可以再次读取一下我们的txt文件，数一数其矩阵的大小，就可以知道具体计算了多少行了。代码如下



```matlab

%每次运行确保文件‘progress_1.txt'，‘progress_2.txt'都是空的

  N=10;

   for l=1:N

   %首先输出一个运行循环的结果到'progress_1.txt'文件

    fid=fopen('progress_1.txt','a');

    fprintf(fid,[datestr(now),' the loop step is %d \n'],l);

    fclose(fid);

   %然后从'progress_1.txt'文件读取文件的字符长度

    fid=fopen('progress_1.txt','r');

    [A, count]=fscanf(fid,'%s');%count是读取字符的个数，我们每一行都有7个字符，所以count是7的倍数

    fclose(fid);

    fid=fopen('progress_2.txt','a');

    %最后在另外一个文件输出我们的总共计算了多少步

    fprintf(fid,[datestr(now),' has looped for  %d  steps \n'],count/7);

    fclose(fid);

    end

```



这样就可以在文件里面实时查看我们的计算进度了。这样的坏处是由于我们频繁读取文件，运行速度会变慢，对于每一个parfor循环都需要很久的情况，这种方法是值得一试的。前面讲的都是在非图形界面的情况，如果我们有图形界面，其实还有更加好的解决方法，可以一边计算，一边显示百分比。在matlab的英文社区搜索“parfor progressbar”，就会有很多的结果，下面我展示一个我认为最好的解决方法，不需要额外的java之类的,我们需要将下面这段代码保存为“parfor_progressbar_v1.m”，和要计算的代码放在同一个文件夹，计算时候调用即可。下面也已经有了调用的例子。



```matlab

classdef parfor_progressbar_v1 < handle

% PARFOR_PROGRESSBAR  Progress bar suitable for multi-process computation.

%

%   H = parfor_progressbar(N, 'message', 'property',value, ...)

%   creates a graphical progress bar with N iterations before completion.

%   A temporary file in tempdir is used to communicate among threads.

%   Any property/value pairs are passed to waitbar internally (optional).

%

%   H.iterate(X) updates the progress bar by X iterations.

%

%   Example:

%   --------

%     N=50;    %total number of parfor iterations

%     hbar = parfor_progressbar(N,'Computing...');  %create the progress bar

%     parfor i=1:N,

%         pause(rand);       % computation

%         hbar.iterate(1);   % update progress by one iteration

%     end

%     close(hbar);   %close progress bar

%

%   Notes:

%   ------

%   Properties cannot be modified while inside a parfor loop. Use iterate only.

%

%   With many short iterations, call iterate() periodically. Example:

%     if mod(i,10)==0,  hbar.iterate(10);  end

%

%   Inspired by the parfor_progress script made by Jeremy Scheff:

%   http://www.mathworks.com/matlabcentral/fileexchange/32101

%

%   See also: WAITBAR, PARFOR.



%   Copyright 2015-2016 Cornell University All Rights Reserved.







% Public properties

properties (SetAccess=protected, GetAccess=public)

    wbh;      % Waitbar figure object handle

    N;        % Total number of iterations expected before completion

    Msg;

end



properties (Dependent, GetAccess=public)

    percent;  % Percentage of completed iterations

end



properties (Dependent, SetAccess=public, GetAccess=public)

    message;  % Message text displayed in waitbar

end



% Internal properties

properties (SetAccess=protected, GetAccess=protected, Hidden)

    ipcfile;  % Path to temporary file for inter-process communication

    htimer;   % Timer object that checks ipcfile for completed iterations

end







methods

    %========================  CONSTRUCTOR  ========================%

    function this = parfor_progressbar_v1(N_init, varargin)

    % Create a new progress bar with N_init iterations before completion.

        

        % Create a unique inter-process communication file.

        for i=1:10

            f = sprintf('%s%d.txt', mfilename, round(rand*1000));

            this.ipcfile = fullfile(tempdir, f);

            if ~exist(this.ipcfile,'file'), break; end

        end



        if exist(this.ipcfile,'file')

            error('Too many temporary files. Clear out tempdir.');

        end

    

        % Create a new waitbar 

        this.N = N_init;

        this.Msg = varargin{1};

        this.wbh = waitbar(0, [this.Msg, '0% Complete']);

        

        % Create timer to periodically update the waitbar in the GUI thread.

        this.htimer = timer( 'ExecutionMode','fixedSpacing', 'Period',0.5, ...

                             'BusyMode','drop', 'Name',mfilename, ...

                             'TimerFcn',@(x,y)this.tupdate );

        start(this.htimer);

    end

    

    

    %=========================  DESTRUCTOR  ========================%

    function delete(this)

        this.close();

    end

    

    function close(this)

    % Closer the progress bar and clean up internal state.

    

        % Stop the timer

        if isa(this.htimer,'timer') && isvalid(this.htimer)

            stop(this.htimer);

            pause(0.01);

            delete(this.htimer);

        end

        this.htimer = [];

        

        % Delete the IPC file.

        if exist(this.ipcfile,'file')

            delete(this.ipcfile);

        end

        

        % Close the waitbar

        if ishandle(this.wbh)

            close(this.wbh);

        end

        this.wbh = [];

    end

    

    

    %======================  GET/SET METHODS  ======================%

    function percent = get.percent(this)

    % Calculate the fraction of completed iterations from IPC file.

        if ~exist(this.ipcfile, 'file')

            percent = 0;  % File may not exist before the first iteration

        else

            fid = fopen( this.ipcfile, 'r' );

            percent = sum(fscanf(fid, '%d')) / this.N;

            percent = max(0, min(1,percent) );

            fclose(fid);

        end

    end

    

    

    function set.message(this, newMsg)

    % Update the progress bar's displayed message.

    

        if ishandle(this.wbh)

            waitbar( this.percent, this.wbh, newMsg );

        end

    end

    

    

    function iterate(this, Nitr)

    % Update the progress bar by Nitr iterations (or 1 if not specified).

        if nargin<2,  Nitr = 1;  end

    

        fid = fopen(this.ipcfile, 'a');

        fprintf(fid, '%d\n', Nitr);

        fclose(fid);

    end

    

    

end %public methods







%=====================  INTERNAL METHODS  =====================%

methods (Access=protected, Hidden)

    

    

    function tupdate(this)

    % Check the IPC file and update the waitbar with progress.

    

        if ishandle(this.wbh)

            waitbar( this.percent, this.wbh, sprintf('%s...%2.0f%% complete', this.Msg, this.percent*100));

        else

            % Kill the timer if the waitbar is closed.

            close(this);

        end

    end 

end %private methods









end %classdef

```



## 输出屏幕信息到文件的方法

*20190629*

一种更好的方法是将运行matlab时屏幕的一些显示信息直接保存到另外的文件，命令为



``` bash

#!/bin/bash



# Call MATLAB with the appropriate input and output.

# Be careful to include 'exit' MATLAB command in M-file.

# Insert a cd command in the main M-file to change the working directory.

# Run the matlab program using runmatlab.sh myfile.m myoutput.txt. 

# Save workspace.mat. 



#nohup /opt/matlab/bin/matlab -nodisplay -nodesktop -nosplash < $1 &> $2 &

# nohup /opt/matlab/bin/matlab -nodisplay -nodesktop -nosplash < test.m &> output.txt &

nohup /opt/matlab/bin/matlab -nodisplay -nodesktop -nojvm -nosplash < test.m &> output.txt &

```



比如我们的测试文件'test.m'如下



```matlab

for l=1:10

l+1

end

exit;

```



那么运行上面的脚本之后，最后得到的‘output.txt’文件如下



```bash



                            < M A T L A B (R) >

                  Copyright 1984-2015 The MathWorks, Inc.

                   R2015b (8.6.0.267246) 64-bit (glnxa64)

                              August 20, 2015



 

For online documentation, see http://www.mathworks.com/support

For product information, visit www.mathworks.com.

 

>> 

ans =



     2





ans =



     3





ans =



     4





ans =



     5





ans =



     6





ans =



     7





ans =



     8





ans =



     9





ans =



    10





ans =



    11



>> 

```



即我们可以将屏幕的结果实时的输出到文件里。
