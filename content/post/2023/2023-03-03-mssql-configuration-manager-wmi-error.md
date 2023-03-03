---
title: "SQL Server Config manager error: Cannot connect to WMI provider"
description: "SQL Server Config manager error: Cannot connect to WMI provider"
date: 2023-03-03
image: 
hidden: false
comments: true
draft: false
tags:
    - sql
    - mssql
    - wmi
    - error
categories:
    - SQL
---

# SQL Server Config manager error: Cannot connect to WMI provider

Run Cmd as Administrator and execute these commands:

First go to SQL Shared folder according to your sql version:

```bash
SQL 2008: C:\Program Files (x86)\Microsoft SQL Server\100\Shared\
SQL 2012: C:\Program Files (x86)\Microsoft SQL Server\110\Shared\
SQL 2014: C:\Program Files (x86)\Microsoft SQL Server\120\Shared\
SQL 2017: C:\Program Files (x86)\Microsoft SQL Server\140\Shared\ -------> My version is 2017 SQL 2019: C:\Program Files (x86)\Microsoft SQL Server\150\Shared\
```

Find more versions here

```
cd "C:\Program Files (x86)\Microsoft SQL Server\140\Shared"
```
Then:

```
mofcomp sqlmgmproviderxpsp2up.mof
```

### Update:

The problem occurs because the Windows Management Instrumentation (WMI) provider configuration file for manage SQL Server services is missing. So the mofcomp command repairs or recreates it.

Here is more explanation: https://learn.microsoft.com/en-us/windows/desktop/wmisdk/mofcomp

src: https://stackoverflow.com/questions/44753745/sql-server-config-manager-error-cannot-connect-to-wmi-provider