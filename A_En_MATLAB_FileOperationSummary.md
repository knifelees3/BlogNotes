# MATLAB File Operation Summary



In doing research,We often need output the result to the file and read from the file.In this note, I will summarize the methods of reading and output method in MATLAB.



## Deirectly read and write



### mat file



We first consider the method of saving and read the MATLAB type file. The Matrix in MATLAB can be directly saved in a "xx.mat" file. This method can save many different result in an whole single file. I really recommend this method. This can be done as follows:



```matlab

filename=['sweep_result_',datestr(now,'yyyy_mm_dd_HHMMSS'),'.mat'];

save(num2str(filename),'matrixa','matrixb','matrixc');

```



to read the file,



```matlab

load('filename')

```



### csv,txt file



the mat file can only be opened in MATLAB, In order to allow other software to open the output file. We can save the file as txt or csv file. This can be done via csvread/cavwrite, textread/textwrite,dlmwrite/dlmread,And I recommend the dlm method



```matlab

% read csv file via "csvread"

data=csvread('<filename>',<begin row>,<begin column>);

%Write matrix M to a file, 'myFile.txt', delimited by the tab character and using a precision of 3 significant digits

dlmwrite('myFile.txt',M,'delimiter','\t','precision',3)

%Export a matrix to a file named myfile.txt. Then, append an additional matrix to the file that is offset one row below the first

X = magic(3);

dlmwrite('myfile.txt',[X*5 X/5],' ')

dlmwrite('myfile.txt',X,'-append', ...

   'roffset',1,'delimiter',' ')

%ead the entire file using dlmread.

M = dlmread('myfile.txt')

```



## fopen method



this can be done via fopen and fprintf method



```matlab

fid=fopen('progress.txt','at');

fprintf(fid,[datestr(now),' the loop step is %d \n'],lk4);

fclose(fid);

```



## "print" output image to file



to save the figure in the window,the best way is to use print.



```matlab

filename=['xxxxx_','.png'];

print(num2str(filename), '-dpng', '-r600')%for eps,'-deps2'

```

