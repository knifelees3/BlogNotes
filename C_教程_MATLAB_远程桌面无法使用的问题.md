# Windows系统MATLAB远程桌面使用时报错的问题





windows自带的远程桌面系统非常好用，比一些第三方的软件比如team viewer 要好用一些，因为其实现方式不同，导致也会有一些新的问题。今天要解决的就是MATLAB远程桌面不能使用报错的问题，这是由于MATLAB激活时选择的license文件时stand alone版本，不是服务器版本。在网络上搜索之后，知道如下解决方案：



https://blog.csdn.net/wcx1293296315/article/details/88738119



需要手动修改“C:\Program Files\MATLAB\R2018b\licenses\license*.lic”文件的内容(实际位置和文件需要根据自己的MATLAB版本和位置修改)，在该文件的每一行最后都加上一个“TS_OK”, 前两行如下



```bash

INCREMENT Aerospace_Blockset MLM 369 permanent uncounted \

	VENDOR_STRING=vi=0:at=200:ae=1:lu=300:lo=IN:ei=6257193:lr=1: \

	HOSTID=ANY SN=968398 SIGN=0D8A1582514C TS_OK

INCREMENT Aerospace_Toolbox MLM 369 permanent uncounted \

	VENDOR_STRING=vi=0:at=200:ae=1:lu=300:lo=IN:ei=6257193:lr=1: \

	HOSTID=ANY SN=968398 SIGN=13FDDFF8C36C TS_OK

```



如果手动一行一行的加太麻烦了，可以选择用正则表达式的方法来查找替换，一般的编辑器都是支持的，我用的时sublime, 输入“ctrl+f+h”，查找`([^\\])($)`,替换为`\1 TS_OK`,即可.



**也有遇到过情况，在“licenses”文件夹下没有“lic”文件，这时候就需要自己手动创建一个即可。**



我这里附上一些lic文件内容，自己创建一个“.lic”文件，复制粘贴内容，替换原文件即可



## MATLAB R2018b



```bash

INCREMENT Aerospace_Blockset MLM 369 permanent uncounted \

	VENDOR_STRING=vi=0:at=200:ae=1:lu=300:lo=IN:ei=6257193:lr=1: \

	HOSTID=ANY SN=968398 SIGN=0D8A1582514C TS_OK

INCREMENT Aerospace_Toolbox MLM 369 permanent uncounted \

	VENDOR_STRING=vi=0:at=200:ae=1:lu=300:lo=IN:ei=6257193:lr=1: \

	HOSTID=ANY SN=968398 SIGN=13FDDFF8C36C TS_OK

INCREMENT Antenna_Toolbox MLM 369 permanent uncounted \

	VENDOR_STRING=vi=0:at=200:ae=1:lu=300:lo=IN:ei=6257193:lr=1: \

	HOSTID=ANY SN=968398 SIGN=2A01DAAA9886 TS_OK

INCREMENT Audio_System_Toolbox MLM 369 permanent uncounted \

	VENDOR_STRING=vi=0:at=200:ae=1:lu=300:lo=IN:ei=6257193:lr=1: \

	HOSTID=ANY SN=968398 SIGN=E025BF62EAD8 TS_OK

INCREMENT Automated_Driving_Toolbox MLM 369 permanent uncounted \

	VENDOR_STRING=vi=0:at=200:ae=1:lu=300:lo=IN:ei=6257193:lr=1: \

	HOSTID=ANY SN=968398 SIGN=C318246C14E2 TS_OK

INCREMENT Bioinformatics_Toolbox MLM 369 permanent uncounted \

	VENDOR_STRING=vi=0:at=200:ae=1:lu=300:lo=IN:ei=6257193:lr=1: \

	HOSTID=ANY SN=968398 SIGN=358194AE1548 TS_OK

INCREMENT Cert_Kit_IEC MLM 369 permanent uncounted \

	VENDOR_STRING=vi=0:at=200:ae=1:lu=300:lo=IN:ei=6257193:lr=1: \

	HOSTID=ANY SN=968398 SIGN=60C2E6F826CE TS_OK

INCREMENT Communication_Blocks MLM 369 permanent uncounted \

	VENDOR_STRING=vi=0:at=200:ae=1:lu=300:lo=IN:ei=6257193:lr=1: \

	HOSTID=ANY SN=968398 SIGN=CF5D32DAABBA TS_OK

INCREMENT Communication_Toolbox MLM 369 permanent uncounted \

	VENDOR_STRING=vi=0:at=200:ae=1:lu=300:lo=IN:ei=6257193:lr=1: \

	HOSTID=ANY SN=968398 SIGN=253B4EECBE48 TS_OK

INCREMENT Compiler MLM 369 permanent uncounted \

	VENDOR_STRING=vi=0:at=200:ae=1:lu=300:lo=IN:ei=6257193:lr=1: \

	HOSTID=ANY SN=968398 SIGN=2DD1C464FD06 TS_OK

INCREMENT Control_Toolbox MLM 369 permanent uncounted \

	VENDOR_STRING=vi=0:at=200:ae=1:lu=300:lo=IN:ei=6257193:lr=1: \

	HOSTID=ANY SN=968398 SIGN=E0D5C4184FB6 TS_OK

INCREMENT Curve_Fitting_Toolbox MLM 369 permanent uncounted \

	VENDOR_STRING=vi=0:at=200:ae=1:lu=300:lo=IN:ei=6257193:lr=1: \

	HOSTID=ANY SN=968398 SIGN=583BAC2E0F7A TS_OK

INCREMENT Data_Acq_Toolbox MLM 369 permanent uncounted \

	VENDOR_STRING=vi=0:at=200:ae=1:lu=300:lo=IN:ei=6257193:lr=1: \

	HOSTID=ANY SN=968398 SIGN=48ECF5F6B11E TS_OK

INCREMENT Database_Toolbox MLM 369 permanent uncounted \

	VENDOR_STRING=vi=0:at=200:ae=1:lu=300:lo=IN:ei=6257193:lr=1: \

	HOSTID=ANY SN=968398 SIGN=E9929C7A187A TS_OK

INCREMENT DATAFEED_TOOLBOX MLM 369 permanent uncounted \

	VENDOR_STRING=vi=0:at=200:ae=1:lu=300:lo=IN:ei=6257193:lr=1: \

	HOSTID=ANY SN=968398 SIGN=9876C540CA8E TS_OK

INCREMENT Dial_and_Gauge_Blocks MLM 369 permanent uncounted \

	VENDOR_STRING=vi=0:at=200:ae=1:lu=300:lo=IN:ei=6257193:lr=1: \

	HOSTID=ANY SN=968398 SIGN=EFBA589A1810 TS_OK

INCREMENT Distrib_Computing_Toolbox MLM 369 permanent uncounted \

	VENDOR_STRING=vi=0:at=200:ae=1:lu=300:lo=IN:ei=6257193:lr=1: \

	HOSTID=ANY SN=968398 SIGN=D995C292E03A TS_OK

INCREMENT Econometrics_Toolbox MLM 369 permanent uncounted \

	VENDOR_STRING=vi=0:at=200:ae=1:lu=300:lo=IN:ei=6257193:lr=1: \

	HOSTID=ANY SN=968398 SIGN=D1EC25D000D8 TS_OK

INCREMENT eda_simulator_link MLM 369 permanent uncounted \

	VENDOR_STRING=vi=0:at=200:ae=1:lu=300:lo=IN:ei=6257193:lr=1: \

	HOSTID=ANY SN=968398 SIGN=DE5E67B09746 TS_OK

INCREMENT Embedded_IDE_Link MLM 369 permanent uncounted \

	VENDOR_STRING=vi=0:at=200:ae=1:lu=300:lo=IN:ei=6257193:lr=1: \

	HOSTID=ANY SN=968398 SIGN=FB290E548926 TS_OK

INCREMENT Excel_Link MLM 369 permanent uncounted \

	VENDOR_STRING=vi=0:at=200:ae=1:lu=300:lo=IN:ei=6257193:lr=1: \

	HOSTID=ANY SN=968398 SIGN=E6527A880B26 TS_OK

INCREMENT Filter_Design_HDL_Coder MLM 369 permanent uncounted \

	VENDOR_STRING=vi=0:at=200:ae=1:lu=300:lo=IN:ei=6257193:lr=1: \

	HOSTID=ANY SN=968398 SIGN=44F6103EBB0E TS_OK

INCREMENT Filter_Design_Toolbox MLM 369 permanent uncounted \

	VENDOR_STRING=vi=0:at=200:ae=1:lu=300:lo=IN:ei=6257193:lr=1: \

	HOSTID=ANY SN=968398 SIGN=58CB0596F32E TS_OK

INCREMENT Fin_Derivatives_Toolbox MLM 369 permanent uncounted \

	VENDOR_STRING=vi=0:at=200:ae=1:lu=300:lo=IN:ei=6257193:lr=1: \

	HOSTID=ANY SN=968398 SIGN=9E9A2B0020BA TS_OK

INCREMENT Fin_Instruments_Toolbox MLM 369 permanent uncounted \

	VENDOR_STRING=vi=0:at=200:ae=1:lu=300:lo=IN:ei=6257193:lr=1: \

	HOSTID=ANY SN=968398 SIGN=325A84A84E4A TS_OK

INCREMENT Financial_Toolbox MLM 369 permanent uncounted \

	VENDOR_STRING=vi=0:at=200:ae=1:lu=300:lo=IN:ei=6257193:lr=1: \

	HOSTID=ANY SN=968398 SIGN=698F9FC2DDDE TS_OK

INCREMENT Fixed_Income_Toolbox MLM 369 permanent uncounted \

	VENDOR_STRING=vi=0:at=200:ae=1:lu=300:lo=IN:ei=6257193:lr=1: \

	HOSTID=ANY SN=968398 SIGN=75BBDA60AC74 TS_OK

INCREMENT Fixed_Point_Toolbox MLM 369 permanent uncounted \

	VENDOR_STRING=vi=0:at=200:ae=1:lu=300:lo=IN:ei=6257193:lr=1: \

	HOSTID=ANY SN=968398 SIGN=BF695EBE4514 TS_OK

INCREMENT Fixed-Point_Blocks MLM 369 permanent uncounted \

	VENDOR_STRING=vi=0:at=200:ae=1:lu=300:lo=IN:ei=6257193:lr=1: \

	HOSTID=ANY SN=968398 SIGN=22A5B32025E6 TS_OK

INCREMENT Fuzzy_Toolbox MLM 369 permanent uncounted \

	VENDOR_STRING=vi=0:at=200:ae=1:lu=300:lo=IN:ei=6257193:lr=1: \

	HOSTID=ANY SN=968398 SIGN=90FDC43A584E TS_OK

INCREMENT GADS_Toolbox MLM 369 permanent uncounted \

	VENDOR_STRING=vi=0:at=200:ae=1:lu=300:lo=IN:ei=6257193:lr=1: \

	HOSTID=ANY SN=968398 SIGN=38C864060ECE TS_OK

INCREMENT GPU_Coder MLM 369 permanent uncounted \

	VENDOR_STRING=vi=0:at=200:ae=1:lu=300:lo=IN:ei=6257193:lr=1: \

	HOSTID=ANY SN=968398 SIGN=D24A7C12C544 TS_OK

INCREMENT Identification_Toolbox MLM 369 permanent uncounted \

	VENDOR_STRING=vi=0:at=200:ae=1:lu=300:lo=IN:ei=6257193:lr=1: \

	HOSTID=ANY SN=968398 SIGN=2620D11C4600 TS_OK

INCREMENT Image_Acquisition_Toolbox MLM 369 permanent uncounted \

	VENDOR_STRING=vi=0:at=200:ae=1:lu=300:lo=IN:ei=6257193:lr=1: \

	HOSTID=ANY SN=968398 SIGN=43B59340F0FC TS_OK

INCREMENT Image_Toolbox MLM 369 permanent uncounted \

	VENDOR_STRING=vi=0:at=200:ae=1:lu=300:lo=IN:ei=6257193:lr=1: \

	HOSTID=ANY SN=968398 SIGN=23C1BC2A0B00 TS_OK

INCREMENT Instr_Control_Toolbox MLM 369 permanent uncounted \

	VENDOR_STRING=vi=0:at=200:ae=1:lu=300:lo=IN:ei=6257193:lr=1: \

	HOSTID=ANY SN=968398 SIGN=C33239E4EABA TS_OK

INCREMENT LTE_HDL_Toolbox MLM 369 permanent uncounted \

	VENDOR_STRING=vi=0:at=200:ae=1:lu=300:lo=IN:ei=6257193:lr=1: \

	HOSTID=ANY SN=968398 SIGN=CBEB4DC65DDE TS_OK

INCREMENT LTE_Toolbox MLM 369 permanent uncounted \

	VENDOR_STRING=vi=0:at=200:ae=1:lu=300:lo=IN:ei=6257193:lr=1: \

	HOSTID=ANY SN=968398 SIGN=DF335124FDAE TS_OK

INCREMENT MAP_Toolbox MLM 369 permanent uncounted \

	VENDOR_STRING=vi=0:at=200:ae=1:lu=300:lo=IN:ei=6257193:lr=1: \

	HOSTID=ANY SN=968398 SIGN=E927B964E6F2 TS_OK

INCREMENT MATLAB MLM 369 permanent uncounted \

	VENDOR_STRING=vi=0:at=200:ae=1:lu=300:lo=IN:ei=6257193:lr=1: \

	HOSTID=ANY SN=968398 SIGN=E3D729D0929E TS_OK

INCREMENT MATLAB_Builder_for_dot_Net MLM 369 permanent uncounted \

	VENDOR_STRING=vi=0:at=200:ae=1:lu=300:lo=IN:ei=6257193:lr=1: \

	HOSTID=ANY SN=968398 SIGN=8E84260A9402 TS_OK

INCREMENT MATLAB_Builder_for_Java MLM 369 permanent uncounted \

	VENDOR_STRING=vi=0:at=200:ae=1:lu=300:lo=IN:ei=6257193:lr=1: \

	HOSTID=ANY SN=968398 SIGN=4B91BD1ADD80 TS_OK

INCREMENT MATLAB_Coder MLM 369 permanent uncounted \

	VENDOR_STRING=vi=0:at=200:ae=1:lu=300:lo=IN:ei=6257193:lr=1: \

	HOSTID=ANY SN=968398 SIGN=BF825F68BD62 TS_OK

INCREMENT MATLAB_Distrib_Comp_Engine MLM 369 permanent uncounted \

	VENDOR_STRING=vi=0:at=200:ae=1:lu=300:lo=IN:ei=6257193:lr=1: \

	HOSTID=ANY SN=968398 SIGN=73FB1C30B022 TS_OK

INCREMENT MATLAB_Excel_Builder MLM 369 permanent uncounted \

	VENDOR_STRING=vi=0:at=200:ae=1:lu=300:lo=IN:ei=6257193:lr=1: \

	HOSTID=ANY SN=968398 SIGN=03A16FD44AC0 TS_OK

INCREMENT MATLAB_Production_Server MLM 369 permanent uncounted \

	VENDOR_STRING=vi=0:at=200:ae=1:lu=300:lo=IN:ei=6257193:lr=1: \

	HOSTID=ANY SN=968398 SIGN=589050B05868 TS_OK

INCREMENT MATLAB_Report_Gen MLM 369 permanent uncounted \

	VENDOR_STRING=vi=0:at=200:ae=1:lu=300:lo=IN:ei=6257193:lr=1: \

	HOSTID=ANY SN=968398 SIGN=07D4A3BCE4E4 TS_OK

INCREMENT MBC_Toolbox MLM 369 permanent uncounted \

	VENDOR_STRING=vi=0:at=200:ae=1:lu=300:lo=IN:ei=6257193:lr=1: \

	HOSTID=ANY SN=968398 SIGN=E894A736918E TS_OK

INCREMENT MPC_Toolbox MLM 369 permanent uncounted \

	VENDOR_STRING=vi=0:at=200:ae=1:lu=300:lo=IN:ei=6257193:lr=1: \

	HOSTID=ANY SN=968398 SIGN=FFF734022FC8 TS_OK

INCREMENT Neural_Network_Toolbox MLM 369 permanent uncounted \

	VENDOR_STRING=vi=0:at=200:ae=1:lu=300:lo=IN:ei=6257193:lr=1: \

	HOSTID=ANY SN=968398 SIGN=442F9C9A894E TS_OK

INCREMENT OPC_Data_Access_Explorer MLM 369 permanent uncounted \

	VENDOR_STRING=vi=0:at=200:ae=1:lu=300:lo=IN:ei=6257193:lr=1: \

	HOSTID=ANY SN=968398 SIGN=F5731D84D732 TS_OK

INCREMENT OPC_Toolbox MLM 369 permanent uncounted \

	VENDOR_STRING=vi=0:at=200:ae=1:lu=300:lo=IN:ei=6257193:lr=1: \

	HOSTID=ANY SN=968398 SIGN=447FAF1A275A TS_OK

INCREMENT Optimization_Toolbox MLM 369 permanent uncounted \

	VENDOR_STRING=vi=0:at=200:ae=1:lu=300:lo=IN:ei=6257193:lr=1: \

	HOSTID=ANY SN=968398 SIGN=C6097A7C2F30 TS_OK

INCREMENT PDE_Toolbox MLM 369 permanent uncounted \

	VENDOR_STRING=vi=0:at=200:ae=1:lu=300:lo=IN:ei=6257193:lr=1: \

	HOSTID=ANY SN=968398 SIGN=F38F1B86FC82 TS_OK

INCREMENT Phased_Array_System_Toolbox MLM 369 permanent uncounted \

	VENDOR_STRING=vi=0:at=200:ae=1:lu=300:lo=IN:ei=6257193:lr=1: \

	HOSTID=ANY SN=968398 SIGN=70481D26033A TS_OK

INCREMENT PolySpace_Bug_Finder MLM 369 permanent uncounted \

	VENDOR_STRING=vi=0:at=200:ae=1:lu=300:lo=IN:ei=6257193:lr=1: \

	HOSTID=ANY SN=968398 SIGN=58A863F8AECC TS_OK

INCREMENT PolySpace_Bug_Finder_Engine MLM 369 permanent uncounted \

	VENDOR_STRING=vi=0:at=200:ae=1:lu=300:lo=IN:ei=6257193:lr=1: \

	HOSTID=ANY SN=968398 SIGN=96E1E2EA2112 TS_OK

INCREMENT PolySpace_Client_ADA MLM 369 permanent uncounted \

	VENDOR_STRING=vi=0:at=200:ae=1:lu=300:lo=IN:ei=6257193:lr=1: \

	HOSTID=ANY SN=968398 SIGN=A3C8672ED368 TS_OK

INCREMENT PolySpace_Code_Prover MLM 369 permanent uncounted \

	VENDOR_STRING=vi=0:at=200:ae=1:lu=300:lo=IN:ei=6257193:lr=1: \

	HOSTID=ANY SN=968398 SIGN=DDC6A7807CA6 TS_OK

INCREMENT PolySpace_Code_Prover_Engine MLM 369 permanent uncounted \

	VENDOR_STRING=vi=0:at=200:ae=1:lu=300:lo=IN:ei=6257193:lr=1: \

	HOSTID=ANY SN=968398 SIGN=039FE14A2750 TS_OK

INCREMENT PolySpace_Server_ADA MLM 369 permanent uncounted \

	VENDOR_STRING=vi=0:at=200:ae=1:lu=300:lo=IN:ei=6257193:lr=1: \

	HOSTID=ANY SN=968398 SIGN=CEFF5262D7A6 TS_OK

INCREMENT PolySpace_Server_C_CPP MLM 369 permanent uncounted \

	VENDOR_STRING=vi=0:at=200:ae=1:lu=300:lo=IN:ei=6257193:lr=1: \

	HOSTID=ANY SN=968398 SIGN=D706AB3A3B4A TS_OK

INCREMENT PolySpace_Server_C_CPP MLM 369 permanent uncounted \

	VENDOR_STRING=vi=0:at=200:ae=1:lu=300:lo=IN:ei=6257193:lr=1: \

	HOSTID=ANY SN=968398 SIGN=D706AB3A3B4A TS_OK

INCREMENT Power_System_Blocks MLM 369 permanent uncounted \

	VENDOR_STRING=vi=0:at=200:ae=1:lu=300:lo=IN:ei=6257193:lr=1: \

	HOSTID=ANY SN=968398 SIGN=5811DD6EC3C4 TS_OK

INCREMENT Powertrain_Blockset MLM 369 permanent uncounted \

	VENDOR_STRING=vi=0:at=200:ae=1:lu=300:lo=IN:ei=6257193:lr=1: \

	HOSTID=ANY SN=968398 SIGN=055FE1169600 TS_OK

INCREMENT Pred_Maintenance_Toolbox MLM 369 permanent uncounted \

	VENDOR_STRING=vi=0:at=200:ae=1:lu=300:lo=IN:ei=6257193:lr=1: \

	HOSTID=ANY SN=968398 SIGN=7B78C1FA14F8 TS_OK

INCREMENT Qual_Kit_DO MLM 369 permanent uncounted \

	VENDOR_STRING=vi=0:at=200:ae=1:lu=300:lo=IN:ei=6257193:lr=1: \

	HOSTID=ANY SN=968398 SIGN=AABBCFFCC244 TS_OK

INCREMENT Real-Time_Win_Target MLM 369 permanent uncounted \

	VENDOR_STRING=vi=0:at=200:ae=1:lu=300:lo=IN:ei=6257193:lr=1: \

	HOSTID=ANY SN=968398 SIGN=ED23164E5034 TS_OK

INCREMENT Real-Time_Workshop MLM 369 permanent uncounted \

	VENDOR_STRING=vi=0:at=200:ae=1:lu=300:lo=IN:ei=6257193:lr=1: \

	HOSTID=ANY SN=968398 SIGN=10134088DF18 TS_OK

INCREMENT RF_Blockset MLM 369 permanent uncounted \

	VENDOR_STRING=vi=0:at=200:ae=1:lu=300:lo=IN:ei=6257193:lr=1: \

	HOSTID=ANY SN=968398 SIGN=10EBAB54B378 TS_OK

INCREMENT RF_Toolbox MLM 369 permanent uncounted \

	VENDOR_STRING=vi=0:at=200:ae=1:lu=300:lo=IN:ei=6257193:lr=1: \

	HOSTID=ANY SN=968398 SIGN=51C81DAE9152 TS_OK

INCREMENT Risk_Management_Toolbox MLM 369 permanent uncounted \

	VENDOR_STRING=vi=0:at=200:ae=1:lu=300:lo=IN:ei=6257193:lr=1: \

	HOSTID=ANY SN=968398 SIGN=4E0C5A02015A TS_OK

INCREMENT Robotics_System_Toolbox MLM 369 permanent uncounted \

	VENDOR_STRING=vi=0:at=200:ae=1:lu=300:lo=IN:ei=6257193:lr=1: \

	HOSTID=ANY SN=968398 SIGN=C2B6D5602A3E TS_OK

INCREMENT Robust_Toolbox MLM 369 permanent uncounted \

	VENDOR_STRING=vi=0:at=200:ae=1:lu=300:lo=IN:ei=6257193:lr=1: \

	HOSTID=ANY SN=968398 SIGN=DF9325BC7A28 TS_OK

INCREMENT RTW_Embedded_Coder MLM 369 permanent uncounted \

	VENDOR_STRING=vi=0:at=200:ae=1:lu=300:lo=IN:ei=6257193:lr=1: \

	HOSTID=ANY SN=968398 SIGN=2CD84F6A6D06 TS_OK

INCREMENT Sensor_Array_Toolbox MLM 369 permanent uncounted \

	VENDOR_STRING=vi=0:at=200:ae=1:lu=300:lo=IN:ei=6257193:lr=1: \

	HOSTID=ANY SN=968398 SIGN=87B58F5885E6 TS_OK

INCREMENT Signal_Blocks MLM 369 permanent uncounted \

	VENDOR_STRING=vi=0:at=200:ae=1:lu=300:lo=IN:ei=6257193:lr=1: \

	HOSTID=ANY SN=968398 SIGN=76EE54D62094 TS_OK

INCREMENT Signal_Toolbox MLM 369 permanent uncounted \

	VENDOR_STRING=vi=0:at=200:ae=1:lu=300:lo=IN:ei=6257193:lr=1: \

	HOSTID=ANY SN=968398 SIGN=EFEAED44A1A2 TS_OK

INCREMENT SimBiology MLM 369 permanent uncounted \

	VENDOR_STRING=vi=0:at=200:ae=1:lu=300:lo=IN:ei=6257193:lr=1: \

	HOSTID=ANY SN=968398 SIGN=5EDB2ED64CD4 TS_OK

INCREMENT SimDriveline MLM 369 permanent uncounted \

	VENDOR_STRING=vi=0:at=200:ae=1:lu=300:lo=IN:ei=6257193:lr=1: \

	HOSTID=ANY SN=968398 SIGN=0EDCEC946F44 TS_OK

INCREMENT SimElectronics MLM 369 permanent uncounted \

	VENDOR_STRING=vi=0:at=200:ae=1:lu=300:lo=IN:ei=6257193:lr=1: \

	HOSTID=ANY SN=968398 SIGN=9EA692CAB216 TS_OK

INCREMENT SimEvents MLM 369 permanent uncounted \

	VENDOR_STRING=vi=0:at=200:ae=1:lu=300:lo=IN:ei=6257193:lr=1: \

	HOSTID=ANY SN=968398 SIGN=3941FB06D5B2 TS_OK

INCREMENT SimHydraulics MLM 369 permanent uncounted \

	VENDOR_STRING=vi=0:at=200:ae=1:lu=300:lo=IN:ei=6257193:lr=1: \

	HOSTID=ANY SN=968398 SIGN=590243A0E584 TS_OK

INCREMENT SimMechanics MLM 369 permanent uncounted \

	VENDOR_STRING=vi=0:at=200:ae=1:lu=300:lo=IN:ei=6257193:lr=1: \

	HOSTID=ANY SN=968398 SIGN=A7F43486F422 TS_OK

INCREMENT Simscape MLM 369 permanent uncounted \

	VENDOR_STRING=vi=0:at=200:ae=1:lu=300:lo=IN:ei=6257193:lr=1: \

	HOSTID=ANY SN=968398 SIGN=013B45668C66 TS_OK

INCREMENT SIMULINK MLM 369 permanent uncounted \

	VENDOR_STRING=vi=0:at=200:ae=1:lu=300:lo=IN:ei=6257193:lr=1: \

	HOSTID=ANY SN=968398 SIGN=E837A9006D3E TS_OK

INCREMENT Simulink_Code_Inspector MLM 369 permanent uncounted \

	VENDOR_STRING=vi=0:at=200:ae=1:lu=300:lo=IN:ei=6257193:lr=1: \

	HOSTID=ANY SN=968398 SIGN=29154C324D06 TS_OK

INCREMENT Simulink_Control_Design MLM 369 permanent uncounted \

	VENDOR_STRING=vi=0:at=200:ae=1:lu=300:lo=IN:ei=6257193:lr=1: \

	HOSTID=ANY SN=968398 SIGN=79FA200447C4 TS_OK

INCREMENT simulink_coverage MLM 369 permanent uncounted \

	VENDOR_STRING=vi=0:at=200:ae=1:lu=300:lo=IN:ei=6257193:lr=1: \

	HOSTID=ANY SN=968398 SIGN=2CD191585516 TS_OK

INCREMENT Simulink_Design_Optim MLM 369 permanent uncounted \

	VENDOR_STRING=vi=0:at=200:ae=1:lu=300:lo=IN:ei=6257193:lr=1: \

	HOSTID=ANY SN=968398 SIGN=25259A54C4C4 TS_OK

INCREMENT Simulink_Design_Verifier MLM 369 permanent uncounted \

	VENDOR_STRING=vi=0:at=200:ae=1:lu=300:lo=IN:ei=6257193:lr=1: \

	HOSTID=ANY SN=968398 SIGN=82BFAC1CEA46 TS_OK

INCREMENT Simulink_HDL_Coder MLM 369 permanent uncounted \

	VENDOR_STRING=vi=0:at=200:ae=1:lu=300:lo=IN:ei=6257193:lr=1: \

	HOSTID=ANY SN=968398 SIGN=D5963DCACF42 TS_OK

INCREMENT Simulink_PLC_Coder MLM 369 permanent uncounted \

	VENDOR_STRING=vi=0:at=200:ae=1:lu=300:lo=IN:ei=6257193:lr=1: \

	HOSTID=ANY SN=968398 SIGN=CCFBF574CE16 TS_OK

INCREMENT SIMULINK_Report_Gen MLM 369 permanent uncounted \

	VENDOR_STRING=vi=0:at=200:ae=1:lu=300:lo=IN:ei=6257193:lr=1: \

	HOSTID=ANY SN=968398 SIGN=9813820C19D4 TS_OK

INCREMENT Simulink_Requirements MLM 369 permanent uncounted \

	VENDOR_STRING=vi=0:at=200:ae=1:lu=300:lo=IN:ei=6257193:lr=1: \

	HOSTID=ANY SN=968398 SIGN=AE15C81AA9EC TS_OK

INCREMENT Simulink_Test MLM 369 permanent uncounted \

	VENDOR_STRING=vi=0:at=200:ae=1:lu=300:lo=IN:ei=6257193:lr=1: \

	HOSTID=ANY SN=968398 SIGN=0B94EC30C1E6 TS_OK

INCREMENT sl_coverage MLM 369 permanent uncounted \

	VENDOR_STRING=vi=0:at=200:ae=1:lu=300:lo=IN:ei=6257193:lr=1: \

	HOSTID=ANY SN=968398 SIGN=B7FE4748A9F2 TS_OK

INCREMENT sl_verification_validation MLM 369 permanent uncounted \

	VENDOR_STRING=vi=0:at=200:ae=1:lu=300:lo=IN:ei=6257193:lr=1: \

	HOSTID=ANY SN=968398 SIGN=D924FEA8C050 TS_OK

INCREMENT Stateflow MLM 369 permanent uncounted \

	VENDOR_STRING=vi=0:at=200:ae=1:lu=300:lo=IN:ei=6257193:lr=1: \

	HOSTID=ANY SN=968398 SIGN=C62F7A988096 TS_OK

INCREMENT Stateflow_Coder MLM 369 permanent uncounted \

	VENDOR_STRING=vi=0:at=200:ae=1:lu=300:lo=IN:ei=6257193:lr=1: \

	HOSTID=ANY SN=968398 SIGN=E86A8B1A92BE TS_OK

INCREMENT Statistics_Toolbox MLM 369 permanent uncounted \

	VENDOR_STRING=vi=0:at=200:ae=1:lu=300:lo=IN:ei=6257193:lr=1: \

	HOSTID=ANY SN=968398 SIGN=666DA9489C32 TS_OK

INCREMENT Symbolic_Toolbox MLM 369 permanent uncounted \

	VENDOR_STRING=vi=0:at=200:ae=1:lu=300:lo=IN:ei=6257193:lr=1: \

	HOSTID=ANY SN=968398 SIGN=21FD3CF6B092 TS_OK

INCREMENT SystemTest MLM 369 permanent uncounted \

	VENDOR_STRING=vi=0:at=200:ae=1:lu=300:lo=IN:ei=6257193:lr=1: \

	HOSTID=ANY SN=968398 SIGN=A52ECE3EB50C TS_OK

INCREMENT Target_Support_Package MLM 369 permanent uncounted \

	VENDOR_STRING=vi=0:at=200:ae=1:lu=300:lo=IN:ei=6257193:lr=1: \

	HOSTID=ANY SN=968398 SIGN=183AD8C25500 TS_OK

INCREMENT Text_Analytics_Toolbox MLM 369 permanent uncounted \

	VENDOR_STRING=vi=0:at=200:ae=1:lu=300:lo=IN:ei=6257193:lr=1: \

	HOSTID=ANY SN=968398 SIGN=C93274BE2C50 TS_OK

INCREMENT TRADING_TOOLBOX MLM 369 permanent uncounted \

	VENDOR_STRING=vi=0:at=200:ae=1:lu=300:lo=IN:ei=6257193:lr=1: \

	HOSTID=ANY SN=968398 SIGN=4033F00CA592 TS_OK

INCREMENT Vehicle_Dynamics_Blockset MLM 369 permanent uncounted \

	VENDOR_STRING=vi=0:at=200:ae=1:lu=300:lo=IN:ei=6257193:lr=1: \

	HOSTID=ANY SN=968398 SIGN=53545E2475D6 TS_OK

INCREMENT Vehicle_Network_Toolbox MLM 369 permanent uncounted \

	VENDOR_STRING=vi=0:at=200:ae=1:lu=300:lo=IN:ei=6257193:lr=1: \

	HOSTID=ANY SN=968398 SIGN=06FD33A6500C TS_OK

INCREMENT Video_and_Image_Blockset MLM 369 permanent uncounted \

	VENDOR_STRING=vi=0:at=200:ae=1:lu=300:lo=IN:ei=6257193:lr=1: \

	HOSTID=ANY SN=968398 SIGN=AFC4F95EF97C TS_OK

INCREMENT Virtual_Reality_Toolbox MLM 369 permanent uncounted \

	VENDOR_STRING=vi=0:at=200:ae=1:lu=300:lo=IN:ei=6257193:lr=1: \

	HOSTID=ANY SN=968398 SIGN=E18982E05F76 TS_OK

INCREMENT Vision_HDL_Toolbox MLM 369 permanent uncounted \

	VENDOR_STRING=vi=0:at=200:ae=1:lu=300:lo=IN:ei=6257193:lr=1: \

	HOSTID=ANY SN=968398 SIGN=B7CBEE12E6DE TS_OK

INCREMENT Wavelet_Toolbox MLM 369 permanent uncounted \

	VENDOR_STRING=vi=0:at=200:ae=1:lu=300:lo=IN:ei=6257193:lr=1: \

	HOSTID=ANY SN=968398 SIGN=5620DE4E8E1A TS_OK

INCREMENT WLAN_System_Toolbox MLM 369 permanent uncounted \

	VENDOR_STRING=vi=0:at=200:ae=1:lu=300:lo=IN:ei=6257193:lr=1: \

	HOSTID=ANY SN=968398 SIGN=0617D9360522 TS_OK

INCREMENT XPC_Embedded_Option MLM 369 permanent uncounted \

	VENDOR_STRING=vi=0:at=200:ae=1:lu=300:lo=IN:ei=6257193:lr=1: \

	HOSTID=ANY SN=968398 SIGN=3D79201A5002 TS_OK

INCREMENT XPC_Target MLM 369 permanent uncounted \

	VENDOR_STRING=vi=0:at=200:ae=1:lu=300:lo=IN:ei=6257193:lr=1: \

	HOSTID=ANY SN=968398 SIGN=316E1E6C5434 TS_OK

 TS_OK

```



## MATLAB 2019a



文件夹在“C:\Program Files\Polyspace\R2019a\licenses”



```

INCREMENT Aerospace_Blockset MLM 369 permanent uncounted \

	VENDOR_STRING=vi=0:at=200:ae=1:lu=300:lo=IN:ei=6257193:lr=1: \

	HOSTID=ANY SN=123456 SIGN=0D8A1582514C TS_OK

INCREMENT Aerospace_Toolbox MLM 369 permanent uncounted \

	VENDOR_STRING=vi=0:at=200:ae=1:lu=300:lo=IN:ei=6257193:lr=1: \

	HOSTID=ANY SN=123456 SIGN=13FDDFF8C36C TS_OK

INCREMENT Antenna_Toolbox MLM 369 permanent uncounted \

	VENDOR_STRING=vi=0:at=200:ae=1:lu=300:lo=IN:ei=6257193:lr=1: \

	HOSTID=ANY SN=123456 SIGN=2A01DAAA9886 TS_OK

INCREMENT Audio_System_Toolbox MLM 369 permanent uncounted \

	VENDOR_STRING=vi=0:at=200:ae=1:lu=300:lo=IN:ei=6257193:lr=1: \

	HOSTID=ANY SN=123456 SIGN=E025BF62EAD8 TS_OK

INCREMENT Automated_Driving_Toolbox MLM 369 permanent uncounted \

	VENDOR_STRING=vi=0:at=200:ae=1:lu=300:lo=IN:ei=6257193:lr=1: \

	HOSTID=ANY SN=123456 SIGN=C318246C14E2 TS_OK

INCREMENT Bioinformatics_Toolbox MLM 369 permanent uncounted \

	VENDOR_STRING=vi=0:at=200:ae=1:lu=300:lo=IN:ei=6257193:lr=1: \

	HOSTID=ANY SN=123456 SIGN=358194AE1548 TS_OK

INCREMENT Cert_Kit_IEC MLM 369 permanent uncounted \

	VENDOR_STRING=vi=0:at=200:ae=1:lu=300:lo=IN:ei=6257193:lr=1: \

	HOSTID=ANY SN=123456 SIGN=60C2E6F826CE TS_OK

INCREMENT Communication_Blocks MLM 369 permanent uncounted \

	VENDOR_STRING=vi=0:at=200:ae=1:lu=300:lo=IN:ei=6257193:lr=1: \

	HOSTID=ANY SN=123456 SIGN=CF5D32DAABBA TS_OK

INCREMENT Communication_Toolbox MLM 369 permanent uncounted \

	VENDOR_STRING=vi=0:at=200:ae=1:lu=300:lo=IN:ei=6257193:lr=1: \

	HOSTID=ANY SN=123456 SIGN=253B4EECBE48 TS_OK

INCREMENT Compiler MLM 369 permanent uncounted \

	VENDOR_STRING=vi=0:at=200:ae=1:lu=300:lo=IN:ei=6257193:lr=1: \

	HOSTID=ANY SN=123456 SIGN=2DD1C464FD06 TS_OK

INCREMENT Control_Toolbox MLM 369 permanent uncounted \

	VENDOR_STRING=vi=0:at=200:ae=1:lu=300:lo=IN:ei=6257193:lr=1: \

	HOSTID=ANY SN=123456 SIGN=E0D5C4184FB6 TS_OK

INCREMENT Curve_Fitting_Toolbox MLM 369 permanent uncounted \

	VENDOR_STRING=vi=0:at=200:ae=1:lu=300:lo=IN:ei=6257193:lr=1: \

	HOSTID=ANY SN=123456 SIGN=583BAC2E0F7A TS_OK

INCREMENT Data_Acq_Toolbox MLM 369 permanent uncounted \

	VENDOR_STRING=vi=0:at=200:ae=1:lu=300:lo=IN:ei=6257193:lr=1: \

	HOSTID=ANY SN=123456 SIGN=48ECF5F6B11E TS_OK

INCREMENT Database_Toolbox MLM 369 permanent uncounted \

	VENDOR_STRING=vi=0:at=200:ae=1:lu=300:lo=IN:ei=6257193:lr=1: \

	HOSTID=ANY SN=123456 SIGN=E9929C7A187A TS_OK

INCREMENT DATAFEED_TOOLBOX MLM 369 permanent uncounted \

	VENDOR_STRING=vi=0:at=200:ae=1:lu=300:lo=IN:ei=6257193:lr=1: \

	HOSTID=ANY SN=123456 SIGN=9876C540CA8E TS_OK

INCREMENT Dial_and_Gauge_Blocks MLM 369 permanent uncounted \

	VENDOR_STRING=vi=0:at=200:ae=1:lu=300:lo=IN:ei=6257193:lr=1: \

	HOSTID=ANY SN=123456 SIGN=EFBA589A1810 TS_OK

INCREMENT Distrib_Computing_Toolbox MLM 369 permanent uncounted \

	VENDOR_STRING=vi=0:at=200:ae=1:lu=300:lo=IN:ei=6257193:lr=1: \

	HOSTID=ANY SN=123456 SIGN=D995C292E03A TS_OK

INCREMENT Econometrics_Toolbox MLM 369 permanent uncounted \

	VENDOR_STRING=vi=0:at=200:ae=1:lu=300:lo=IN:ei=6257193:lr=1: \

	HOSTID=ANY SN=123456 SIGN=D1EC25D000D8 TS_OK

INCREMENT eda_simulator_link MLM 369 permanent uncounted \

	VENDOR_STRING=vi=0:at=200:ae=1:lu=300:lo=IN:ei=6257193:lr=1: \

	HOSTID=ANY SN=123456 SIGN=DE5E67B09746 TS_OK

INCREMENT Embedded_IDE_Link MLM 369 permanent uncounted \

	VENDOR_STRING=vi=0:at=200:ae=1:lu=300:lo=IN:ei=6257193:lr=1: \

	HOSTID=ANY SN=123456 SIGN=FB290E548926 TS_OK

INCREMENT Excel_Link MLM 369 permanent uncounted \

	VENDOR_STRING=vi=0:at=200:ae=1:lu=300:lo=IN:ei=6257193:lr=1: \

	HOSTID=ANY SN=123456 SIGN=E6527A880B26 TS_OK

INCREMENT Filter_Design_HDL_Coder MLM 369 permanent uncounted \

	VENDOR_STRING=vi=0:at=200:ae=1:lu=300:lo=IN:ei=6257193:lr=1: \

	HOSTID=ANY SN=123456 SIGN=44F6103EBB0E TS_OK

INCREMENT Filter_Design_Toolbox MLM 369 permanent uncounted \

	VENDOR_STRING=vi=0:at=200:ae=1:lu=300:lo=IN:ei=6257193:lr=1: \

	HOSTID=ANY SN=123456 SIGN=58CB0596F32E TS_OK

INCREMENT Fin_Derivatives_Toolbox MLM 369 permanent uncounted \

	VENDOR_STRING=vi=0:at=200:ae=1:lu=300:lo=IN:ei=6257193:lr=1: \

	HOSTID=ANY SN=123456 SIGN=9E9A2B0020BA TS_OK

INCREMENT Fin_Instruments_Toolbox MLM 369 permanent uncounted \

	VENDOR_STRING=vi=0:at=200:ae=1:lu=300:lo=IN:ei=6257193:lr=1: \

	HOSTID=ANY SN=123456 SIGN=325A84A84E4A TS_OK

INCREMENT Financial_Toolbox MLM 369 permanent uncounted \

	VENDOR_STRING=vi=0:at=200:ae=1:lu=300:lo=IN:ei=6257193:lr=1: \

	HOSTID=ANY SN=123456 SIGN=698F9FC2DDDE TS_OK

INCREMENT Fixed_Income_Toolbox MLM 369 permanent uncounted \

	VENDOR_STRING=vi=0:at=200:ae=1:lu=300:lo=IN:ei=6257193:lr=1: \

	HOSTID=ANY SN=123456 SIGN=75BBDA60AC74 TS_OK

INCREMENT Fixed_Point_Toolbox MLM 369 permanent uncounted \

	VENDOR_STRING=vi=0:at=200:ae=1:lu=300:lo=IN:ei=6257193:lr=1: \

	HOSTID=ANY SN=123456 SIGN=BF695EBE4514 TS_OK

INCREMENT Fixed-Point_Blocks MLM 369 permanent uncounted \

	VENDOR_STRING=vi=0:at=200:ae=1:lu=300:lo=IN:ei=6257193:lr=1: \

	HOSTID=ANY SN=123456 SIGN=22A5B32025E6 TS_OK

INCREMENT Fuzzy_Toolbox MLM 369 permanent uncounted \

	VENDOR_STRING=vi=0:at=200:ae=1:lu=300:lo=IN:ei=6257193:lr=1: \

	HOSTID=ANY SN=123456 SIGN=90FDC43A584E TS_OK

INCREMENT GADS_Toolbox MLM 369 permanent uncounted \

	VENDOR_STRING=vi=0:at=200:ae=1:lu=300:lo=IN:ei=6257193:lr=1: \

	HOSTID=ANY SN=123456 SIGN=38C864060ECE TS_OK

INCREMENT GPU_Coder MLM 369 permanent uncounted \

	VENDOR_STRING=vi=0:at=200:ae=1:lu=300:lo=IN:ei=6257193:lr=1: \

	HOSTID=ANY SN=123456 SIGN=D24A7C12C544 TS_OK

INCREMENT Identification_Toolbox MLM 369 permanent uncounted \

	VENDOR_STRING=vi=0:at=200:ae=1:lu=300:lo=IN:ei=6257193:lr=1: \

	HOSTID=ANY SN=123456 SIGN=2620D11C4600 TS_OK

INCREMENT Image_Acquisition_Toolbox MLM 369 permanent uncounted \

	VENDOR_STRING=vi=0:at=200:ae=1:lu=300:lo=IN:ei=6257193:lr=1: \

	HOSTID=ANY SN=123456 SIGN=43B59340F0FC TS_OK

INCREMENT Image_Toolbox MLM 369 permanent uncounted \

	VENDOR_STRING=vi=0:at=200:ae=1:lu=300:lo=IN:ei=6257193:lr=1: \

	HOSTID=ANY SN=123456 SIGN=23C1BC2A0B00 TS_OK

INCREMENT Instr_Control_Toolbox MLM 369 permanent uncounted \

	VENDOR_STRING=vi=0:at=200:ae=1:lu=300:lo=IN:ei=6257193:lr=1: \

	HOSTID=ANY SN=123456 SIGN=C33239E4EABA TS_OK

INCREMENT LTE_HDL_Toolbox MLM 369 permanent uncounted \

	VENDOR_STRING=vi=0:at=200:ae=1:lu=300:lo=IN:ei=6257193:lr=1: \

	HOSTID=ANY SN=123456 SIGN=CBEB4DC65DDE TS_OK

INCREMENT LTE_Toolbox MLM 369 permanent uncounted \

	VENDOR_STRING=vi=0:at=200:ae=1:lu=300:lo=IN:ei=6257193:lr=1: \

	HOSTID=ANY SN=123456 SIGN=DF335124FDAE TS_OK

INCREMENT MAP_Toolbox MLM 369 permanent uncounted \

	VENDOR_STRING=vi=0:at=200:ae=1:lu=300:lo=IN:ei=6257193:lr=1: \

	HOSTID=ANY SN=123456 SIGN=E927B964E6F2 TS_OK

INCREMENT MATLAB MLM 369 permanent uncounted \

	VENDOR_STRING=vi=0:at=200:ae=1:lu=300:lo=IN:ei=6257193:lr=1: \

	HOSTID=ANY SN=123456 SIGN=E3D729D0929E TS_OK

INCREMENT MATLAB_Builder_for_dot_Net MLM 369 permanent uncounted \

	VENDOR_STRING=vi=0:at=200:ae=1:lu=300:lo=IN:ei=6257193:lr=1: \

	HOSTID=ANY SN=123456 SIGN=8E84260A9402 TS_OK

INCREMENT MATLAB_Builder_for_Java MLM 369 permanent uncounted \

	VENDOR_STRING=vi=0:at=200:ae=1:lu=300:lo=IN:ei=6257193:lr=1: \

	HOSTID=ANY SN=123456 SIGN=4B91BD1ADD80 TS_OK

INCREMENT MATLAB_Coder MLM 369 permanent uncounted \

	VENDOR_STRING=vi=0:at=200:ae=1:lu=300:lo=IN:ei=6257193:lr=1: \

	HOSTID=ANY SN=123456 SIGN=BF825F68BD62 TS_OK

INCREMENT MATLAB_Distrib_Comp_Engine MLM 369 permanent uncounted \

	VENDOR_STRING=vi=0:at=200:ae=1:lu=300:lo=IN:ei=6257193:lr=1: \

	HOSTID=ANY SN=123456 SIGN=73FB1C30B022 TS_OK

INCREMENT MATLAB_Excel_Builder MLM 369 permanent uncounted \

	VENDOR_STRING=vi=0:at=200:ae=1:lu=300:lo=IN:ei=6257193:lr=1: \

	HOSTID=ANY SN=123456 SIGN=03A16FD44AC0 TS_OK

INCREMENT MATLAB_Production_Server MLM 369 permanent uncounted \

	VENDOR_STRING=vi=0:at=200:ae=1:lu=300:lo=IN:ei=6257193:lr=1: \

	HOSTID=ANY SN=123456 SIGN=589050B05868 TS_OK

INCREMENT MATLAB_Report_Gen MLM 369 permanent uncounted \

	VENDOR_STRING=vi=0:at=200:ae=1:lu=300:lo=IN:ei=6257193:lr=1: \

	HOSTID=ANY SN=123456 SIGN=07D4A3BCE4E4 TS_OK

INCREMENT MBC_Toolbox MLM 369 permanent uncounted \

	VENDOR_STRING=vi=0:at=200:ae=1:lu=300:lo=IN:ei=6257193:lr=1: \

	HOSTID=ANY SN=123456 SIGN=E894A736918E TS_OK

INCREMENT MPC_Toolbox MLM 369 permanent uncounted \

	VENDOR_STRING=vi=0:at=200:ae=1:lu=300:lo=IN:ei=6257193:lr=1: \

	HOSTID=ANY SN=123456 SIGN=FFF734022FC8 TS_OK

INCREMENT Neural_Network_Toolbox MLM 369 permanent uncounted \

	VENDOR_STRING=vi=0:at=200:ae=1:lu=300:lo=IN:ei=6257193:lr=1: \

	HOSTID=ANY SN=123456 SIGN=442F9C9A894E TS_OK

INCREMENT OPC_Data_Access_Explorer MLM 369 permanent uncounted \

	VENDOR_STRING=vi=0:at=200:ae=1:lu=300:lo=IN:ei=6257193:lr=1: \

	HOSTID=ANY SN=123456 SIGN=F5731D84D732 TS_OK

INCREMENT OPC_Toolbox MLM 369 permanent uncounted \

	VENDOR_STRING=vi=0:at=200:ae=1:lu=300:lo=IN:ei=6257193:lr=1: \

	HOSTID=ANY SN=123456 SIGN=447FAF1A275A TS_OK

INCREMENT Optimization_Toolbox MLM 369 permanent uncounted \

	VENDOR_STRING=vi=0:at=200:ae=1:lu=300:lo=IN:ei=6257193:lr=1: \

	HOSTID=ANY SN=123456 SIGN=C6097A7C2F30 TS_OK

INCREMENT PDE_Toolbox MLM 369 permanent uncounted \

	VENDOR_STRING=vi=0:at=200:ae=1:lu=300:lo=IN:ei=6257193:lr=1: \

	HOSTID=ANY SN=123456 SIGN=F38F1B86FC82 TS_OK

INCREMENT Phased_Array_System_Toolbox MLM 369 permanent uncounted \

	VENDOR_STRING=vi=0:at=200:ae=1:lu=300:lo=IN:ei=6257193:lr=1: \

	HOSTID=ANY SN=123456 SIGN=70481D26033A TS_OK

INCREMENT PolySpace_Bug_Finder MLM 369 permanent uncounted \

	VENDOR_STRING=vi=0:at=200:ae=1:lu=300:lo=IN:ei=6257193:lr=1: \

	HOSTID=ANY SN=123456 SIGN=58A863F8AECC TS_OK

INCREMENT PolySpace_Bug_Finder_Engine MLM 369 permanent uncounted \

	VENDOR_STRING=vi=0:at=200:ae=1:lu=300:lo=IN:ei=6257193:lr=1: \

	HOSTID=ANY SN=123456 SIGN=96E1E2EA2112 TS_OK

INCREMENT PolySpace_Client_ADA MLM 369 permanent uncounted \

	VENDOR_STRING=vi=0:at=200:ae=1:lu=300:lo=IN:ei=6257193:lr=1: \

	HOSTID=ANY SN=123456 SIGN=A3C8672ED368 TS_OK

INCREMENT PolySpace_Code_Prover MLM 369 permanent uncounted \

	VENDOR_STRING=vi=0:at=200:ae=1:lu=300:lo=IN:ei=6257193:lr=1: \

	HOSTID=ANY SN=123456 SIGN=DDC6A7807CA6 TS_OK

INCREMENT PolySpace_Code_Prover_Engine MLM 369 permanent uncounted \

	VENDOR_STRING=vi=0:at=200:ae=1:lu=300:lo=IN:ei=6257193:lr=1: \

	HOSTID=ANY SN=123456 SIGN=039FE14A2750 TS_OK

INCREMENT PolySpace_Server_ADA MLM 369 permanent uncounted \

	VENDOR_STRING=vi=0:at=200:ae=1:lu=300:lo=IN:ei=6257193:lr=1: \

	HOSTID=ANY SN=123456 SIGN=CEFF5262D7A6 TS_OK

INCREMENT PolySpace_Server_C_CPP MLM 369 permanent uncounted \

	VENDOR_STRING=vi=0:at=200:ae=1:lu=300:lo=IN:ei=6257193:lr=1: \

	HOSTID=ANY SN=123456 SIGN=D706AB3A3B4A TS_OK

INCREMENT PolySpace_Server_C_CPP MLM 369 permanent uncounted \

	VENDOR_STRING=vi=0:at=200:ae=1:lu=300:lo=IN:ei=6257193:lr=1: \

	HOSTID=ANY SN=123456 SIGN=D706AB3A3B4A TS_OK

INCREMENT Power_System_Blocks MLM 369 permanent uncounted \

	VENDOR_STRING=vi=0:at=200:ae=1:lu=300:lo=IN:ei=6257193:lr=1: \

	HOSTID=ANY SN=123456 SIGN=5811DD6EC3C4 TS_OK

INCREMENT Powertrain_Blockset MLM 369 permanent uncounted \

	VENDOR_STRING=vi=0:at=200:ae=1:lu=300:lo=IN:ei=6257193:lr=1: \

	HOSTID=ANY SN=123456 SIGN=055FE1169600 TS_OK

INCREMENT Pred_Maintenance_Toolbox MLM 369 permanent uncounted \

	VENDOR_STRING=vi=0:at=200:ae=1:lu=300:lo=IN:ei=6257193:lr=1: \

	HOSTID=ANY SN=123456 SIGN=7B78C1FA14F8 TS_OK

INCREMENT Qual_Kit_DO MLM 369 permanent uncounted \

	VENDOR_STRING=vi=0:at=200:ae=1:lu=300:lo=IN:ei=6257193:lr=1: \

	HOSTID=ANY SN=123456 SIGN=AABBCFFCC244 TS_OK

INCREMENT Real-Time_Win_Target MLM 369 permanent uncounted \

	VENDOR_STRING=vi=0:at=200:ae=1:lu=300:lo=IN:ei=6257193:lr=1: \

	HOSTID=ANY SN=123456 SIGN=ED23164E5034 TS_OK

INCREMENT Real-Time_Workshop MLM 369 permanent uncounted \

	VENDOR_STRING=vi=0:at=200:ae=1:lu=300:lo=IN:ei=6257193:lr=1: \

	HOSTID=ANY SN=123456 SIGN=10134088DF18 TS_OK

INCREMENT RF_Blockset MLM 369 permanent uncounted \

	VENDOR_STRING=vi=0:at=200:ae=1:lu=300:lo=IN:ei=6257193:lr=1: \

	HOSTID=ANY SN=123456 SIGN=10EBAB54B378 TS_OK

INCREMENT RF_Toolbox MLM 369 permanent uncounted \

	VENDOR_STRING=vi=0:at=200:ae=1:lu=300:lo=IN:ei=6257193:lr=1: \

	HOSTID=ANY SN=123456 SIGN=51C81DAE9152 TS_OK

INCREMENT Risk_Management_Toolbox MLM 369 permanent uncounted \

	VENDOR_STRING=vi=0:at=200:ae=1:lu=300:lo=IN:ei=6257193:lr=1: \

	HOSTID=ANY SN=123456 SIGN=4E0C5A02015A TS_OK

INCREMENT Robotics_System_Toolbox MLM 369 permanent uncounted \

	VENDOR_STRING=vi=0:at=200:ae=1:lu=300:lo=IN:ei=6257193:lr=1: \

	HOSTID=ANY SN=123456 SIGN=C2B6D5602A3E TS_OK

INCREMENT Robust_Toolbox MLM 369 permanent uncounted \

	VENDOR_STRING=vi=0:at=200:ae=1:lu=300:lo=IN:ei=6257193:lr=1: \

	HOSTID=ANY SN=123456 SIGN=DF9325BC7A28 TS_OK

INCREMENT RTW_Embedded_Coder MLM 369 permanent uncounted \

	VENDOR_STRING=vi=0:at=200:ae=1:lu=300:lo=IN:ei=6257193:lr=1: \

	HOSTID=ANY SN=123456 SIGN=2CD84F6A6D06 TS_OK

INCREMENT Sensor_Array_Toolbox MLM 369 permanent uncounted \

	VENDOR_STRING=vi=0:at=200:ae=1:lu=300:lo=IN:ei=6257193:lr=1: \

	HOSTID=ANY SN=123456 SIGN=87B58F5885E6 TS_OK

INCREMENT Signal_Blocks MLM 369 permanent uncounted \

	VENDOR_STRING=vi=0:at=200:ae=1:lu=300:lo=IN:ei=6257193:lr=1: \

	HOSTID=ANY SN=123456 SIGN=76EE54D62094 TS_OK

INCREMENT Signal_Toolbox MLM 369 permanent uncounted \

	VENDOR_STRING=vi=0:at=200:ae=1:lu=300:lo=IN:ei=6257193:lr=1: \

	HOSTID=ANY SN=123456 SIGN=EFEAED44A1A2 TS_OK

INCREMENT SimBiology MLM 369 permanent uncounted \

	VENDOR_STRING=vi=0:at=200:ae=1:lu=300:lo=IN:ei=6257193:lr=1: \

	HOSTID=ANY SN=123456 SIGN=5EDB2ED64CD4 TS_OK

INCREMENT SimDriveline MLM 369 permanent uncounted \

	VENDOR_STRING=vi=0:at=200:ae=1:lu=300:lo=IN:ei=6257193:lr=1: \

	HOSTID=ANY SN=123456 SIGN=0EDCEC946F44 TS_OK

INCREMENT SimElectronics MLM 369 permanent uncounted \

	VENDOR_STRING=vi=0:at=200:ae=1:lu=300:lo=IN:ei=6257193:lr=1: \

	HOSTID=ANY SN=123456 SIGN=9EA692CAB216 TS_OK

INCREMENT SimEvents MLM 369 permanent uncounted \

	VENDOR_STRING=vi=0:at=200:ae=1:lu=300:lo=IN:ei=6257193:lr=1: \

	HOSTID=ANY SN=123456 SIGN=3941FB06D5B2 TS_OK

INCREMENT SimHydraulics MLM 369 permanent uncounted \

	VENDOR_STRING=vi=0:at=200:ae=1:lu=300:lo=IN:ei=6257193:lr=1: \

	HOSTID=ANY SN=123456 SIGN=590243A0E584 TS_OK

INCREMENT SimMechanics MLM 369 permanent uncounted \

	VENDOR_STRING=vi=0:at=200:ae=1:lu=300:lo=IN:ei=6257193:lr=1: \

	HOSTID=ANY SN=123456 SIGN=A7F43486F422 TS_OK

INCREMENT Simscape MLM 369 permanent uncounted \

	VENDOR_STRING=vi=0:at=200:ae=1:lu=300:lo=IN:ei=6257193:lr=1: \

	HOSTID=ANY SN=123456 SIGN=013B45668C66 TS_OK

INCREMENT SIMULINK MLM 369 permanent uncounted \

	VENDOR_STRING=vi=0:at=200:ae=1:lu=300:lo=IN:ei=6257193:lr=1: \

	HOSTID=ANY SN=123456 SIGN=E837A9006D3E TS_OK

INCREMENT Simulink_Code_Inspector MLM 369 permanent uncounted \

	VENDOR_STRING=vi=0:at=200:ae=1:lu=300:lo=IN:ei=6257193:lr=1: \

	HOSTID=ANY SN=123456 SIGN=29154C324D06 TS_OK

INCREMENT Simulink_Control_Design MLM 369 permanent uncounted \

	VENDOR_STRING=vi=0:at=200:ae=1:lu=300:lo=IN:ei=6257193:lr=1: \

	HOSTID=ANY SN=123456 SIGN=79FA200447C4 TS_OK

INCREMENT simulink_coverage MLM 369 permanent uncounted \

	VENDOR_STRING=vi=0:at=200:ae=1:lu=300:lo=IN:ei=6257193:lr=1: \

	HOSTID=ANY SN=123456 SIGN=2CD191585516 TS_OK

INCREMENT Simulink_Design_Optim MLM 369 permanent uncounted \

	VENDOR_STRING=vi=0:at=200:ae=1:lu=300:lo=IN:ei=6257193:lr=1: \

	HOSTID=ANY SN=123456 SIGN=25259A54C4C4 TS_OK

INCREMENT Simulink_Design_Verifier MLM 369 permanent uncounted \

	VENDOR_STRING=vi=0:at=200:ae=1:lu=300:lo=IN:ei=6257193:lr=1: \

	HOSTID=ANY SN=123456 SIGN=82BFAC1CEA46 TS_OK

INCREMENT Simulink_HDL_Coder MLM 369 permanent uncounted \

	VENDOR_STRING=vi=0:at=200:ae=1:lu=300:lo=IN:ei=6257193:lr=1: \

	HOSTID=ANY SN=123456 SIGN=D5963DCACF42 TS_OK

INCREMENT Simulink_PLC_Coder MLM 369 permanent uncounted \

	VENDOR_STRING=vi=0:at=200:ae=1:lu=300:lo=IN:ei=6257193:lr=1: \

	HOSTID=ANY SN=123456 SIGN=CCFBF574CE16 TS_OK

INCREMENT SIMULINK_Report_Gen MLM 369 permanent uncounted \

	VENDOR_STRING=vi=0:at=200:ae=1:lu=300:lo=IN:ei=6257193:lr=1: \

	HOSTID=ANY SN=123456 SIGN=9813820C19D4 TS_OK

INCREMENT Simulink_Requirements MLM 369 permanent uncounted \

	VENDOR_STRING=vi=0:at=200:ae=1:lu=300:lo=IN:ei=6257193:lr=1: \

	HOSTID=ANY SN=123456 SIGN=AE15C81AA9EC TS_OK

INCREMENT Simulink_Test MLM 369 permanent uncounted \

	VENDOR_STRING=vi=0:at=200:ae=1:lu=300:lo=IN:ei=6257193:lr=1: \

	HOSTID=ANY SN=123456 SIGN=0B94EC30C1E6 TS_OK

INCREMENT sl_coverage MLM 369 permanent uncounted \

	VENDOR_STRING=vi=0:at=200:ae=1:lu=300:lo=IN:ei=6257193:lr=1: \

	HOSTID=ANY SN=123456 SIGN=B7FE4748A9F2 TS_OK

INCREMENT sl_verification_validation MLM 369 permanent uncounted \

	VENDOR_STRING=vi=0:at=200:ae=1:lu=300:lo=IN:ei=6257193:lr=1: \

	HOSTID=ANY SN=123456 SIGN=D924FEA8C050 TS_OK

INCREMENT Stateflow MLM 369 permanent uncounted \

	VENDOR_STRING=vi=0:at=200:ae=1:lu=300:lo=IN:ei=6257193:lr=1: \

	HOSTID=ANY SN=123456 SIGN=C62F7A988096 TS_OK

INCREMENT Stateflow_Coder MLM 369 permanent uncounted \

	VENDOR_STRING=vi=0:at=200:ae=1:lu=300:lo=IN:ei=6257193:lr=1: \

	HOSTID=ANY SN=123456 SIGN=E86A8B1A92BE TS_OK

INCREMENT Statistics_Toolbox MLM 369 permanent uncounted \

	VENDOR_STRING=vi=0:at=200:ae=1:lu=300:lo=IN:ei=6257193:lr=1: \

	HOSTID=ANY SN=123456 SIGN=666DA9489C32 TS_OK

INCREMENT Symbolic_Toolbox MLM 369 permanent uncounted \

	VENDOR_STRING=vi=0:at=200:ae=1:lu=300:lo=IN:ei=6257193:lr=1: \

	HOSTID=ANY SN=123456 SIGN=21FD3CF6B092 TS_OK

INCREMENT SystemTest MLM 369 permanent uncounted \

	VENDOR_STRING=vi=0:at=200:ae=1:lu=300:lo=IN:ei=6257193:lr=1: \

	HOSTID=ANY SN=123456 SIGN=A52ECE3EB50C TS_OK

INCREMENT Target_Support_Package MLM 369 permanent uncounted \

	VENDOR_STRING=vi=0:at=200:ae=1:lu=300:lo=IN:ei=6257193:lr=1: \

	HOSTID=ANY SN=123456 SIGN=183AD8C25500 TS_OK

INCREMENT Text_Analytics_Toolbox MLM 369 permanent uncounted \

	VENDOR_STRING=vi=0:at=200:ae=1:lu=300:lo=IN:ei=6257193:lr=1: \

	HOSTID=ANY SN=123456 SIGN=C93274BE2C50 TS_OK

INCREMENT TRADING_TOOLBOX MLM 369 permanent uncounted \

	VENDOR_STRING=vi=0:at=200:ae=1:lu=300:lo=IN:ei=6257193:lr=1: \

	HOSTID=ANY SN=123456 SIGN=4033F00CA592 TS_OK

INCREMENT Vehicle_Dynamics_Blockset MLM 369 permanent uncounted \

	VENDOR_STRING=vi=0:at=200:ae=1:lu=300:lo=IN:ei=6257193:lr=1: \

	HOSTID=ANY SN=123456 SIGN=53545E2475D6 TS_OK

INCREMENT Vehicle_Network_Toolbox MLM 369 permanent uncounted \

	VENDOR_STRING=vi=0:at=200:ae=1:lu=300:lo=IN:ei=6257193:lr=1: \

	HOSTID=ANY SN=123456 SIGN=06FD33A6500C TS_OK

INCREMENT Video_and_Image_Blockset MLM 369 permanent uncounted \

	VENDOR_STRING=vi=0:at=200:ae=1:lu=300:lo=IN:ei=6257193:lr=1: \

	HOSTID=ANY SN=123456 SIGN=AFC4F95EF97C TS_OK

INCREMENT Virtual_Reality_Toolbox MLM 369 permanent uncounted \

	VENDOR_STRING=vi=0:at=200:ae=1:lu=300:lo=IN:ei=6257193:lr=1: \

	HOSTID=ANY SN=123456 SIGN=E18982E05F76 TS_OK

INCREMENT Vision_HDL_Toolbox MLM 369 permanent uncounted \

	VENDOR_STRING=vi=0:at=200:ae=1:lu=300:lo=IN:ei=6257193:lr=1: \

	HOSTID=ANY SN=123456 SIGN=B7CBEE12E6DE TS_OK

INCREMENT Wavelet_Toolbox MLM 369 permanent uncounted \

	VENDOR_STRING=vi=0:at=200:ae=1:lu=300:lo=IN:ei=6257193:lr=1: \

	HOSTID=ANY SN=123456 SIGN=5620DE4E8E1A TS_OK

INCREMENT WLAN_System_Toolbox MLM 369 permanent uncounted \

	VENDOR_STRING=vi=0:at=200:ae=1:lu=300:lo=IN:ei=6257193:lr=1: \

	HOSTID=ANY SN=123456 SIGN=0617D9360522 TS_OK

INCREMENT XPC_Embedded_Option MLM 369 permanent uncounted \

	VENDOR_STRING=vi=0:at=200:ae=1:lu=300:lo=IN:ei=6257193:lr=1: \

	HOSTID=ANY SN=123456 SIGN=3D79201A5002 TS_OK

INCREMENT XPC_Target MLM 369 permanent uncounted \

	VENDOR_STRING=vi=0:at=200:ae=1:lu=300:lo=IN:ei=6257193:lr=1: \

	HOSTID=ANY SN=123456 SIGN=316E1E6C5434 TS_OK

INCREMENT MATLAB_5G_Toolbox MLM 369 permanent uncounted \

	VENDOR_STRING=vi=0:at=200:ae=1:lu=300:lo=IN:ei=6257193:lr=1: \

	HOSTID=ANY SN=123456 SIGN=8583DC1EA636 TS_OK

INCREMENT Sensor_Fusion_and_Tracking MLM 369 permanent uncounted \

	VENDOR_STRING=vi=0:at=200:ae=1:lu=300:lo=IN:ei=6257193:lr=1: \

	HOSTID=ANY SN=123456 SIGN=E372A00ACE84 TS_OK

INCREMENT PolySpace_BF MLM 369 permanent uncounted \

	VENDOR_STRING=vi=0:at=200:ae=1:lu=300:lo=IN:ei=6257193:lr=1: \

	HOSTID=ANY SN=123456 SIGN=844010F4F9A0 TS_OK

INCREMENT PolySpace_BF_Engine MLM 369 permanent uncounted \

	VENDOR_STRING=vi=0:at=200:ae=1:lu=300:lo=IN:ei=6257193:lr=1: \

	HOSTID=ANY SN=123456 SIGN=8862A3D6D7DC TS_OK

INCREMENT PolySpace_BF_Server MLM 369 permanent uncounted \

	VENDOR_STRING=vi=0:at=200:ae=1:lu=300:lo=IN:ei=6257193:lr=1: \

	HOSTID=ANY SN=123456 SIGN=818517DE5E88 TS_OK

INCREMENT PolySpace_CP MLM 369 permanent uncounted \

	VENDOR_STRING=vi=0:at=200:ae=1:lu=300:lo=IN:ei=6257193:lr=1: \

	HOSTID=ANY SN=123456 SIGN=7C2CCEC42EB0 TS_OK

INCREMENT PolySpace_CP_Engine MLM 369 permanent uncounted \

	VENDOR_STRING=vi=0:at=200:ae=1:lu=300:lo=IN:ei=6257193:lr=1: \

	HOSTID=ANY SN=123456 SIGN=9C0B926A356C TS_OK

INCREMENT PolySpace_CP_Server MLM 369 permanent uncounted \

	VENDOR_STRING=vi=0:at=200:ae=1:lu=300:lo=IN:ei=6257193:lr=1: \

	HOSTID=ANY SN=123456 SIGN=48F649303232 TS_OK

INCREMENT AUTOSAR_Blockset MLM 369 permanent uncounted \

	VENDOR_STRING=vi=0:at=200:ae=1:lu=300:lo=IN:ei=6257193:lr=1: \

	HOSTID=ANY SN=123456 SIGN=F59CD894C358 TS_OK

INCREMENT System_Composer MLM 369 permanent uncounted \

	VENDOR_STRING=vi=0:at=200:ae=1:lu=300:lo=IN:ei=6257193:lr=1: \

	HOSTID=ANY SN=123456 SIGN=64A67D287C12 TS_OK

INCREMENT SoC_Blockset MLM 369 permanent uncounted \

	VENDOR_STRING=vi=0:at=200:ae=1:lu=300:lo=IN:ei=6257193:lr=1: \

	HOSTID=ANY SN=123456 SIGN=5080646CB4CA TS_OK

INCREMENT SerDes_Toolbox MLM 369 permanent uncounted \

	VENDOR_STRING=vi=0:at=200:ae=1:lu=300:lo=IN:ei=6257193:lr=1: \

	HOSTID=ANY SN=123456 SIGN=A76AB9C02DEA TS_OK

INCREMENT Reinforcement_Learn_Toolbox MLM 369 permanent uncounted \

	VENDOR_STRING=vi=0:at=200:ae=1:lu=300:lo=IN:ei=6257193:lr=1: \

	HOSTID=ANY SN=123456 SIGN=667F745271E6 TS_OK

INCREMENT Mixed_Signal_Blockset MLM 369 permanent uncounted \

	VENDOR_STRING=vi=0:at=200:ae=1:lu=300:lo=IN:ei=6257193:lr=1: \

	HOSTID=ANY SN=123456 SIGN=06EEE99C143E TS_OK

 TS_OK

 ```
