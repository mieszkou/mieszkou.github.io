---
title: "Windows: Update error 0x80070643"
description: 
date: 2022-05-16
image: 
hidden: false
comments: true
draft: false
tags:
    - windows
    - windowsupdate
    - windowserror
categories:
    - Windows update
---

## Windows Update error 0x80070643

Here’s what you can do to fix the issue.

Rename the SoftwareDistribution folder

To solve this, it is advisable to rename the SoftwareDistribution folder. To rename the Software Distribution folder, open an elevated command prompt windows, type the following commands one after the other, and hit Enter:

```
net stop wuauserv
net stop bits
rename c:windowsSoftwareDistribution SoftwareDistribution.bak
pause
net start wuauserv
net start bits
pause
```
 
Next clear the contents of the Catroot2 folder.
Clear Catroot2 folder contents
 
Catroot and Catroot2 are the some of the important Windows OS folders which are required while Windows Updates process. So, if you are facing the problem while updating your Windows and receiving error message – 0x80070643, then reset the Catroot2 folder.

To reset the catroot2 folder do this:
Open an elevated Command Prompt, type the following command one after the other and hit Enter:
```
net stop cryptsvc
md %systemroot%system32catroot2.old
xcopy %systemroot%system32catroot2 %systemroot%system32catroot2.old /s
```
Next, delete all the contents of the catroot2 folder.

Having done this, in the CMD windows, type the following and hit Enter:
```
net start cryptsvc
```

Your catroot folder will be reset, once you start Windows Update again.

---------------------

svchost.exe i duże użycie procesora:
Zatrzymaj usługę Windows Update i usuń folder c:windowssoftware distribution
po restarcie powstanie nowy


3 things you should do if Window is unable to install the driver ...
This problem is the result of the Windows Update agent file (Wups2.dll) not being registered correctly. To resolve the problem, register the Windows Update files. Or, you can download and install the Windows Update agent. By ensuring that the Windows Update file is registered correctly, you will also be ensuring that any additional keys are also registered. To register the Windows Update files, create a file named register.bat and save it to the desktop. For Windows XP, Windows Server 2003, or Windows 2000, the .bat file should contain the following:

1. REGSVR32 WUPS2.DLL /S
2. REGSVR32 WUPS.DLL /S
3. REGSVR32 WUAUENG.DLL /S
4. REGSVR32 WUAPI.DLL /S
5. REGSVR32 MUCLTUI.DLL /S
6. REGSVR32 WUCLTUI.DLL /S
7. REGSVR32 WUWEB.DLL /S
8. REGSVR32 MUWEB.DLL /S
9. REGSVR32 QMGR.DLL /S

REGSVR32 QMGRPRXY.DLL /S

If you are running Vista or Windows Server 2008, the .bat file should contain the following:

1. REGSVR32 WUPS2.DLL /S
2. REGSVR32 WUPS.DLL /S
3. REGSVR32 WUAUENG.DLL /S
4. REGSVR32 WUAPI.DLL /S
5. REGSVR32 WUCLTUX.DLL /S
6. REGSVR32 WUWEBV.DLL /S
7. REGSVR32 JSCRIPT.DLL /S

REGSVR32 MSXML3.DLL /S
