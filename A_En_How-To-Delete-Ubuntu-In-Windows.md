---
title: How to uninstall ubuntu with windows/ubuntu dual system
date: 2019-10-17 16:42:14
tags: 
- Ubuntu
categories: 
- 技术
- EnglishNotes
---

 https://www.jianshu.com/p/66a092caaa36?tdsourcetag=s_pctim_aiomsg 

***This is original from above blog.***

 On a dual-system computer, if you use Ubuntu's built-in grub program as boot to boot, you cannot directly format the disk on windows where Ubuntu is located, otherwise the MBR contents on the hard disk will be wiped out and the boot will not succeed. 

To uninstall Ubuntu, you need to first delete its MBR content and then format its hard disk. For different computers, there are different ways to modify the MBR, so the first step is to identify the BIOS boot type, the method is: 

`Win+R` open and run, enter `msinfo32`, press enter to view system information

If **traditional** is displayed in BIOS mode, the boot  method is **Legacy BIOS**. If **UEFI** is displayed, then the boot method is **UEFI**.

### If Legacy BIOS is enabled

1.1 download the Mbrfix tool and place it anywhere, such as: 'D\Tools\'

1.2 run the command prompt as the administrator to enter the MBRfix tool directory, for example:

```bash
D:
cd \Tools
```

1.3 entering

```undefined
MbrFix /drive 0 fixmbr /yes
```

1.4 restart the computer, see whether directly into the Win10 system, if so, that deleted successfully



### If UEFI BIOS is enabled

2.1 download Easy UEFI

[Easy UEFI] (https://www.easyuefi.com/index-cn.html)

2.2 after installing UEFI, enter the function of management EFI startup and delete the EFI partition of Ubuntu

2.3 restart the computer, directly enter Win10, successful



After successfully modifying the MBR content, you can directly format the corresponding hard disk of Ubuntu











