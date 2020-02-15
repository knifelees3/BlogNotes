# How to use COMSOL, MATLAB and COMSOL livelink with MATLAB on Server



This note is to show the way of using MATLAB, COMSOL,COMSOL Livelink With MATLAB on our server   (ubuntu). We hope that we can run them with bash code in backgorund and after we logout or exit the server the simulations will continue. We also need to know the simulation progress from a log file. These needs can all be satisfied only if you write proper bash code.



## Run COMSOL on server



If you want to run COMSOL on server, you can use the command of the following form



```bash

nohup comsol batch -inputfile <inputfilename> -outputfile <outputfilename> -batchlog <logfilename> -np <number of cores> &

```



above command shows the smallest example and  the "< >" isn't included in the actual terminal command. The form `nohup <command> &` is used to execute the command in the background even if we logout from the server. To avoid confusion, I give a more specific example, If we want to simulate the file "test.mph", then the command should be as follows



```bash

nohup comsol batch -inputfile test.mph -outputfile test_out.mph -batchlog test.log -np 30 &

```



In above example we  use 30 cores (set with "-np 30")to simulate our mph file. If we have many mph files to simulate, we can write a bash code to arrange our simulation works. We create a file with the name "comsolscript.sh" with the following content



```bash

#! /bin/bash

nohup comsol batch -inputfile test1.mph -outputfile test1_out.mph -batchlog test1.log -np 30 &&

nohup comsol batch -inputfile test2.mph -outputfile test2_out.mph -batchlog test2.log -np 30 &&

nohup comsol batch -inputfile test3.mph -outputfile test3_out.mph -batchlog test3.log -np 30 &

```



Above code will simulate the file "test1.mph", "test2.mph", "test3.mph" respectively. The "&&" at the end of the line will let the server to execute the next command only when this command complete. if you use "&" then all the mission will simultaneously execute. You need upload the "comsolscript.sh" file to the correct folder and make it executable



```bash

chmod +x ./comsolscript.sh

```



then in the corresponding folder type



```bash

./comsolscript.sh

```



The simulation will begin and you can see the progress from the log file by typing `vi test.log`.



If you write the bash code on windows then upload the file to the server, when you try to run the bash file there may be error: "`/bin/bash^M:bad interpreter:No such file or directory`", this is because of the difference of coding in Unix and Windows. You can use the following command in the corresponding folder to fix it



```bash

sed -i -e 's/\r$//' ./comsolscrpt.sh

```



if you use vi on the server to create the bash file, this error can also be avoided.



## Run MATLAB on server



Before using the MATLAB on server, you need make sure that the matlab is in the system enviroment path. The method of adding the MATLAB path to the system enviroemnt can be found from my another note [Ubuntu安装COMSOL,MATLAB以及FDTD Solutions](https://knifelees3.github.io/2020/01/01/C_%E6%95%99%E7%A8%8B_Ubuntu_%E5%AE%89%E8%A3%85COMSOL_MATLAB_FDTD%20Solutions/).



If you want to run matlab without displaying the desktop, you can type



```bash

matlab -nodekstop -nosplash -nojvm

```



If you want to run a file in the background, you can type the following command



```bash

nohup matlab -nodesktop -nosplash -nojvm <test.m> progress.txt &

```



above code run the  "test.m" in the background and save the screen display into the file "progress.txt", so we can know the progress from the file. "-nojvm" is used to hide the plot progress if you don't want to see the plot during the simulation. When the simulation meets some problems, there will be a "nohup.out"  file to show the error information.



A better choice is to use a bash file "matlabscript.sh" to run the corresponding MATLAB file.



```bash

#! /bin/bash

matlab -nodesktop -nosplash -nojvm <test1.m;test2.test3.m;exit;> progress.txt

```



Above bash file doesn't use the "nohup command &" and it will not run in the background. If you want to run in the background, you can type



```bash

nohup ./matlabscript.sh &

```



The "exit" is important and if not after the simulation the MATLAB will be still alive in the background, then you need kill the MATLAB by typing `kill <pid of MATLAB progress>`.



## Run COMSOL live link with MATLAB on server



The usage of COMSOL live link with MATLAB can be found on the installation folder of COMSOL, the detailed usage is in the file "LiveLinkForMATLABUsersGuide.pdf".



If you can use the graphics window, then you can run a MATLAB file "test.m" to run a COMSOL file by typing



```bash

comsol mphserver matlab test

```



You can also run the script in batch without the MATLAB desktop and the MATLAB splash screen. Enter this command:



```bash

comsol mphserver matlab test -nodesktop -mlnosplash

```



However, if you want to run the script in the background, you can not just simply add a "nohup+command+&", I don't know the reason. From the "LiveLinkForMATLABUsersGuide.pdf", we can see the following words



>To connect COMSOL with a MATLAB terminal requires that xterm is installed on the machine. If this is not the case as it might be for a computation COMSOL server, a workaround is to connect manually MATLAB to a COMSOL server with the function *mphstart*.



After trying for a while I finally know how to run the COMSOL livelink with MATLAB in the background on server. We need to create four files named "matlab_exe.m","test.m","comsolscript.sh","test.mph".



- "test.mph" is the COMSOL file you want to simulate.

- "test.m" is the file to run "test.mph" from MATLAB.

- "matlab_exe.m" is used to link the MATLAB with COMSOL mphserver and run the "test.m" file and finally exit MATLAB.

- "comsolscript.sh" is the bash code to open the COMSOL mphserver and run the file "matlab_exe.m"

the following is the detailed code.



**For "matlab_exe.m"**



```matlab

% This code is to connect to the COMSOL livelink with MATLAB server



% add the livelink path to the server for comsol5.4

addpath('/usr/local/comsol54/multiphysics/mli/'); 



% connect to the server, the default port number is 2036 and then 2037 ...

mphstart(2036)



% the MATLAB file you want to run

test;



% exit the program

exit;

```



**For "comsolscript.sh"**



```bash

#! /bin/bash

# if the run the file and getting the error "/bin/bash^M:bad interpreter:No such file or directory",you can use 

# the following command in the corresponding cluster to fix it

# sed -i -e 's/\r$//' scriptname.sh





# this is to run the MATLAB file in script

# First start the COMSOL livelink with MATLAB for 5.4

# use "np" to define the number of cores you will use

comsol54 mphserver -np 28 -silent &



# run the MATLAB file

# The "screenout.txt" will store the screen output for MATLAB

matlab -nodesktop -nosplash  <matlab_exe.m> screenout.txt

```



**For "test.m"**



```matlab

% save the COMSOLcprogress file as "COMSOL_Progress.txt" during simulations

clear;clc;

import com.comsol.model.*

import com.comsol.model.util.*

ModelUtil.showProgress('COMSOL_Progress.txt');



% other command

%........

```



The note ends here. Thanks for your reading, if you have any questions please contact me

knifelees3@gmail.com
